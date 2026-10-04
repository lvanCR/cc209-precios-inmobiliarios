# Pasos del proyecto hasta el TP1 (semana 7)

Dataset: **King County House Sales** (`harlfoxem/housesalesprediction`, Kaggle).
Entorno: `D:\Topicos de computacion\.venv` (Python 3.12).
Alcance: desde la descarga de datos hasta los primeros modelos. Clustering/PCA, Optuna, SHAP y despliegue quedan para el TF1.

> Referencia del enunciado: `docs/enunciado_proyecto.md`, sección 4. Entre paréntesis, el criterio de la rúbrica (20 pts) que cubre cada paso.

---

## Paso 0. Preparación del entorno
- [x] Seleccionar el `.venv` como kernel de los notebooks.
- [x] Ajustar `requirements.txt` a lo que realmente se usa (con versiones).
- [x] Definir semilla global (`RANDOM_STATE = 42`) en la celda de configuración del notebook 01.
- [x] Definir rutas (`data/raw`, `data/processed`, `models`) en esa misma celda.

## Paso 1. Descarga y registro de datos (Problema y dataset, 3 pts)
- [x] Descargar con `kagglehub.dataset_download("harlfoxem/housesalesprediction")`.
- [x] Copiar el CSV a `data/raw/` sin modificarlo (los datos crudos son inmutables).
- [x] Anotar en `data/README.md`: fuente, URL, licencia (pendiente de verificar en la página de Kaggle), nº de filas y columnas, período (aprox. mayo 2014 – mayo 2015), variable objetivo (`price`).
- [x] Redactar el diccionario de variables (`id`, `date`, `price`, `bedrooms`, `bathrooms`, `sqft_living`, `sqft_lot`, `floors`, `waterfront`, `view`, `condition`, `grade`, `sqft_above`, `sqft_basement`, `yr_built`, `yr_renovated`, `zipcode`, `lat`, `long`, `sqft_living15`, `sqft_lot15`).
- [x] Documentar limitaciones conocidas: un solo condado, un solo año, solo ventas cerradas (no precio de oferta), sin variables de entorno (colegios, criminalidad, etc.).

## Paso 2. Definición del problema (Problema y dataset, 3 pts)
Notebook: `notebooks/01_problema_y_datos.ipynb`
- [x] Contexto y necesidad (tasación de viviendas, detección de precios fuera de mercado).
- [x] Unidad de análisis: una venta de vivienda.
- [x] Pregunta principal, concreta. Borrador:
  > ¿Con qué error puede estimarse el precio de venta de una vivienda en King County a partir de sus características físicas y su ubicación, y qué ventas se desvían de forma anómala de lo que el modelo espera?
- [x] Tipo de problema: regresión (principal) + detección de anomalías basada en residuos (secundario).
- [x] Criterios de utilidad: definir un umbral antes de modelar (por ejemplo, error mediano relativo menor al X % y mejora clara sobre el baseline).
- [x] Qué NO se pretende afirmar (el modelo predice precio de cierre, no valor "justo").

## Paso 3. Carga y auditoría inicial (Calidad y preparación, 4 pts)
Notebook: `notebooks/02_eda.ipynb` (inicio)
- [x] `shape`, `dtypes`, `describe()`, vistazo a las primeras filas.
- [x] Convertir `date` a fecha; derivar año/mes de venta (solo en análisis, no tocar el crudo).
- [x] Verificar la unicidad de `id`: hay viviendas vendidas más de una vez (ventas repetidas). Esto afecta el split (ver Paso 6).

## Paso 4. EDA guiado por preguntas (EDA, 4 pts)
Notebook: `notebooks/02_eda.ipynb`
Cada gráfico lleva una interpretación escrita, separando **lo que muestran los datos** de **lo que interpretamos**.
- [x] **Variable objetivo:** distribución de `price` (asimetría fuerte a la derecha); comparar con `log(price)`. Decide si el modelo usará el objetivo transformado.
- [x] **Tamaño vs precio:** `sqft_living` vs `price` (¿relación lineal? ¿heterocedasticidad?). Idem `grade`, `bathrooms`, `bedrooms`.
- [x] **Ubicación:** mapa de dispersión (`lat`/`long`) coloreado por precio; precio mediano por `zipcode`; efecto de `waterfront` y `view`.
- [x] **Antigüedad:** `yr_built`, `yr_renovated` (0 = nunca renovada) y su relación con el precio.
- [x] **Diferencias entre grupos:** precio por `condition`, `grade`, `waterfront`.
- [x] **Correlaciones:** matriz de correlación (Spearman) y multicolinealidad (`sqft_living` vs `sqft_above`, etc.).
- [x] **Anomalías visibles:** casos extremos de precio, tamaño y número de habitaciones.
- [x] Cerrar con una lista de "hallazgos que condicionan la preparación".

## Paso 5. Calidad y preparación de datos (Calidad y preparación, 4 pts)
Notebook: `notebooks/03_calidad_y_preparacion.ipynb`
Para cada punto: detectar → decidir → justificar → registrar.
- [x] **Faltantes:** contar nulos por columna (el dataset suele venir completo; verificarlo, no suponerlo).
- [x] **Duplicados:** filas completamente duplicadas vs. `id` repetidos (ventas distintas de la misma casa).
- [x] **Tipos:** `date` a fecha; `zipcode` como categórica, no numérica; `waterfront` binaria.
- [x] **Reglas lógicas:** `bedrooms = 0` o `bathrooms = 0`, la vivienda con ~33 habitaciones, `sqft_above + sqft_basement = sqft_living`, `yr_renovated < yr_built`.
- [x] **Outliers:** distinguir error de dato (corregir/descartar) de valor extremo legítimo (conservar). No eliminar por defecto: este es un proyecto de detección de anomalías, así que los extremos son parte del objeto de estudio.
- [x] **Transformaciones candidatas:** `log` del precio; `log1p` de `sqft_lot`; variables derivadas (`antiguedad`, `renovada` binaria, `tiene_sotano`).
- [x] Guardar el dataset limpio en `data/interim/` y registrar cada decisión en una tabla (problema, evidencia, decisión, justificación, riesgo).

## Paso 6. Separación de datos y control de leakage (Split y leakage, 2 pts)
- [x] Estrategia: partición **train / validation / test** (por ejemplo 70/15/15) o **train/test + validación cruzada** sobre train. Justificar la elección.
- [x] Evitar fuga por ventas repetidas: que un mismo `id` quede en un solo conjunto (`GroupShuffleSplit` / `GroupKFold`).
- [x] Decidir si se justifica un split temporal (entrenar con ventas anteriores y probar con posteriores) y discutir por qué sí o no: el período es solo de un año.
- [x] Hacer el split **antes** de ajustar cualquier transformación (escaladores, codificadores, imputadores).
- [x] No usar el conjunto de test hasta la evaluación final.
- [x] Revisar variables que podrían filtrar información del objetivo (por ejemplo, agregados de precio por zona calculados con todos los datos). Si se usan, calcularlos solo con train.
- [x] Guardar los índices de cada partición para poder reproducirla.

## Paso 7. Pipeline reproducible (Flujo reproducible, 2 pts)
Código en `src/`, usado desde `notebooks/04_baseline_y_modelos.ipynb`
- [x] `ColumnTransformer` con ramas diferenciadas:
  - numéricas asimétricas → `log1p` + `StandardScaler` (para modelos lineales);
  - numéricas restantes → escalado (solo si el modelo lo requiere);
  - categóricas (`zipcode`, `condition`, `grade`) → `OneHotEncoder(handle_unknown="ignore")` o codificación ordinal según el caso;
  - binarias → paso directo.
- [x] `Pipeline` = preprocesamiento + modelo, de modo que `fit` solo ve train.
- [x] Objetivo transformado con `TransformedTargetRegressor` (`log` / `exp`).
- [x] Guardar el pipeline con `joblib` en `models/`.

## Paso 8. Baseline (Baseline, modelos y evaluación, 3 pts)
- [ ] `DummyRegressor(strategy="median")` como piso absoluto.
- [ ] Un baseline de dominio: regresión lineal simple con `sqft_living`, o precio mediano por `zipcode`.
- [ ] Reportar sus métricas con el mismo protocolo que los modelos.

## Paso 9. Modelos preliminares (Baseline, modelos y evaluación, 3 pts)
- [ ] Mínimo **dos** modelos comparables. Propuesta:
  1. Modelo lineal regularizado (`Ridge`) como referencia interpretable.
  2. `RandomForestRegressor`.
  3. `XGBRegressor` (opcional en TP1; se puede dejar para el TF1).
- [ ] Hiperparámetros por defecto o una búsqueda mínima. La optimización sistemática (Optuna, MLflow) es del TF1.
- [ ] Mismos datos, mismo split y misma semilla para todos, para que la comparación sea justa.

## Paso 10. Evaluación preliminar (Baseline, modelos y evaluación, 3 pts)
- [ ] Métricas, cada una con su justificación:
  - **MAE** en dólares (fácil de interpretar);
  - **RMSE** (penaliza errores grandes);
  - **R²**;
  - **error porcentual mediano (MdAPE)**: el error absoluto en dólares engaña entre casas de 150 mil y de 3 millones.
- [ ] Evaluar en validación (o en CV sobre train). **El test se toca una sola vez**, al final.
- [ ] Tabla comparativa: baseline vs. modelos, con interpretación en lenguaje del problema ("el modelo se equivoca en promedio X %…").
- [ ] Gráficos: real vs. predicho, residuos vs. predicho (¿heterocedasticidad?), distribución del error.
- [ ] Revisión rápida de dónde falla más: por rango de precio y por zona (el análisis profundo es del TF1).

## Paso 11. Primer vistazo a anomalías (opcional en TP1)
- [ ] Marcar como candidatas las ventas con residuo extremo (por ejemplo, |residuo| mayor al percentil 99).
- [ ] Comparar con la detección independiente por `IsolationForest`.
- [ ] Dejar claro que es exploratorio: un residuo grande puede ser un error del modelo y no una anomalía real.

## Paso 12. Estado del proyecto y plan hacia el TF1 (Análisis crítico y plan, 2 pts)
- [ ] Hallazgos principales hasta ahora.
- [ ] Problemas no resueltos y limitaciones (por ejemplo, un solo año de datos, ausencia de variables de entorno).
- [ ] Plan concreto hacia el TF1, conectado con los resultados:
  - clustering o PCA de zonas (si el error se concentra geográficamente);
  - Optuna + MLflow;
  - SHAP;
  - análisis de errores;
  - Streamlit o FastAPI;
  - tabla de evolución TP1 → TF1.

## Paso 13. Entregables del TP1
- [ ] Notebooks 01–04 ejecutados de principio a fin, con resultados visibles.
- [ ] `README.md` con problema, fuente de datos, instrucciones de ejecución y estructura.
- [ ] `requirements.txt` actualizado.
- [ ] Matriz de decisiones de herramientas (`docs/decisiones_herramientas.md`) con las columnas EDA, Preparación y Modelamiento llenas.
- [ ] Presentación en PDF o PPTX: **10 min** de exposición + 5 de preguntas, con todos los integrantes participando. Priorizar problema, evidencia, decisiones y resultados, y pocos bloques de código.
- [ ] Declaración breve de uso de IA generativa.
- [ ] Acceso del docente al repositorio.

---

## Orden de trabajo sugerido

| Orden | Paso | Notebook / archivo |
|---|---|---|
| 1 | 0–1 Entorno y descarga | `src/config.py`, `data/README.md` |
| 2 | 2 Problema | `01_problema_y_datos.ipynb` |
| 3 | 3–4 Auditoría y EDA | `02_eda.ipynb` |
| 4 | 5 Calidad y preparación | `03_calidad_y_preparacion.ipynb` |
| 5 | 6–7 Split y pipeline | `src/`, `04_baseline_y_modelos.ipynb` |
| 6 | 8–10 Baseline, modelos, evaluación | `04_baseline_y_modelos.ipynb` |
| 7 | 11–12 Anomalías y plan | `04_...` + presentación |
| 8 | 13 Entregables | README, PDF/PPTX |

## Puntos que el grupo debe decidir
1. **Split:** ¿70/15/15 o train/test más CV? ¿Se justifica uno temporal?
2. **Objetivo:** ¿modelar `price` o `log(price)`? (Se decide con la evidencia del EDA.)
3. **Outliers:** criterio para distinguir error de dato de valor extremo legítimo.
4. **Umbral de utilidad:** qué error se considera aceptable.
5. **Segundo modelo:** ¿Random Forest ahora y XGBoost en el TF1, o ambos desde el TP1?
