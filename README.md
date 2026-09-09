# EGIT 2024 — preparación y exposición de k-means

Proyecto académico con los cuatro trimestres de la Encuesta de Gasto Interno en Turismo del DANE. El notebook principal es [K-means.ipynb](K-means.ipynb).

## Estado actual

Se consolidaron 36 CSV en 121.979 filas y 278 columnas, con una fila por persona y trimestre. Los cruces conservan los módulos personales, hogar, vivienda y los registros de vivienda recreativa. Se comprobaron llaves, conservación de filas y recuperación de los valores de los 36 archivos desde la base consolidada.

El notebook contiene carga, exploración inicial, calidad, construcción de la base y celdas configurables para selección, corrección, imputación y revisión de atípicos. Las decisiones de limpieza siguen pendientes del estudiante. Aún no se ejecutan escalado, reducción de dimensionalidad ni k-means.

## Objetivo propuesto para la exposición — pendiente de elegir

Explorar perfiles de comportamiento turístico entre las personas encuestadas que realizaron turismo interno en 2024, agrupándolas mediante k-means según cantidades relacionadas con sus viajes y gastos que se seleccionarán después de revisar el diccionario y la calidad de los datos.

Es una propuesta de enfoque, no un resultado ni un filtro aplicado. La selección exacta de población, variables, escala y número de grupos todavía no está definida. Los grupos deberán describirse después de ajustar el algoritmo; no se presuponen perfiles ni nombres.

K-means es un modelo de aprendizaje no supervisado: aprende centros de grupos y asigna observaciones según su proximidad. La exposición puede mostrar una ilustración de asignación y actualización de centros, el criterio para elegir k, una proyección de los grupos y una comparación de sus características en unidades originales. PCA es una posibilidad de reducción y visualización, no un requisito automático.

Estos perfiles describirían inicialmente la muestra analizada. Generalizarlos a la población requiere considerar el diseño de la encuesta y sus factores de expansión. Los datos de hogar repetidos en personas no deben sumarse como hogares independientes.

## Ejecutar

Con Python 3.11, desde esta carpeta:

```bash
python3.11 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
```

Abrir el notebook en un IDE compatible con Jupyter, seleccionar `.venv/bin/python` como intérprete y ejecutar las celdas en orden desde la raíz del proyecto. Los CSV originales necesarios están incluidos en `Bases de datos/`.

La ejecución genera `Resultados/egit_2024_consolidada.csv.gz` y `Resultados/egit_2024_preparacion_actual.csv.gz`. Este último representa las reglas configuradas; no certifica una matriz terminada para clustering. Ver [estado de preparación](Resultados/LEEME.md).

## Qué se versiona

- Notebook, 36 CSV utilizados, reportes de control, documentación y dependencias.
- Se ignoran el catálogo local `funciones_notebooks_profesor.txt`, los ZIP, TXT, SAV y SAS7BDAT de las bases, el entorno virtual, archivos del IDE y bases comprimidas regenerables.
- Ignorar un archivo no lo elimina del equipo. No se ha borrado material original.

Las funciones de preparación retoman el catálogo del profesor y el parcial de referencia; el código necesario está dentro del notebook y no necesita esos materiales externos para ejecutarse. El desarrollo de k-means y sus gráficas queda para la siguiente etapa.

## Referencias

- [DANE: diccionario EGIT 2024](https://microdatos.dane.gov.co/index.php/catalog/864/data-dictionary).
- [scikit-learn: funcionamiento de k-means](https://scikit-learn.org/stable/modules/clustering.html#k-means).
- [Real Python: tutorial solicitado](https://realpython.com/k-means-clustering-python/).
