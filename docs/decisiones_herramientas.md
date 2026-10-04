# Matriz de decisiones de herramientas

Las filas marcadas **(propuesto TF1)** aún no se implementan: son la decisión prevista y su justificación.

| Necesidad | Herramienta elegida | Alternativa considerada | Justificación |
|---|---|---|---|
| EDA | `pandas` + `matplotlib` / `seaborn` | `plotly` (interactivo); `ydata-profiling` (informe automático) | Las preguntas del EDA son específicas (precio vs tamaño, ubicación, antigüedad) y cada gráfico debe llevar interpretación. Un informe automático produce muchos gráficos sin criterio, justo lo que el enunciado desaconseja. `matplotlib`/`seaborn` permiten figuras estáticas reproducibles que se guardan para el informe |
| Preparación | `pandas` para reglas fijas fila a fila; `Pipeline` + `ColumnTransformer` de `scikit-learn` para todo lo que se ajusta | Limpieza manual en el notebook; `feature-engine` | Separar reglas fijas (no usan estadísticas del dataset) de transformaciones aprendidas evita fuga de información: imputador, escalador y codificador se ajustan solo con *train*. El mismo objeto se reutiliza en validación cruzada y en la aplicación |
| Separación de datos | `GroupShuffleSplit` (por `id`) | `train_test_split` simple; split temporal | Hay 176 viviendas vendidas varias veces. Un split aleatorio simple las repartiría entre *train* y *test* y haría que el error pareciera menor al real. El split temporal se descartó por cubrir solo ~13 meses (se revisará como prueba de robustez en el TF1) |
| Objetivo | `TransformedTargetRegressor` con `log` / `exp` | Modelar `price` directo; `log` manual | El precio tiene asimetría 4.0 (0.43 con log). Encapsular la transformación en el pipeline garantiza que las predicciones salgan en USD y que no se olvide invertirla |
| Modelamiento | `Ridge`, `RandomForestRegressor` (`scikit-learn`) y `XGBRegressor` (`xgboost`) | `LightGBM`, `CatBoost`; regresión lineal sin regularizar | Cubren una referencia lineal interpretable y dos familias de árboles. Ridge controla la multicolinealidad (`sqft_above` / `sqft_living`) y las 70 columnas de `zipcode`. `LightGBM` y `CatBoost` no se probaron para no ampliar la comparación sin motivo: el resultado entre RF y XGBoost ya está dentro del ruido |
| Baseline | `DummyRegressor`, regresión lineal simple y regla por zona (USD/pie² × tamaño) | Solo `DummyRegressor` | Un baseline trivial no basta: la regla por zona ya cumplía el umbral inicial de MdAPE ≤ 15 %. Se mide la mejora contra la referencia más fuerte |
| Métricas | MAE, RMSE, R², **MdAPE** y % dentro de ±20 % | Solo RMSE o R² | Las métricas en USD engañan entre casas de 150 mil y de 3 millones; el error porcentual mediano refleja el error típico y es el que usa el criterio de utilidad |
| Incertidumbre | *Bootstrap* sobre validation y test (1 000 réplicas) | Reportar solo el valor puntual | Con ~3 200 ventas por partición, una diferencia pequeña puede ser ruido; los intervalos permiten decir cuáles diferencias son reales |
| Anomalías | Residuo robusto (z con MAD) e `IsolationForest` | Solo residuo; `LocalOutlierFactor` | Dos criterios independientes permiten ver cuánto coinciden (18 ventas frente a 5 esperadas por azar) y no depender de un único método |
| Experimentación **(propuesto TF1)** | `GroupKFold` + `Optuna`, con registro en `MLflow` | `GridSearchCV`; registro manual en CSV | Optuna explora mejor el espacio de hiperparámetros con menos pruebas; MLflow permite saber qué configuración produjo cada resultado. `GroupKFold` mantiene todas las ventas de un `id` en el mismo pliegue |
| Técnica adicional **(propuesto TF1)** | Clustering de zonas (`K-Means` / `DBSCAN` sobre `lat`/`long`) y `PCA` | `UMAP`; usar solo `zipcode` | La ubicación explica ~40 % de la importancia y `zipcode` suma 70 columnas. Se conserva solo si mejora el error o reduce la dimensión |
| Interpretabilidad **(propuesto TF1)** | `SHAP` (global y local) | Importancia por ganancia; *permutation importance* | La importancia por ganancia se reparte entre variables correlacionadas. SHAP da explicaciones por predicción y permite revisar casos concretos |
| Despliegue **(propuesto TF1)** | `Streamlit` cargando el pipeline guardado | `FastAPI`; `Docker` | Una interfaz interactiva muestra mejor el uso del modelo en la exposición. FastAPI sería preferible si se necesitara un servicio consumible por otros sistemas |

# Tabla de evolución TP1 → TF1

La columna TF1 se completa con lo que efectivamente se haga; hoy contiene lo previsto.

| Elemento | TP1 | TF1 | Motivo del cambio |
|---|---|---|---|
| Preparación | Reglas fijas (ceros imposibles a `NaN`, variables derivadas); `ColumnTransformer` con `log1p`, imputación por mediana, escalado y *one-hot* de `zipcode` | _por definir_ (zonas por clustering en lugar de, o junto a, `zipcode`) | `zipcode` suma 70 columnas y el error por zona varía de 4.7 % a 15.9 % |
| Variables | 19 predictores (`zipcode`, `lat`/`long`, superficies, `grade`, etc.) | _por definir_ | _por definir_ |
| Modelo(s) | Ridge, Random Forest y XGBoost con hiperparámetros por defecto o casi por defecto | _por definir_ (hiperparámetros optimizados) | RF y XGBoost empatan en MdAPE; no hay ajuste |
| Métricas | MAE, RMSE, R², MdAPE y % dentro de ±20 %, con *bootstrap* sobre una partición | _por definir_ (validación cruzada agrupada) | Las diferencias entre modelos se midieron en una sola partición |
| Validación | Split 70/15/15 agrupado por `id` | _por definir_ (CV agrupada + prueba temporal) | El split aleatorio no mide el desempeño con ventas futuras |
| Otras decisiones | Umbral de utilidad: mejora de al menos 15 % relativo sobre el mejor baseline (propuesta) | _por definir_ | El umbral inicial (MdAPE ≤ 15 %) lo cumplía una regla sin aprendizaje |
