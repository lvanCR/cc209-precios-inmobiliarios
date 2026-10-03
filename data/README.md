# Fuente y diccionario de datos

- **Fuente / URL:** King County House Sales, Kaggle — https://www.kaggle.com/datasets/harlfoxem/housesalesprediction
- **Archivo:** `data/raw/kc_house_data.csv` (no se versiona; se descarga con `kagglehub`, ver `notebooks/01_problema_y_datos.ipynb`)
- **Licencia:** por verificar en la página de Kaggle antes de la entrega.
- **Observaciones x variables:** 21 613 x 21
- **Período:** 2014-05-02 a 2015-05-27
- **Variable objetivo:** `price` (USD)
- **Calidad inicial:** 0 valores nulos; 177 filas con `id` repetido (21 436 `id` únicos).
- **Limitaciones conocidas:**
  - un solo condado y un solo año;
  - precio de cierre, no de oferta, sin marca de ventas atípicas;
  - sin variables de entorno (colegios, criminalidad, transporte);
  - ventas repetidas de una misma vivienda;
  - ceros que significan "no aplica" (`yr_renovated`, `sqft_basement`).
- **Justificación de idoneidad:** tiene ubicación (`lat`/`long`, `zipcode`), características físicas y fecha, suficientes para EDA geográfico, tratamiento de asimetría y outliers, modelos de regresión y detección de anomalías.

## Diccionario de variables
| Variable | Tipo | Descripción |
|---|---|---|
| `id` | identificador | Identificador de la vivienda (se repite si se vendió más de una vez) |
| `date` | fecha (texto) | Fecha de la venta, formato `YYYYMMDDT000000` |
| `price` | numérica (USD) | Precio de venta. Variable objetivo |
| `bedrooms` | numérica discreta | Número de dormitorios |
| `bathrooms` | numérica | Número de baños (fraccionario: 0.5 = medio baño) |
| `sqft_living` | numérica (pies²) | Superficie habitable interior |
| `sqft_lot` | numérica (pies²) | Superficie del terreno |
| `floors` | numérica | Número de pisos |
| `waterfront` | binaria | 1 si da al agua, 0 si no |
| `view` | ordinal 0-4 | Calidad de la vista |
| `condition` | ordinal 1-5 | Estado de conservación |
| `grade` | ordinal 1-13 | Calidad de construcción y diseño según el sistema del condado |
| `sqft_above` | numérica (pies²) | Superficie sobre el nivel del suelo |
| `sqft_basement` | numérica (pies²) | Superficie del sótano (0 = sin sótano) |
| `yr_built` | año | Año de construcción |
| `yr_renovated` | año | Año de renovación (0 = nunca renovada) |
| `zipcode` | categórica | Código postal. Es una categoría, no una cantidad |
| `lat`, `long` | numérica | Coordenadas |
| `sqft_living15` | numérica (pies²) | Superficie habitable promedio de las 15 viviendas vecinas más cercanas |
| `sqft_lot15` | numérica (pies²) | Superficie de terreno promedio de las 15 viviendas vecinas más cercanas |
