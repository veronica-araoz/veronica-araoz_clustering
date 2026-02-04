Clustering de notas periodísticas con embeddings + UMAP + K-Means

Este repositorio contiene el código desarrollado en el marco de mi tesis doctoral y beca doctoral de CONICET, con el objetivo de realizar una aproximación exploratoria al corpus mediante técnicas de clustering no supervisado aplicadas a textos periodísticos. El propósito principal es identificar agrupamientos temáticos/discursivos y explorar permanencias o variaciones en el conjunto de datos.

El corpus está compuesto por notas publicadas en tres portales de noticias online de Argentina (La Voz de Córdoba, Diario Uno de Mendoza y La Capital de Rosario) durante el período 2015–2020, recolectadas por su vinculación con las movilizaciones feministas. Esto responde al objetivo principal de la investigación: comprender la producción discursiva en torno a movilizaciones feministas por parte de la prensa de alcance local y regional en Argentina durante 2015–2020.

Objetivos del notebook

El pipeline implementado permite:

Cargar y preparar un dataset de notas periodísticas con campos textuales.

Unificar texto (Titular + Bajada + Cuerpo_texto) en una única variable para análisis.

Generar embeddings semánticos mediante modelos preentrenados (SentenceTransformers).

Reducir dimensionalidad con UMAP.

Estimar un k óptimo para clustering (método del codo + silueta).

Aplicar K-Means para asignar clústeres al corpus.

Explorar resultados con:

visualización 2D (UMAP)

nubes de palabras por clúster

palabras clave y palabras distintivas por clúster

Dataset (estructura esperada)

El dataset utilizado no se incluye en este repositorio. Para ejecutar el notebook, se espera un archivo tabular con las siguientes columnas:

ID

Titular

Bajada

Cuerpo_texto

medio (opcional, si se desea segmentar por portal)

anio (opcional, si se desea segmentar por período)

En el preprocesamiento, las columnas Titular, Bajada y Cuerpo_texto se concatenan en una variable adicional:

texto_completo

Metodología (resumen técnico)
1) Embeddings (SentenceTransformers)

Se utiliza un modelo preentrenado multilingüe para representar semánticamente cada nota periodística:

distiluse-base-multilingual-cased-v1

El objetivo es obtener una matriz de embeddings que capture similitudes semánticas entre textos.

2) Reducción de dimensionalidad (UMAP)

Dado que los embeddings tienen alta dimensionalidad, se aplica UMAP para:

reducir el espacio (por ejemplo a 5 dimensiones) y facilitar el clustering

generar una reducción adicional a 2 dimensiones para visualización

3) Clustering (K-Means)

Se aplica K-Means sobre los embeddings reducidos.

Para seleccionar el número de clústeres k, se utilizan dos criterios complementarios:

Método de la silueta (cohesión/separación entre clústeres)

Método del codo (inercia y punto de inflexión)

Nota metodológica sobre la interpretación de k

La silueta mide qué tan bien separados y cohesionados están los clústeres:

Valores cercanos a 1 → clústeres bien definidos y separados

Valores cercanos a 0 → clústeres superpuestos o poco claros

Valores negativos → mala asignación de clústeres

La inercia mide la suma de distancias al centroide dentro de cada clúster. Se busca el “codo”, donde agregar más clústeres ya no reduce significativamente la inercia.

En este caso, los resultados sugieren que 2–3 clústeres podrían ofrecer un balance razonable entre simplicidad e interpretabilidad, aunque la decisión final depende del objetivo analítico.

Outputs generados

El notebook produce:

una columna cluster_label con la asignación de clúster por nota

visualización UMAP en 2D del corpus coloreada por clúster

nubes de palabras por clúster

tablas de:

palabras clave por clúster (Top N más frecuentes)

palabras distintivas por clúster (términos exclusivos por agrupamiento)

exportación opcional del dataset con resultados (por ejemplo a Excel)

Ejecución en Google Colab

El notebook fue diseñado para ejecutarse en Google Colab.
En caso de utilizar Google Drive, se incluye la celda:

from google.colab import drive
drive.mount('/content/drive')


La ruta del archivo debe definirse en el bloque de carga del dataset (ejemplo):

DATASET_PATH = "/content/drive/MyDrive/CLUSTERING/cluster_global.xlsx"
df = pd.read_excel(DATASET_PATH)

Referencias

Este pipeline fue desarrollado tomando como referencia:

Raimondo Anselmino, Natalia; Rostagno, José; Cardoso, Ana Laura (2021). Aplicación de técnicas de clustering para el estudio sociosemiótico sobre géneros periodísticos en fanpages de Clarín y La Nación.

Alomar, Francisco J. (2025). pasantia_TUIA_CIM_Francisco_J._Alomar [Repositorio de código]. GitHub:
https://github.com/Fran251184/pasantia_TUIA_CIM_Francisco_J._Alomar

Recolección de datos (scraping)

Las notas periodísticas que componen el dataset fueron recolectadas mediante técnicas de web scraping, utilizando como referencia herramientas de acceso libre desarrolladas para la extracción automatizada de artículos de prensa en Argentina:

Basel, V. (2024). Webscraping diarios arg (Version 0.1) [Publicación en GitLab].
https://gitlab.com/valentinbasel/webscraping-diarios-arg

Si querés, también te armo una versión más corta para el “About” del repo (una o dos líneas) y te dejo un requirements.txt listo para subir.

quise copiar y pegar todo esto que me pasaste pero no esta adaptado al lenguaje de github entonces no me aparece el formato con titulos, con punteo, etc

Perfecto, eso pasa porque GitHub formatea con Markdown, y si lo pegás sin respetar algunos detalles (saltos de línea, espacios, etc.) queda como texto plano.

Acá te lo dejo 100% en Markdown para GitHub, listo para copiar y pegar tal cual en README.md 👇

Clustering de notas periodísticas con embeddings + UMAP + K-Means

Este repositorio contiene el código desarrollado en el marco de mi tesis doctoral y beca doctoral de CONICET, con el objetivo de realizar una aproximación exploratoria al corpus mediante técnicas de clustering no supervisado aplicadas a textos periodísticos. El propósito principal es identificar agrupamientos temáticos/discursivos y explorar permanencias o variaciones en el conjunto de datos.

El corpus está compuesto por notas publicadas en tres portales de noticias online de Argentina (La Voz de Córdoba, Diario Uno de Mendoza y La Capital de Rosario) durante el período 2015–2020, recolectadas por su vinculación con las movilizaciones feministas. Esto responde al objetivo principal de la investigación: comprender la producción discursiva en torno a movilizaciones feministas por parte de la prensa de alcance local y regional en Argentina durante 2015–2020.

Objetivos del notebook

El pipeline implementado permite:

Cargar y preparar un dataset de notas periodísticas con campos textuales.

Unificar texto (Titular + Bajada + Cuerpo_texto) en una única variable para análisis.

Generar embeddings semánticos mediante modelos preentrenados (SentenceTransformers).

Reducir dimensionalidad con UMAP.

Estimar un k óptimo para clustering (método del codo + silueta).

Aplicar K-Means para asignar clústeres al corpus.

Explorar resultados con:

visualización 2D (UMAP)

nubes de palabras por clúster

palabras clave y palabras distintivas por clúster

Dataset (estructura esperada)

El dataset utilizado no se incluye en este repositorio. Para ejecutar el notebook, se espera un archivo tabular con las siguientes columnas:

ID

Titular

Bajada

Cuerpo_texto

medio (opcional, si se desea segmentar por portal)

anio (opcional, si se desea segmentar por período)

En el preprocesamiento, las columnas Titular, Bajada y Cuerpo_texto se concatenan en una variable adicional:

texto_completo

Metodología (resumen técnico)
1) Embeddings (SentenceTransformers)

Se utiliza un modelo preentrenado multilingüe para representar semánticamente cada nota periodística:

distiluse-base-multilingual-cased-v1

El objetivo es obtener una matriz de embeddings que capture similitudes semánticas entre textos.

2) Reducción de dimensionalidad (UMAP)

Dado que los embeddings tienen alta dimensionalidad, se aplica UMAP para:

reducir el espacio (por ejemplo a 5 dimensiones) y facilitar el clustering

generar una reducción adicional a 2 dimensiones para visualización

3) Clustering (K-Means)

Se aplica K-Means sobre los embeddings reducidos.

Para seleccionar el número de clústeres k, se utilizan dos criterios complementarios:

Método de la silueta (cohesión/separación entre clústeres)

Método del codo (inercia y punto de inflexión)

Nota metodológica sobre la interpretación de k

La silueta mide qué tan bien separados y cohesionados están los clústeres:

valores cercanos a 1 → clústeres bien definidos y separados

valores cercanos a 0 → clústeres superpuestos o poco claros

valores negativos → mala asignación de clústeres

La inercia mide la suma de distancias al centroide dentro de cada clúster. Se busca el “codo”, donde agregar más clústeres ya no reduce significativamente la inercia.

En este caso, los resultados sugieren que 2–3 clústeres podrían ofrecer un balance razonable entre simplicidad e interpretabilidad, aunque la decisión final depende del objetivo analítico.

Outputs generados

El notebook produce:

una columna cluster_label con la asignación de clúster por nota

visualización UMAP en 2D del corpus coloreada por clúster

nubes de palabras por clúster

tablas de:

palabras clave por clúster (Top N más frecuentes)

palabras distintivas por clúster (términos exclusivos por agrupamiento)

exportación opcional del dataset con resultados (por ejemplo a Excel)

Ejecución en Google Colab

El notebook fue diseñado para ejecutarse en Google Colab.

En caso de utilizar Google Drive, se incluye la celda:

from google.colab import drive
drive.mount('/content/drive')


La ruta del archivo debe definirse en el bloque de carga del dataset (ejemplo):

DATASET_PATH = "/content/drive/MyDrive/CLUSTERING/cluster_global.xlsx"
df = pd.read_excel(DATASET_PATH)

Referencias

Este pipeline fue desarrollado tomando como referencia:

Raimondo Anselmino, Natalia; Rostagno, José; Cardoso, Ana Laura (2021). Aplicación de técnicas de clustering para el estudio sociosemiótico sobre géneros periodísticos en fanpages de Clarín y La Nación.

Alomar, Francisco J. (2025). pasantia_TUIA_CIM_Francisco_J._Alomar [Repositorio de código]. GitHub:
https://github.com/Fran251184/pasantia_TUIA_CIM_Francisco_J._Alomar

Recolección de datos (scraping)

Las notas periodísticas que componen el dataset fueron recolectadas mediante técnicas de web scraping, utilizando como referencia herramientas de acceso libre desarrolladas para la extracción automatizada de artículos de prensa en Argentina:

Basel, V. (2024). Webscraping diarios arg (Version 0.1) [Publicación en GitLab].
https://gitlab.com/valentinbasel/webscraping-diarios-arg
