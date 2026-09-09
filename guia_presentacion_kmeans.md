# Presentación: K-Means Clustering

Guía de contenido para armar el notebook. El formato es el de los notebooks del profesor
(01, 02 y 03): celdas markdown explicando antes de cada bloque de código, gráficas en loop
cuando aplique, y tablas comparativas al final.

**Ojo:** el profesor va a hacer un quiz con lo que expliquemos, así que lo que quede flojo
en la presentación es lo que va a estar flojo en el quiz.

---

## Bibliografía

El link que nos dio el profesor (Real Python, *K-Means Clustering in Python: A Practical
Guide*) sirve como base, pero tiene tres huecos que hay que llenar nosotros:

1. **No trae las fórmulas.** Explica el SSE en palabras pero no lo escribe.
2. **No enseña a interpretar los clusters.** Se queda en "aquí están los grupos".
3. **El ejemplo real no es presentable** (expresión génica, 20.531 variables).

Además está en inglés, es nivel "advanced", y el código es de 2020: hay al menos una línea
de seaborn con sintaxis vieja que ya no corre (usa argumentos posicionales donde ahora se
exige `x=` y `y=`). No copiar y pegar sin probar.

Para las fórmulas y los parámetros exactos, complementar con la documentación de
scikit-learn.

---

## Estructura del notebook

### Sección 1 — Ubicar el tema

Marcar la diferencia con lo que ya vimos en clase: en los notebooks anteriores había una
variable objetivo y el modelo aprendía a predecirla. Aquí **no hay respuesta correcta**;
el algoritmo busca estructura por sí solo. Eso es aprendizaje no supervisado.

Mencionar los dos usos del clustering:
- **Descubrir conocimiento**: encontrar grupos que nadie había definido.
- **Paso intermedio**: segmentar para después hacer algo con cada segmento.

### Sección 2 — Las tres familias de clustering

Tabla comparativa:

| Familia | Cómo agrupa | ¿Hay que decirle k? | Fuerte en | Débil en |
|---|---|---|---|---|
| **Particional** (k-means, k-medoids) | Divide en k grupos sin traslape | Sí | Escalabilidad, simplicidad | Formas no esféricas, densidades distintas |
| **Jerárquico** (aglomerativo, divisivo) | Construye un árbol (dendrograma) | Al cortar el árbol | Muestra relaciones finas; es determinista | Costoso; sensible a ruido y outliers |
| **Densidad** (DBSCAN, OPTICS) | Zonas densas separadas por zonas vacías | **No** | Formas arbitrarias, resiste outliers | Alta dimensión, densidades variables |

Dos contrastes que probablemente entren en el quiz:
- k-means es **no determinista**; el jerárquico **sí** lo es.
- DBSCAN es el único de los tres que **no** exige definir el número de grupos de antemano.

### Sección 3 — Cómo funciona k-means

El corazón de la presentación. Los cuatro pasos:

1. Elegir k y colocar k centroides iniciales.
2. **Paso de expectativa**: asignar cada punto al centroide más cercano.
3. **Paso de maximización**: recalcular cada centroide como la media de sus puntos.
4. Repetir 2 y 3 hasta que los centroides dejen de moverse (convergencia).

Ese ciclo se llama *expectation-maximization*.

La función objetivo es el **SSE** (suma de distancias euclidianas al cuadrado de cada punto
a su centroide). k-means busca minimizarlo:

$$SSE = \sum_{i=1}^{k} \sum_{x \in C_i} \|x - \mu_i\|^2$$

Escribirla en el notebook aunque el artículo no la traiga.

**Lo que más se presta para pregunta de quiz:** la inicialización es aleatoria, por eso el
algoritmo no es determinista. De ahí salen dos parámetros que hay que explicar bien:

- `n_init`: cuántas veces corre el algoritmo completo desde cero; se queda con la corrida
  de menor SSE.
- `init="k-means++"` vs `"random"`: k-means++ separa los centroides iniciales a propósito,
  converge más rápido y con mejores resultados.

Otros parámetros a nombrar: `n_clusters` (el más importante), `max_iter`, `random_state`.

Atributos que quedan después de entrenar: `.labels_`, `.cluster_centers_`, `.inertia_`,
`.n_iter_`.

Vale la pena incluir un ejemplo sintético sencillo aquí, antes del caso real, para que se
vea el algoritmo funcionando con datos que se puedan graficar en 2D.

### Sección 4 — Por qué hay que escalar

No puede faltar. k-means agrupa por **distancia euclidiana**, así que una variable con
rango grande domina el cálculo y las demás casi no cuentan.

Conexión con lo que ya vimos: es el mismo `StandardScaler` que usamos antes — media 0,
desviación 1.

### Sección 5 — Cómo elegir k

Dos métodos, y hay que explicar por qué se usan **juntos**, no uno u otro.

**Método del codo.** Se corre k-means para k = 1, 2, 3... y se grafica el SSE. La idea
clave: el SSE **siempre baja** al aumentar k (con k = número de puntos, SSE = 0), así que
no se elige el mínimo, sino el punto donde la curva se dobla — el equilibrio entre error y
complejidad.

**Coeficiente de silueta.** Para cada punto compara qué tan cerca está de los de su grupo
(cohesión) contra qué tan lejos está del grupo vecino más cercano (separación). Va de −1 a 1:

- cerca de 1 → bien asignado
- cerca de 0 → está en la frontera entre dos grupos
- negativo → estaría mejor en otro cluster

Detalle que puede entrar en quiz: **empieza en k=2**; con un solo cluster no está definido.

Extra que vale mucho y no está en el artículo: además del promedio existe el **gráfico de
silueta por muestra**, donde cada cluster se ve como un "cuchillo". Si uno sale mucho más
delgado o con valores negativos, ese grupo está mal formado — algo que el promedio esconde.

Cerrar con lo que dice el artículo: la decisión final combina las métricas **con
conocimiento del dominio**. No es una fórmula automática.

### Sección 6 — Interpretar los clusters

Esta parte la tenemos que aportar nosotros; el artículo no la trae. Es donde el clustering
pasa de ser un número a ser un resultado.

La idea: una vez asignados los grupos, se calcula el **perfil** de cada uno (la media de
cada variable por cluster) y se compara contra la media global. De ahí sale la narrativa de
qué representa cada grupo.

Dos recursos que funcionan bien frente a una clase:

- **Heatmap de los perfiles en unidades estandarizadas** (rojo = por encima del promedio,
  azul = por debajo). Se lee de un vistazo.
- **Mostrar los casos más cercanos a cada centroide**: los ejemplos más representativos de
  cada grupo. Que la audiencia reconozca el patrón sola es lo que hace que se entienda.

### Sección 7 — Limitaciones

El profesor casi seguro pregunta por esto. El artículo trae el ejemplo perfecto: datos en
forma de dos medias lunas, donde k-means falla (parte el espacio en regiones esféricas) y
DBSCAN acierta.

Lo interesante y contraintuitivo: **la silueta le da mejor puntaje a k-means (0.5) que a
DBSCAN (0.38)**, aunque visualmente DBSCAN es el que agrupa bien. El ARI, que sí usa las
etiquetas verdaderas, da 0.47 vs 1.0 y corrige el diagnóstico.

Moraleja para el quiz: las métricas internas como la silueta **pueden ser engañosas**; hay
que mirar también los datos.

Limitaciones a listar:

- Supone clusters esféricos y de tamaño similar
- Sensible a outliers (el centroide es una media, y la media se jala fácil)
- Hay que definir k de antemano
- No determinista
- Solo funciona con variables numéricas
- Sufre en alta dimensionalidad (por eso a veces se aplica PCA antes)

### Sección 8 — PCA y pipelines *(opcional)*

Última sección del artículo. PCA reduce dimensiones combinando variables en "componentes".
Se usa para dos cosas: poder **visualizar** los clusters en 2D, y mitigar la maldición de la
dimensionalidad cuando hay muchas variables.

El `Pipeline` de sklearn encadena escalado + PCA + k-means en un solo objeto, para que los
pasos se apliquen siempre en el mismo orden.

**Es la sección más prescindible** si andamos cortos de tiempo.

---

## Prioridades

Si el quiz sale de lo que nosotros expliquemos, esto es lo que no puede faltar:

1. Supervisado vs no supervisado
2. Los 4 pasos del algoritmo y el SSE
3. Por qué hay que escalar
4. Codo y silueta: qué son, cómo se leen, por qué la silueta empieza en 2
5. Que k-means es no determinista, y para qué sirven `n_init` y `k-means++`
6. Cuándo k-means falla (el ejemplo de las lunas)

Los puntos **2, 3, 4 y 6** son los más probables en un quiz.

---

## Propuesta de división

Cuatro bloques de carga parecida. Ajustar según cuántos seamos.

| Bloque | Secciones | Qué implica |
|---|---|---|
| **A — Teoría y contexto** | 1, 2 | Redacción, tabla comparativa. Poco código. |
| **B — El algoritmo** | 3, 4 | Fórmula del SSE, parámetros, ejemplo sintético en 2D. |
| **C — Elección de k** | 5 | Codo, silueta, gráfico de silueta por muestra. La parte más técnica. |
| **D — Resultados y límites** | 6, 7, (8) | Perfilado de clusters, ejemplo de las lunas, conclusiones. |

**Trabajo compartido (no asignar a una sola persona):**

- Definir el dataset y hacer el EDA inicial — todo lo demás depende de eso, así que va
  primero y de común acuerdo.
- Unificar el notebook al final: que los nombres de variables coincidan entre secciones y
  que corra de arriba abajo sin errores.
- Ensayar la exposición completa una vez, para calcular tiempos.

**Antes de repartirnos:** que cada uno verifique que le instalan las librerías. Si a alguien
le falla el entorno, mejor saberlo ahora y no el día antes.
