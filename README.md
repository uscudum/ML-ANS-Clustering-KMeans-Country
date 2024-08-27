# Análisis de Clusters de Países en Google Colab

Este proyecto utiliza técnicas de `Machine Learning` para realizar una clusterización de datos de países utilizando el algoritmo `K-Means`. El objetivo es agrupar los países en diferentes clusters según características socioeconómicas. El análisis se realizó en Google Colab.

## Requisitos

- Una cuenta de Google.
- Acceso a Google Colab.
- Archivo `Country-data.csv` almacenado en Google Drive.

## Uso

1. **Acceso a Google Colab**: Abre el [Google Colab](https://colab.research.google.com/) en tu navegador.
2. **Subida del archivo CSV**: Asegúrate de que el archivo `Country-data.csv` esté almacenado en tu Google Drive.
3. **Configuración del entorno**: Ejecuta el siguiente código en una celda de Google Colab para montar tu Google Drive y acceder al archivo CSV.

   ```python
   from google.colab import drive
   drive.mount('/content/drive')

   import pandas as pd
   from sklearn.preprocessing import StandardScaler
   from sklearn.cluster import KMeans

   # Cargamos el DataFrame desde Google Drive
   df = pd.read_csv('/content/drive/My Drive/Country-data.csv')
   print(df.head())

   # En nuestras variables independientes almacenamos todas las columnas
   # excepto las localidades, ya que sus ítems no son numéricos
   X = df.drop(columns=['country'])
   print(X.head())

   # Escalamos los datos
   scaler = StandardScaler()
   X_std = scaler.fit_transform(X)

   # Creamos el modelo
   kmeans = KMeans(n_clusters=3)
   kmeans.fit(X_std)

   # Añadimos al DataFrame una nueva columna, con los resultados
   # de la clusterización
   df['cluster'] = kmeans.labels_

   # Visualizamos y analizamos coincidencias en las primeras 60 filas
   print(df[['country','cluster']].head(60))

   # Filtro las filas para observar en qué cluster se ubicó Uruguay
   print(df[df['country']=='Uruguay'])

   # Filtro solamente las columnas que me interesan de la fila de Uruguay
   print(df[df['country']=='Uruguay'][['country','cluster']])

4. **Ejecución del código**: Ejecuta cada celda del código en Google Colab para realizar la clusterización y visualizar los resultados.

## Explicación
1. **Carga de Datos:** Se carga un DataFrame a partir de un archivo CSV que contiene información sobre diferentes países, almacenado en Google Drive.
2. **Preprocesamiento:** Se eliminan las columnas no numéricas y se escalan los datos para su normalización.
3. **Clusterización:** Se aplica el algoritmo K-Means para agrupar los países en 3 clusters diferentes.
4. **Resultados:** Se añaden los resultados de la clusterización como una nueva columna en el DataFrame y se visualizan las primeras 60 filas. También se filtra específicamente la información sobre Uruguay para ver en qué cluster fue clasificado.

## Resultados Esperados
El script imprimirá las primeras filas del DataFrame original, el DataFrame procesado (sin la columna de país), y mostrará los resultados de la clusterización, incluyendo en qué cluster fue clasificado Uruguay.

## Contribuciones
Las contribuciones son bienvenidas. Por favor, crea una rama nueva para tus cambios y envía un pull request.
