# ¿Qué contienen las cuatro bases de datos de EGIT 2024?

Tenemos la **Encuesta de Gasto Interno en Turismo (EGIT) del DANE, correspondiente a 2024**. Combina información sobre las personas, sus hogares y sus viajes: quiénes son, si viajan, cómo lo hacen y cuánto gastan. Fuente: [diccionario del DANE](https://microdatos.dane.gov.co/index.php/catalog/864/data-dictionary).

## Los cuatro trimestres

Las cuatro bases son los **cuatro trimestres de la misma encuesta**. Cada trimestre trae los mismos nueve módulos; por eso encontramos 36 CSV. Según la revisión de los archivos locales:

| Trimestre de 2024 | Registros de personas |
|---|---:|
| Primero | 31.185 |
| Segundo | 30.542 |
| Tercero | 30.740 |
| Cuarto | 29.512 |
| **Total** | **121.979** |

Este total representa observaciones de personas por trimestre. No debemos asumir que son las mismas personas encuestadas cuatro veces.

## Los nueve módulos

| Módulo | ¿Qué información contiene? |
|---|---|
| **Características generales** | Edad, sexo, nacimiento y parentesco con la persona que encabeza el hogar. |
| **Educación** | Asistencia a instituciones educativas y nivel educativo alcanzado. |
| **Fuerza de trabajo** | Situación laboral: ocupación, búsqueda de trabajo e inactividad, entre otras preguntas. |
| **Hogar** | Información del hogar, fuentes de ingresos y tenencia de vivienda recreativa. |
| **Vivienda** | Información sobre la vivienda, ubicación y hogares que contiene. |
| **Vivienda de uso recreativo** | Gastos relacionados con esas viviendas, como servicios y mantenimiento. |
| **Turismo** | Viajes pasando al menos una noche fuera: destino, motivo, transporte, alojamiento, noches y gastos. |
| **Excursionismo** | Viajes en los que se regresa el mismo día: destino, motivo, transporte y gastos. |
| **Complementarias** | Preguntas adicionales sobre viajes dentro del país: último destino, fechas, alojamiento, transporte y motivos para no viajar. |

Las descripciones proceden del [diccionario general](https://microdatos.dane.gov.co/index.php/catalog/864/data-dictionary), las [características personales](https://microdatos.dane.gov.co/index.php/catalog/864/data-dictionary/F4?file_name=Caracteristicas+generales), [turismo](https://microdatos.dane.gov.co/index.php/catalog/864/data-dictionary/F17?file_name=Turismo), [excursionismo](https://microdatos.dane.gov.co/index.php/catalog/864/data-dictionary/F16?file_name=Excursionismo) y [complementarias](https://microdatos.dane.gov.co/index.php/catalog/864/data-dictionary/F14?file_name=Complementarias).

## ¿Qué representa una fila de la base consolidada?

Una fila reúne las respuestas de **una persona en un trimestre**, junto con la información de su hogar y vivienda. Por ejemplo, podría reunir su edad, nivel educativo, situación laboral y respuestas sobre viajes.

Si dos personas pertenecen al mismo hogar, ambas tendrán asociados los datos de ese hogar. Por eso no se deben sumar los ingresos o gastos del hogar sobre todas las personas como si cada fila correspondiera a un hogar diferente.

## ¿Qué tipos de datos tenemos?

- **Cantidades:** edad, noches y montos de gastos.
- **Categorías:** nivel educativo, motivo del viaje, transporte o alojamiento. Aunque aparezcan como números, pueden ser códigos.
- **Fechas:** inicio y finalización de viajes.
- **Identificadores y factores:** sirven para relacionar registros y trabajar con la encuesta; no son características personales equivalentes a edad o gasto.

## ¿Por qué hay tantos vacíos?

No todas las preguntas corresponden a todas las personas. Por ejemplo, si alguien no realizó un viaje, podría no tener respuestas sobre alojamiento. Ese vacío necesita revisar el formulario antes de tratarlo como un dato perdido.

## ¿Qué tenemos para analizar?

Tenemos **el perfil de las personas y sus hogares junto con su comportamiento de viaje**.

El estudiante decide qué aspecto quiere estudiar y qué variables lo representan. Esta explicación describe el contenido de la base; no afirma qué grupos existen ni elige variables, imputaciones o métodos de agrupación.
