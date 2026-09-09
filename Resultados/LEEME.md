# EGIT 2024: estado de preparación

El notebook `../K-means.ipynb` reproduce la carga y los controles. Seleccionar el intérprete `../.venv/bin/python` en Jupyter o en el IDE y ejecutar desde la carpeta `K_means`.

- Completado: carga de 36 CSV, verificación de llaves, unión de módulos, concatenación de los cuatro trimestres y diagnóstico de calidad.
- Unidad provisional: una persona por trimestre. Los datos de hogar y vivienda se repiten en las personas correspondientes; no sumar esas columnas como si cada fila fuera un hogar distinto.
- `egit_2024_consolidada.csv.gz`: base completa, con columnas prefijadas por módulo. CSV separado por comas, comprimido con gzip. Al cargar, conservar los códigos con `dtype="string", keep_default_na=False, na_values=[""]`.
- `egit_2024_preparacion_actual.csv.gz`: estado de las reglas de limpieza configuradas. Las listas están inicialmente vacías; no es una matriz terminada para clustering.
- Los CSV de control contienen inventario, calidad, esquemas, llaves, cruces y procedencia de columnas.
- Pendiente del estudiante: población, significado y selección de variables, reglas de aplicabilidad, imputación, exclusiones e interpretación. El notebook incorpora celdas configurables para estas decisiones.
- Pendiente después: codificación y escala, decidir reducción de dimensionalidad y desarrollar k-means. No se ejecutaron en esta etapa.

Los CSV originales permanecen intactos. Ejecutar el notebook actualiza los resultados derivados de esta carpeta.
