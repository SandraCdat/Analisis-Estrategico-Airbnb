# "Analisis-Estrategico-Airbnb"
El proyecto se centra en el análisis de datos de disponibilidad de habitaciones en Airbnb, aprovechando herramientas de Business Intelligence (BI) para descubrir patrones y oportunidades. En un contexto donde la economía compartida y la hospitalidad se entrelazan, maximizar la eficiencia y rentabilidad es crucial tanto para los anfitriones como para la plataforma.

![airbnb](https://github.com/user-attachments/assets/654c240f-d436-4912-a994-9e52e6d62b26)

# Menú
- [Objetivo](Objetivo)
- [Herramientas y Tecnologías](HerramientasyTecnologías)
- [Procesamiento y análisis](Procesamientoyanálisis)
- [Resultados y Conclusiones](ResultadosyConclusiones)
- [Enlaces de interés](Enlacesdeinterés)
## Objetivo
Identificar los factores clave que influyen en la ocupación de las habitaciones, y a partir de estos datos, generar recomendaciones para mejorar la rentabilidad de los anfitriones.
## Herramientas y Tecnologías:

### Herramientas y/o plataformas
Google BigQuery
Power BI
Chat GPT

### Lenguajes
SQL en BigQuery
Fórmulas DAX en PowerBI

## Procesamiento y análisis
- ### Conectar/importar datos a herramientas
Las tablas reviews y rooms se cargaron corectamente.
La tabla hosts no se pudo subir correctamente porque tenía valores en la columna que deben ser número pero están algunas filas en texto. Se tomó la decisión de renombrar las columnas.

[Ver Consultas Big Query](Consulta.md)

- ### Identificar y manejar valores nulos
  Se utilizó una fórmula en cada tabla para identificar las filas que contienen cualquier valores nulos, valores numéricos y texto.
 [Ver Consultas Big Query](Consulta.md)

Tabla host_final

![image](https://github.com/user-attachments/assets/46259aef-beaf-4dd0-9687-8b6215951a79)

Tabla reviews

![image](https://github.com/user-attachments/assets/571e905c-661b-43c0-a39c-6a793899ad41)

Tabla rooms

![image](https://github.com/user-attachments/assets/cc58d7f7-236c-43cf-985e-eacafda23242)


- ### Identificar valores duplicados  
  Se utilizó una fórmula en las tres tablas para identificar cuántos valores duplicados existe. De esta consulta solo en la tabla host_final se encontraron duplicados.
  [Ver Consultas Big Query](Consulta.md)
  
  ![image](https://github.com/user-attachments/assets/84f3d234-4761-4ab9-be9f-10b742bb3832)

- ### Identificar y manejar datos discrepantes en variables categóricas  
  Se utilizó una fórmula en cada tabla para manejar datos discrepantes en variables categóricas. En la tabla host_final y en la tabla rooms se encontraron datos discrepantes. Vale recalcar que los nombres que no estaban en español no se los eliminó.
  [Ver Consultas Big Query](Consulta.md)

- ### Identificar y manejar datos discrepantes en variables numéricas  
  Se utilizó una fórmula en cada tabla para manejar datos discrepantes en variables numéricas. En la tabla reviews se cambío a la columna last_reviews a tipo la fecha para llenar con la media todas filas que estaban en nulo.
  [Ver Consultas Big Query](Consulta.md)

- ### Crear nuevas variables
  Se crearon nuevas variables para el análisis, como ganancias por habitación y número de reservas por año directamente me POWER BI.
  
  ```Ganancias por habitación = reviews_clean[price] * reviews_clean[availability_365]```
  
  ``` Numero_Reservas_Año = DIVIDE(365, rooms[minimum_nights]) ```

- ### Agrupar datos según variables categóricas
  Las variables categóricas se agruparon a través de tablas matrix en Power BI.

- ### Visualizar las variables categóricas
  Para visualizar los datos de las variables categóricas que se agruparon se utilizó gráfico de barras en Power BI.
  
- ### Representar datos a través de tabla resumen o scorecards
  La base de datos contiene la información relevante para realizar el analísis, junto con un dashboard para visualizar los resultados.

- ### Representar datos a través de gráficos simples
  Los gráficos utilizados para el proyecto fueron los gráficos de barra y gráficos circulares. debido a que son los más útiles al momento de presentar los resultados del análisis. 

## Resultados y Conclusiones
El análisis revela que Manhattan y Brooklyn son las zonas más rentables en Airbnb, con un enfoque en propiedades completas que generan mayores ingresos. La experiencia de los anfitriones también influye en el éxito, ya que más propiedades suelen traducirse en más reseñas y mayores ingresos. Se recomienda que los nuevos anfitriones se centren en estas áreas, ofrezcan casas completas, flexibilicen las políticas de reserva para estancias cortas y monitoreen las tendencias de ocupación y precios para maximizar la rentabilidad.

## Enlaces de interés:
[Dashboard Power BI](https://drive.google.com/file/d/1e44p6GRHkyoiD3R5H2_udV73olTpoUqd/view?usp=sharing)
