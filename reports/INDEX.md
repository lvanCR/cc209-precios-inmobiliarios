# Insumos para el informe

Todas las figuras (`reports/figures/`) y tablas (`reports/tables/`) se **regeneran** al ejecutar los notebooks en orden (`01` → `04`). Las figuras están en PNG a 150 dpi.

## Figuras

| Archivo | Qué muestra | Notebook · sección | Idea para el informe |
|---|---|---|---|
| `eda_01_ventas_por_mes.png` | Ventas por mes (mayo 2014 – mayo 2015) | 02 · 3.1 | Cobertura temporal; mayo de 2015 es parcial por el corte del dataset |
| `eda_02_distribucion_precio.png` | Distribución de `price` y de `log(price)` | 02 · 4.1 | Justifica modelar `log(price)`: asimetría 4.0 → 0.43 |
| `eda_03_tamano_vs_precio.png` | `sqft_living` vs `price`, en escala original y logarítmica | 02 · 4.2 | La dispersión crece con el tamaño; la escala log la estabiliza |
| `eda_04_grade_view_condition.png` | Precio por `grade`, `view` y `condition` | 02 · 4.3 | `grade` y `view` ordenan el precio; `condition` casi no |
| `eda_05_mapa_precio.png` | Mapa (`lat`/`long`) coloreado por precio | 02 · 4.4 | La ubicación es un determinante fuerte |
| `eda_06_correlaciones.png` | Correlación de Spearman entre variables | 02 · 4.6 | Redundancia entre superficies; qué variables se asocian con el precio |
| `split_01_precio_mediano_por_mes.png` | Precio mediano mensual | 04 · 6.1 | Sustenta no usar un split temporal (precio estable, ±5 %) |
| `modelo_01_comparacion_validation.png` | MdAPE y MAE de baselines y modelos, con IC 95 % | 04 · 9.1 | Figura central de la comparación de modelos |
| `modelo_02_real_vs_predicho_validation.png` | Real vs predicho, error vs predicho y distribución del error (XGBoost) | 04 · 10.1 | Calidad del ajuste y forma del error |
| `modelo_03_error_por_rango_precio.png` | MdAPE por quintil de precio y sesgo de XGBoost | 04 · 10.2 | El error es mayor en los extremos; el sesgo cambia de signo |
| `modelo_04_importancia_variables.png` | Importancia de variables de XGBoost | 04 · 10.3 | Qué usa el modelo: `grade`, `zipcode`, `lat`, `sqft_living` |
| `modelo_05_real_vs_predicho_test.png` | Real vs predicho y distribución del error en test | 04 · 10.4 | Evaluación final |
| `anomalias_01_residuos_e_isolation_forest.png` | Residuos marcados y comparación con Isolation Forest | 04 · 11 | Candidatas a anomalía (exploratorio) |

## Tablas (CSV)

| Archivo | Contenido |
|---|---|
| `eda_ventas_por_mes.csv`, `eda_precio_por_grade.csv`, `eda_precio_por_zipcode.csv`, `eda_dispersion_por_cuartil_sqft.csv`, `eda_correlacion_spearman.csv` | Tablas de apoyo del EDA |
| `split_tamanos.csv`, `split_comparacion_precio.csv` | Tamaño de las particiones y comparación del precio entre ellas |
| `modelos_metricas_validation.csv` | Métricas de baselines y modelos en validation |
| `modelos_intervalos_bootstrap_validation.csv`, `modelos_diferencias_bootstrap_validation.csv` | Intervalos del 95 % y diferencias entre modelos |
| `modelos_error_por_rango_precio_validation.csv`, `modelos_error_por_zipcode_validation.csv` | Dónde falla más el modelo |
| `modelos_importancia_xgboost.csv` | Importancia de variables (con `zipcode` agrupado) |
| `modelos_metricas_test_final.csv`, `modelos_xgboost_validation_vs_test.csv`, `modelos_intervalos_bootstrap_test.csv`, `modelos_criterios_utilidad.csv` | Evaluación final en test y criterios de utilidad |
| `anomalias_candidatas_validation.csv` | Ventas marcadas por el residuo robusto |

Los registros de decisiones de calidad (Paso 5) y de hallazgos del EDA (4.8) están como tablas en los notebooks `03` y `02`; se pueden copiar de ahí.

## Cifras clave

**Dataset:** King County House Sales · 21 613 ventas × 21 variables · 2014-05-02 a 2015-05-27 · 0 nulos · 176 viviendas vendidas más de una vez (177 `id` repetidos).

**Split:** 70 / 15 / 15 agrupado por `id` (15 130 / 3 242 / 3 241).

**Validation**

| Modelo | MAE (USD) | RMSE (USD) | R² | MdAPE | ± 20 % |
|---|---|---|---|---|---|
| B1 · Mediana global | 219 515 | 368 055 | −0.05 | 34.3 % | 29.9 % |
| B2 · Lineal simple | 166 401 | 273 689 | 0.42 | 26.2 % | 38.3 % |
| B3 · Regla por zona | 100 340 | 173 632 | 0.77 | 14.3 % | 64.2 % |
| Ridge | 73 487 | 126 817 | 0.87 | 10.1 % | 78.6 % |
| Random Forest | 69 894 | 131 481 | 0.87 | 8.7 % | 80.9 % |
| XGBoost | 64 949 | 112 824 | 0.90 | 8.7 % | 82.2 % |

**Test (evaluado una sola vez)**

| Modelo | MAE (USD) | RMSE (USD) | R² | MdAPE | ± 20 % |
|---|---|---|---|---|---|
| B3 · Regla por zona | 101 791 | 178 862 | 0.80 | 14.0 % | 65.2 % |
| **XGBoost** | **66 446** | **126 805** | **0.90** | **8.6 %** | **82.9 %** |

Intervalos del 95 % (bootstrap, test): MdAPE de XGBoost 8.2 %–9.1 %; reducción frente a B3 de 31.8 %–37.4 % en MAE y 35.3 %–43.0 % en MdAPE.

## Qué debe quedar claro en el informe
- **Evidencia, interpretación e hipótesis están separadas** en los notebooks: respetar esa distinción.
- **El umbral de utilidad se revisó:** el baseline por zona ya cumplía MdAPE ≤ 15 %, por lo que el criterio que manda es la mejora relativa de al menos 15 % sobre el mejor baseline (propuesta pendiente de validar por el grupo).
- **RF y XGBoost empatan en MdAPE;** la diferencia de MAE (~4 900 USD) es de una sola partición.
- **Qué no puede concluirse:** que el modelo funcione con ventas futuras o de otras zonas; que las variables importantes causen el precio; que las ventas marcadas sean anomalías reales.
- **El test se usó una vez.** No debe usarse para decidir nada en el TF1.
