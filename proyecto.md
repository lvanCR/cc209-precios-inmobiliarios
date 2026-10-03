# PROYECTO INTEGRADOR DE DATA SCIENCE
## Trabajo Parcial (TP1) y Trabajo Final (TF1)

**Universidad:** Universidad Peruana de Ciencias Aplicadas
**Curso:** Data Mining Tools – CC209
**Docente:** Carlos Fernando Montoya Cubas
**Modalidad:** Trabajo grupal
**Integrantes por grupo:** 2 a 4 estudiantes
**TP1:** Semana 7 – 10 % del curso
**TF1:** Semana 15 – 25 % del curso

> **El Trabajo Parcial y el Trabajo Final corresponden al mismo proyecto.**
> El TP1 es el primer corte formal del desarrollo y el TF1 presenta la solución integrada, refinada, evaluada, interpretada y documentada.

---

## 1. Propósito del proyecto

El Proyecto Integrador tiene por finalidad que los estudiantes diseñen, desarrollen y sustenten una solución de Data Science de extremo a extremo, empleando de manera pertinente y fundamentada las herramientas estudiadas durante el curso. La evaluación no se orienta exclusivamente al logro de métricas elevadas, sino a la capacidad del grupo para **seleccionar herramientas adecuadas, justificar su elección, integrarlas de manera coherente y analizar críticamente los resultados obtenidos**.

El proyecto deberá desarrollarse progresivamente a lo largo del semestre, siguiendo el siguiente flujo de trabajo:

**Problema y datos → EDA → Preparación → Modelamiento → Experimentación → Interpretación → Aplicación / despliegue**

> **Principio general de evaluación.** Una gráfica, tabla o métrica carente de interpretación no constituye, por sí sola, un análisis completo. Del mismo modo, toda conclusión deberá estar respaldada por evidencia verificable y reproducible dentro del proyecto.

---

## 2. Modalidad y organización

- El proyecto se desarrollará en **grupos de 2 a 4 estudiantes**.
- Cada grupo deberá proponer un problema concreto y pertinente, así como seleccionar un conjunto de datos adecuado para su estudio.
- Podrán abordarse problemas de clasificación, regresión, segmentación, detección de anomalías u otros enfoques de minería de datos, siempre que el alcance propuesto sea técnica y temporalmente viable durante el semestre.
- El conjunto de datos podrá provenir de repositorios públicos, instituciones, proyectos de investigación o fuentes propias. En todos los casos, su procedencia, licencia o condiciones de uso deberán quedar debidamente documentadas.
- El grupo será responsable de verificar que el problema seleccionado posea suficiente alcance y complejidad para aplicar de manera significativa el flujo de herramientas contemplado en el curso.
- El mismo proyecto deberá mantenerse desde el TP1 hasta el TF1. Cualquier cambio sustantivo de tema posterior a la entrega del TP1 requerirá autorización previa del docente.

---

## 3. Requisitos generales del proyecto

Todo proyecto debe cumplir los siguientes requisitos mínimos:

1. Plantear un problema concreto y una pregunta de análisis o predicción claramente definida.
2. Utilizar un dataset suficientemente rico para realizar EDA, preparación, modelamiento y evaluación.
3. Documentar problemas de calidad y decisiones de preparación.
4. Separar apropiadamente los datos destinados a entrenamiento, validación y prueba, o justificar una estrategia equivalente cuando corresponda.
5. Evitar data leakage durante el preprocesamiento y modelamiento.
6. Construir un flujo reproducible de preparación y modelamiento.
7. Comparar el desempeño con un baseline apropiado.
8. Interpretar los resultados más allá de reportar métricas.
9. Documentar limitaciones, riesgos y aspectos que no pueden concluirse a partir de los datos disponibles.
10. Mantener un repositorio organizado que permita reproducir el trabajo.

---

## 4. Trabajo Parcial (TP1) – Semana 7

### 4.1. Objetivo del TP1

El Trabajo Parcial constituye el **primer avance formal y evaluable del proyecto**. Su propósito es evidenciar que el grupo ha transitado desde una idea inicial hacia un problema de Data Science correctamente delimitado y que dispone de un primer flujo reproducible que incluya análisis exploratorio, preparación de datos y modelos preliminares.

El TP1 **no debe presentarse como un producto concluido**. Se espera que el grupo identifique de manera explícita los aspectos pendientes, las limitaciones detectadas y las actividades que deberán desarrollarse de cara al Trabajo Final.

### 4.2. Alcance obligatorio del TP1

#### 4.2.1. Definición del problema

El grupo debe presentar:

- contexto del problema;
- necesidad o situación que se desea abordar;
- unidad de análisis;
- pregunta principal del proyecto;
- tipo de problema de Data Science;
- utilidad esperada de la solución;
- criterios bajo los cuales se considerará útil el resultado.

No se consideran suficientes formulaciones genéricas como "aplicar Machine Learning al dataset". La pregunta debe ser concreta y permitir evaluar si el análisis o modelo aporta información útil.

#### 4.2.2. Dataset y procedencia

El grupo debe documentar:

- fuente y procedencia;
- número de observaciones y variables;
- período temporal, si corresponde;
- variable objetivo, cuando aplique;
- diccionario de variables relevante;
- licencia o condiciones de uso, cuando corresponda;
- limitaciones conocidas del dataset;
- justificación de por qué el dataset es adecuado para el problema.

#### 4.2.3. Análisis exploratorio de datos (EDA)

El EDA debe responder preguntas relevantes para el problema y no convertirse en una colección automática de gráficos. Debe incluir, cuando corresponda:

- distribuciones relevantes;
- análisis de la variable objetivo;
- relaciones entre variables;
- diferencias entre grupos;
- posibles patrones y anomalías;
- problemas de calidad que condicionen decisiones posteriores.

Cada visualización importante debe ir acompañada de una interpretación. Debe distinguirse entre **lo que los datos muestran** y **lo que el grupo interpreta**.

#### 4.2.4. Calidad y preparación de datos

Se debe documentar el análisis de:

- valores faltantes;
- duplicados;
- tipos de datos;
- categorías inconsistentes;
- outliers o valores extremos;
- reglas lógicas o de negocio;
- transformaciones realizadas.

Las decisiones de preparación deben justificarse. No se considera suficiente indicar únicamente que "se eliminaron outliers" o que "se imputaron faltantes".

#### 4.2.5. Separación de los datos

El grupo debe especificar:

- estrategia de separación train / validation / test, o equivalente;
- proporciones utilizadas;
- razón de dicha elección;
- medidas adoptadas para evitar data leakage.

#### 4.2.6. Flujo reproducible de preprocesamiento

El proyecto debe mostrar una estrategia reproducible mediante herramientas como `Pipeline`, `ColumnTransformer` o una arquitectura equivalente. Debe quedar claro qué transformaciones se aplican a variables numéricas y categóricas y en qué momento se ajustan dichas transformaciones.

#### 4.2.7. Baseline

Todo proyecto debe incluir un baseline que permita responder la pregunta:

> *¿El modelo propuesto mejora realmente frente a una solución trivial o simple?*

Puede emplearse `DummyClassifier`, `DummyRegressor`, una regla simple del dominio u otra referencia justificada.

#### 4.2.8. Modelos preliminares

El grupo debe comparar al menos **dos alternativas de modelamiento** apropiadas para el problema. No se exige que todos los grupos utilicen los mismos algoritmos. La selección debe ser coherente con las características de los datos y la pregunta planteada.

#### 4.2.9. Evaluación preliminar

Las métricas deben seleccionarse de acuerdo con el problema. Debe explicarse por qué son apropiadas. Reportar una métrica sin interpretar su significado en el contexto del proyecto se considera insuficiente.

#### 4.2.10. Estado del proyecto y plan hacia el TF1

El TP1 debe cerrar con:

- principales hallazgos hasta el momento;
- problemas aún no resueltos;
- limitaciones identificadas;
- mejoras que se realizarán;
- actividades previstas para llegar al Trabajo Final.

### 4.3. Entregables del TP1

El grupo debe entregar:

1. **Repositorio del proyecto** con estructura organizada y acceso proporcionado al docente.
2. **Notebook(s) ejecutados** con análisis, código y resultados visibles.
3. **README inicial** con descripción del problema, fuente de datos, instrucciones básicas de ejecución y estructura del proyecto.
4. **Archivo de dependencias** (por ejemplo, `requirements.txt` o equivalente).
5. **Presentación del TP1** en PDF o PPTX.

Se recomienda una estructura similar a:

```
proyecto/
|-- data/
|-- notebooks/
|-- src/
|-- models/
|-- reports/
|-- README.md
'-- requirements.txt
```

### 4.4. Exposición del TP1

- **Tiempo de exposición: 10 minutos por grupo.**
- **Preguntas y retroalimentación: hasta 5 minutos adicionales.**
- Todos los integrantes deben participar de la exposición.
- La presentación debe priorizar problema, evidencia, decisiones y resultados; no se espera una explicación línea por línea del código.
- El grupo debe estar preparado para abrir el notebook o repositorio si se requiere verificar algún resultado.
- El exceso de tiempo podrá ser interrumpido para respetar el cronograma de la sesión.

---

## 5. Trabajo Final (TF1) – Semana 15

### 5.1. Objetivo del TF1

El Trabajo Final corresponde a la versión integrada, refinada y sustentada del proyecto iniciado en el TP1. Deberá evidenciar la mejora de la solución mediante experimentación sistemática, interpretación crítica de resultados, análisis de errores, documentación técnica y una forma funcional de uso o despliegue.

### 5.2. Alcance obligatorio del TF1

#### 5.2.1. Evolución respecto al TP1

El grupo debe incluir una tabla explícita de cambios:

| Elemento | TP1 | TF1 | Motivo del cambio |
|---|---|---|---|
| Preparación | | | |
| Variables | | | |
| Modelo(s) | | | |
| Métricas | | | |
| Otras decisiones | | | |

El objetivo es evidenciar aprendizaje y evolución, no simplemente volver a presentar el TP1.

#### 5.2.2. Experimentación sistemática

El TF1 debe incluir una comparación más rigurosa de alternativas. Según el problema, puede incorporar:

- validación cruzada;
- ajuste de hiperparámetros;
- Optuna u otra herramienta de optimización;
- seguimiento de experimentos mediante MLflow u otra herramienta equivalente.

Debe poder identificarse qué configuración produjo cada resultado relevante.

#### 5.2.3. Técnica o herramienta adicional

El grupo debe incorporar al menos una técnica o herramienta vista en la segunda mitad del curso cuando sea pertinente para el problema, por ejemplo:

- clustering;
- PCA / UMAP;
- técnicas adicionales de visualización o reducción dimensional;
- Deep Learning;
- transfer learning;
- otra técnica debidamente justificada.

No se evaluará positivamente incorporar una técnica únicamente para "cumplir". Debe existir una razón clara para utilizarla.

#### 5.2.4. Interpretabilidad

El grupo debe explicar qué factores influyen en las predicciones o resultados del modelo empleando, según corresponda:

- importancia de variables;
- SHAP;
- interpretaciones locales o globales;
- mecanismos equivalentes apropiados al modelo.

Debe analizarse si las explicaciones son coherentes con el problema y qué precauciones deben considerarse al interpretarlas.

#### 5.2.5. Análisis de errores

Es obligatorio analizar casos donde el modelo falla. Según el tipo de problema, pueden estudiarse:

- falsos positivos y falsos negativos;
- observaciones con mayor error de regresión;
- segmentos con desempeño desigual;
- casos atípicos o difíciles.

El grupo debe proponer hipótesis razonables sobre las causas de dichos errores y distinguir entre evidencia y especulación.

#### 5.2.6. Aplicación o despliegue

El TF1 debe incluir una demostración utilizable de la solución. Puede emplearse, por ejemplo:

- Streamlit para una interfaz interactiva;
- FastAPI para un servicio de inferencia;
- otra alternativa aprobada por el docente.

Docker puede incorporarse cuando resulte pertinente. La solución no necesita infraestructura de producción, pero debe demostrar que el modelo puede ser utilizado fuera del notebook de experimentación.

#### 5.2.7. Arquitectura de la solución

El grupo debe presentar un diagrama sencillo que muestre el flujo entre datos, preprocesamiento, modelo, aplicación y salida. Por ejemplo:

**Usuario → Aplicación → Preprocesamiento → Modelo → Predicción / resultado**

#### 5.2.8. Reproducibilidad y documentación

La versión final debe incluir:

- README completo;
- dependencias;
- instrucciones de ejecución;
- modelo o artefacto necesario para inferencia;
- pipeline de transformación;
- organización clara del repositorio;
- documentación suficiente para que otra persona pueda reproducir la solución.

#### 5.2.9. Conclusiones y limitaciones

El grupo debe responder explícitamente:

- ¿qué puede concluirse a partir del proyecto?;
- ¿qué no puede concluirse?;
- ¿cuáles son las principales limitaciones de los datos y del modelo?;
- ¿qué riesgos tendría utilizar la solución fuera del contexto analizado?;
- ¿qué trabajo futuro sería razonable realizar?

### 5.3. Entregables del TF1

El grupo debe entregar:

1. **Repositorio final** actualizado y organizado.
2. **Notebook(s) y/o scripts** completamente ejecutables.
3. **README final** con instrucciones de reproducción y uso.
4. **Archivo de dependencias** actualizado.
5. **Artefactos del modelo y pipeline** necesarios para la demostración.
6. **Aplicación o API funcional** según la solución elegida.
7. **Presentación final** en PDF o PPTX.
8. **Breve documento de decisiones de herramientas**, que puede formar parte del README o del informe técnico.

### 5.4. Exposición del TF1

- **Tiempo de exposición: 12 minutos por grupo.**
- **Demostración funcional: incluida dentro de los 12 minutos.**
- **Preguntas y retroalimentación: hasta 5 minutos adicionales.**
- Todos los integrantes deben intervenir.
- La presentación debe mostrar la evolución respecto al TP1, la evidencia experimental, interpretación, análisis de errores y funcionamiento de la solución.
- No se recomienda emplear tiempo de exposición para mostrar grandes bloques de código.
- El grupo debe prever un plan de contingencia si la demostración depende de conexión externa.

---

## 6. Matriz de decisiones de herramientas

Como parte del proyecto, cada grupo debe mantener una tabla como la siguiente:

| Necesidad | Herramienta elegida | Alternativa considerada | Justificación |
|---|---|---|---|
| EDA | | | |
| Preparación | | | |
| Modelamiento | | | |
| Experimentación | | | |
| Interpretabilidad | | | |
| Despliegue | | | |

El objetivo no consiste en utilizar el mayor número posible de herramientas, sino en justificar de manera técnica por qué cada herramienta seleccionada resulta pertinente para el problema abordado.

---

## 7. Rúbrica del Trabajo Parcial (TP1)

El TP1 se califica sobre **20 puntos**.

| Criterio | Pts. | Excelente | Logrado | En proceso | Insuficiente |
|---|:---:|---|---|---|---|
| Problema y dataset | 3 | Problema preciso, útil y bien delimitado; dataset pertinente, documentado y con limitaciones reconocidas. | Problema claro y dataset adecuado, con documentación suficiente. | Problema parcialmente delimitado o dataset con justificación débil. | Problema ambiguo o dataset inadecuado / sin sustento. |
| EDA e interpretación | 4 | EDA orientado por preguntas, visualizaciones pertinentes e interpretación crítica y sustentada. | EDA correcto con interpretaciones mayormente adecuadas. | Predomina la descripción o hay gráficos con poca interpretación. | EDA superficial, automático o sin interpretación. |
| Calidad y preparación | 4 | Detecta problemas relevantes, justifica decisiones y reconoce incertidumbre y riesgos. | Detecta y trata los principales problemas con justificación suficiente. | Tratamiento parcialmente mecánico o con decisiones poco justificadas. | Limpieza sin criterio, decisiones incorrectas o ausencia de análisis. |
| Train/validation/test y leakage | 2 | Estrategia correcta, claramente justificada y sin fuga de información. | Estrategia correcta con justificación básica. | Hay omisiones o riesgo menor de leakage. | Separación incorrecta o leakage evidente. |
| Flujo reproducible | 2 | Preprocesamiento organizado y reproducible; transformaciones claramente vinculadas al tipo de variable. | Flujo reproducible funcional con pequeños problemas de organización. | Flujo parcialmente reproducible o disperso. | Operaciones manuales inconsistentes o imposibles de reproducir. |
| Baseline, modelos y evaluación | 3 | Baseline adecuado; compara al menos dos modelos; métricas bien elegidas e interpretadas. | Cumple comparación y métricas con interpretación suficiente. | Comparación limitada o métricas poco justificadas. | No existe comparación significativa o se reportan métricas sin sentido contextual. |
| Análisis crítico y plan hacia TF1 | 2 | Reconoce limitaciones, pendientes y propone un plan concreto y coherente de mejora. | Presenta limitaciones y próximos pasos razonables. | Próximos pasos genéricos o poco conectados con los resultados. | No identifica limitaciones ni plan de continuidad. |
| **Total** | **20** | | | | |

---

## 8. Rúbrica del Trabajo Final (TF1)

El TF1 se califica sobre **20 puntos**.

| Criterio | Pts. | Excelente | Logrado | En proceso | Insuficiente |
|---|:---:|---|---|---|---|
| Evolución respecto al TP1 | 2 | Cambios claramente documentados, motivados por evidencia y retroalimentación. | Se observan mejoras pertinentes y documentadas. | Cambios menores o débilmente justificados. | No existe evolución significativa respecto al TP1. |
| Flujo completo y calidad técnica | 3 | Solución integrada, coherente, reproducible y sin errores conceptuales relevantes. | Flujo funcional y organizado con problemas menores. | Flujo parcial o con inconsistencias. | Solución incompleta o no reproducible. |
| Experimentación y comparación | 3 | Experimentación sistemática, trazable y bien interpretada; comparación justa entre alternativas. | Compara alternativas con metodología suficiente. | Experimentación limitada, poco sistemática o difícil de rastrear. | Selección de modelo sin experimentación sustentada. |
| Evaluación y análisis de errores | 3 | Métricas apropiadas, análisis de errores profundo y conclusiones basadas en casos concretos. | Evaluación correcta y análisis de errores suficiente. | Métricas correctas pero análisis superficial. | Métricas inadecuadas o ausencia de análisis de errores. |
| Interpretabilidad | 2 | Aplica técnica pertinente e interpreta críticamente resultados y limitaciones. | Interpretabilidad correcta con análisis suficiente. | Presenta resultados de interpretabilidad con escasa discusión. | No hay interpretabilidad o se interpreta incorrectamente. |
| Decisiones de herramientas | 2 | Selección de herramientas coherente, comparada con alternativas y claramente justificada. | Herramientas adecuadas con justificación suficiente. | Algunas elecciones poco justificadas. | Uso de herramientas por inercia o sin relación con el problema. |
| Aplicación / despliegue | 3 | Aplicación o API funcional, clara y conectada correctamente con el pipeline/modelo. | Demostración funcional con limitaciones menores. | Prototipo parcial o poco robusto. | No existe demostración funcional. |
| Reproducibilidad y documentación | 2 | Repositorio limpio, README completo, dependencias e instrucciones permiten reproducir el proyecto. | Documentación suficiente para ejecutar el proyecto. | Requiere intervención adicional o faltan instrucciones importantes. | No puede reproducirse a partir de lo entregado. |
| **Total** | **20** | | | | |

---

## 9. Criterios para la exposición oral

La exposición oral constituye parte de la evidencia evaluable del proyecto y podrá incidir en los criterios de la rúbrica vinculados con claridad, justificación y dominio del trabajo. Se espera que:

- los integrantes conozcan el proyecto completo y no únicamente la sección que programaron;
- las afirmaciones estén respaldadas por evidencia;
- se pueda explicar por qué se tomó una decisión técnica;
- se puedan distinguir resultados, interpretación e hipótesis;
- se respondan preguntas sobre limitaciones y posibles fuentes de error;
- la presentación priorice gráficos, diagramas y resultados relevantes por encima de texto o código extenso.

---

## 10. Uso de herramientas de IA generativa

Las herramientas de IA generativa podrán emplearse como apoyo técnico para tareas tales como consulta de sintaxis, explicación de errores, organización del código o exploración de alternativas. Su utilización no sustituye la responsabilidad académica del grupo respecto del análisis, la interpretación y las conclusiones del proyecto.

> **No se considerarán válidas aquellas conclusiones que el grupo no pueda explicar, justificar y defender a partir de la evidencia generada en el proyecto.** Si se utilizaron herramientas de IA generativa de manera significativa en la elaboración de código, documentación o materiales, el grupo deberá declararlo brevemente e indicar para qué se utilizaron.

---

## 11. Consideraciones finales

- Una métrica mayor no implica automáticamente una mejor calificación.
- Un modelo complejo no obtiene ventaja por el solo hecho de ser complejo.
- Se valorará especialmente la capacidad para justificar decisiones, reconocer incertidumbre y documentar limitaciones.
- No se debe forzar el uso de una herramienta o técnica si no aporta al problema.
- La reproducibilidad y la interpretación forman parte del resultado, no son elementos opcionales.

> **Objetivo final del proyecto:** demostrar que el grupo es capaz de diseñar, implementar, documentar y sustentar un flujo de Data Science completo, reproducible y críticamente analizado, empleando de manera pertinente las herramientas del curso.
