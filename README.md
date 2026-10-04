# Optimización de Precios y Detección de Anomalías en el Mercado Inmobiliario

Proyecto Integrador – Data Mining Tools (CC209), Universidad Peruana de Ciencias Aplicadas.
TP1 (semana 7) y TF1 (semana 15).

## Integrantes
- Jairo Luis Orihuela Paredes (U202319900)
- Jilary Avril Torres
- Sebastian Timana
- Iván Cunyas

## Problema
Estimar el precio de venta de una vivienda en King County (Seattle, EE. UU.) a partir de sus características físicas y su ubicación, y marcar las ventas cuyo precio se aleja de lo que el modelo espera.

- **Unidad de análisis:** una venta de vivienda.
- **Pregunta principal:** ¿con qué error puede estimarse el precio de venta de una vivienda a partir de sus características físicas y su ubicación, y qué ventas se desvían de forma anómala de lo que el modelo espera?
- **Tipo de problema:** regresión (principal) y detección de anomalías basada en residuos (exploratoria).
- **Criterio de utilidad:** mejora de al menos 15 % relativo sobre el mejor baseline (la regla por zona).

## Dataset
King County House Sales, Kaggle: <https://www.kaggle.com/datasets/harlfoxem/housesalesprediction>
21 613 ventas × 21 variables, del 2014-05-02 al 2015-05-27; sin valores nulos. Detalle, diccionario de variables y limitaciones en [`data/README.md`](data/README.md). Licencia: la indicada en la página del dataset en Kaggle.

Los datos **no se versionan**: el notebook `01` los descarga con `kagglehub` a `data/raw/`.

## Resultados del TP1 (test, evaluado una sola vez)
| Modelo | MAE (USD) | R² | MdAPE | Dentro de ±20 % |
|---|---|---|---|---|
| Mejor baseline (regla por zona) | 101 791 | 0.80 | 14.0 % | 65.2 % |
| **XGBoost** | **66 446** | **0.90** | **8.6 %** | **82.9 %** |

XGBoost reduce el MAE entre 32 % y 37 % y el MdAPE entre 35 % y 43 % frente a la mejor regla simple (intervalos del 95 %). Random Forest y XGBoost empatan en error relativo mediano.

**Limitaciones:** un solo condado y ~13 meses de ventas; el split es aleatorio y no mide el desempeño con ventas futuras; hiperparámetros sin optimizar. Las ventas marcadas como anómalas son candidatas, no anomalías confirmadas. Ver los notebooks y `reports/INDEX.md`.

## Estructura del repositorio
```
data/
  raw/          datos originales (no se versionan)
  interim/      datos tras la limpieza (no se versionan)
  processed/    índices del split (no se versionan)
notebooks/      análisis numerados y ejecutados
models/         pipeline entrenado (.joblib, no se versiona)
reports/
  figures/      figuras para el informe (PNG)
  tables/       tablas de resultados (CSV)
  INDEX.md      qué contiene cada figura/tabla y las cifras clave
docs/
  enunciado_proyecto.md        enunciado del curso
  decisiones_herramientas.md   matriz de herramientas y tabla TP1 → TF1
  tp/pasos_tp1.md              pasos del TP1 con su avance
app/  src/  tests/             reservados para el TF1
```

## Notebooks (ejecutar en este orden)
| Notebook | Contenido |
|---|---|
| `01_problema_y_datos.ipynb` | Descarga, registro de datos y definición del problema |
| `02_eda.ipynb` | Auditoría inicial y EDA guiado por preguntas |
| `03_calidad_y_preparacion.ipynb` | Calidad de datos, reglas lógicas y dataset limpio |
| `04_baseline_y_modelos.ipynb` | Split sin fuga, pipeline, baselines, modelos, evaluación, anomalías y plan hacia el TF1 |

Dependencias entre notebooks: `02` y `03` leen el CSV crudo que descarga `01`, y `04` lee el CSV limpio que escribe `03`.

## Ejecución
Requiere Python 3.12.

```bash
python -m venv .venv
.venv\Scripts\activate            # en Linux/macOS: source .venv/bin/activate
pip install -r requirements.txt
```

Abrir los notebooks desde VS Code (con el `.venv` como kernel) o ejecutarlos desde la terminal, en orden:

```bash
cd notebooks
jupyter nbconvert --to notebook --execute --inplace 01_problema_y_datos.ipynb
jupyter nbconvert --to notebook --execute --inplace 02_eda.ipynb
jupyter nbconvert --to notebook --execute --inplace 03_calidad_y_preparacion.ipynb
jupyter nbconvert --to notebook --execute --inplace 04_baseline_y_modelos.ipynb
```

La semilla es `RANDOM_STATE = 42`; los resultados son reproducibles. Al ejecutar, los notebooks regeneran `reports/figures/`, `reports/tables/`, `data/interim/`, `data/processed/split.csv` y `models/xgb_pipeline_tp1.joblib`.

## Estado
- **TP1:** pasos 0 a 12 completos (ver `docs/tp/pasos_tp1.md`). Pendientes de entrega: presentación en PDF o PPTX, informe y acceso del docente al repositorio.
- **TF1:** plan en el notebook `04`, sección 12.


