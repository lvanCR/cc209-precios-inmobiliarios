# Optimización de Precios y Detección de Anomalías en el Mercado Inmobiliario

Proyecto Integrador – Data Mining Tools (CC209), UPC.
TP1 (semana 7) y TF1 (semana 15).

## Integrantes
- _completar_

## Problema
_Contexto, unidad de análisis, pregunta principal, tipo de problema (regresión + detección de anomalías), criterios de utilidad._

## Dataset
_Fuente, licencia, nº de observaciones/variables, período, variable objetivo, limitaciones._ Ver `data/README.md`.

## Estructura del repositorio
```
data/
  raw/          datos originales (inmutables, no se versionan)
  interim/      datos intermedios (limpieza)
  processed/    datasets finales para modelar
notebooks/      análisis (numerados, ejecutados)
src/            código reutilizable (preprocesamiento, pipeline, modelos)
models/         artefactos entrenados (pipeline + modelo)
app/            aplicación / API (TF1)
reports/        figuras y presentaciones
docs/           enunciado, matriz de herramientas, decisiones
tests/          pruebas básicas
```

## Notebooks
| Notebook | Contenido |
|---|---|
| `01_problema_y_datos.ipynb` | Definición, procedencia, diccionario de variables |
| `02_eda.ipynb` | EDA guiado por preguntas, con interpretación |
| `03_calidad_y_preparacion.ipynb` | Faltantes, duplicados, outliers, reglas lógicas |
| `04_baseline_y_modelos.ipynb` | Split, Pipeline, baseline, ≥2 modelos, métricas |
| `05_experimentacion.ipynb` | (TF1) CV, Optuna/MLflow |
| `06_clustering_pca.ipynb` | (TF1) técnica adicional |
| `07_interpretabilidad_errores.ipynb` | (TF1) SHAP, análisis de errores |

## Ejecución
```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
jupyter lab
```

## Uso de IA generativa
_Declarar brevemente para qué se utilizó._
