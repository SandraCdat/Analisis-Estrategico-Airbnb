# CONSULTAS BIG QUERY
## 1. Conectar/importar datos a otras herramientas
```
CREATE TABLE `proyecto5-435216.Proyecto5.hosts_final` AS
SELECT
  SAFE_CAST(string_field_0 AS INT64) AS host_id,
  string_field_1 AS host_name
FROM
  `proyecto5-435216.Proyecto5.hosts`;
```
## 2. Identificar y manejar valores nulos, texto, numérico
### Tabla host_final
```
WITH classification AS (
  SELECT
    host_id,
    host_name,
    -- Clasificación para la columna host_id
    CASE
      WHEN SAFE_CAST(host_id AS INT64) IS NULL AND host_id IS NOT NULL THEN 'Texto (host_id)'
      WHEN host_id IS NULL THEN 'Nulo (host_id)'
      WHEN SAFE_CAST(host_id AS INT64) IS NOT NULL THEN 'Numérico (host_id)'
    END AS host_id_data_type,
    -- Clasificación para la columna host_name
    CASE
      WHEN SAFE_CAST(host_name AS INT64) IS NULL AND host_name IS NOT NULL THEN 'Texto (host_name)'
      WHEN host_name IS NULL THEN 'Nulo (host_name)'
      WHEN SAFE_CAST(host_name AS INT64) IS NOT NULL THEN 'Numérico (host_name)'
    END AS host_name_data_type,
    
  FROM `proyecto5-435216.Proyecto5.hosts_final`
)

-- Contar cuántas veces aparece cada tipo de dato en las columnas
SELECT
  'host_id' AS column_name,
  host_id_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  host_id_data_type

UNION ALL

SELECT
  'host_name' AS column_name,
  host_name_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  host_name_data_type
```
### Tabla reviews
```
#FÓRMULA PARA ENCONTRAR NULOS, TEXTO Y NUMÉRICO
WITH classification AS (
  SELECT
    host_id,
    id,
    number_of_reviews,
    last_review,
    price,
    reviews_per_month,
    calculated_host_listings_count,
    availability_365,
    
    -- Clasificación para la columna host_id
    CASE
      WHEN SAFE_CAST(host_id AS INT64) IS NULL AND host_id IS NOT NULL THEN 'Texto (host_id)'
      WHEN host_id IS NULL THEN 'Nulo (host_id)'
      WHEN SAFE_CAST(host_id AS INT64) IS NOT NULL THEN 'Numérico (host_id)'
    END AS host_id_data_type,

    -- Clasificación para la columna id
    CASE
      WHEN SAFE_CAST(id AS INT64) IS NULL AND id IS NOT NULL THEN 'Texto (id)'
      WHEN id IS NULL THEN 'Nulo (id)'
      WHEN SAFE_CAST(id AS INT64) IS NOT NULL THEN 'Numérico (id)'
    END AS id_data_type,

    -- Clasificación para la columna number_of_reviews
    CASE
      WHEN SAFE_CAST(number_of_reviews AS INT64) IS NULL AND number_of_reviews IS NOT NULL THEN 'Texto (number_of_reviews)'
      WHEN number_of_reviews IS NULL THEN 'Nulo (number_of_reviews)'
      WHEN SAFE_CAST(number_of_reviews AS INT64) IS NOT NULL THEN 'Numérico (number_of_reviews)'
    END AS number_of_reviews_data_type,

    -- Clasificación para la columna last_review
    CASE
      WHEN SAFE_CAST(last_review AS STRING) IS NULL AND last_review IS NOT NULL THEN 'Texto (last_review)'
      WHEN last_review IS NULL THEN 'Nulo (last_review)'
      WHEN SAFE_CAST(last_review AS STRING) IS NOT NULL THEN 'Texto (last_review)' -- Las fechas se tratan como texto
    END AS last_review_data_type,

    -- Clasificación para la columna price
    CASE
      WHEN SAFE_CAST(price AS FLOAT64) IS NULL AND price IS NOT NULL THEN 'Texto (price)'
      WHEN price IS NULL THEN 'Nulo (price)'
      WHEN SAFE_CAST(price AS FLOAT64) IS NOT NULL THEN 'Numérico (price)'
    END AS price_data_type,

    -- Clasificación para la columna reviews_per_month
    CASE
      WHEN SAFE_CAST(reviews_per_month AS FLOAT64) IS NULL AND reviews_per_month IS NOT NULL THEN 'Texto (reviews_per_month)'
      WHEN reviews_per_month IS NULL THEN 'Nulo (reviews_per_month)'
      WHEN SAFE_CAST(reviews_per_month AS FLOAT64) IS NOT NULL THEN 'Numérico (reviews_per_month)'
    END AS reviews_per_month_data_type,

    -- Clasificación para la columna calculated_host_listings_count
    CASE
      WHEN SAFE_CAST(calculated_host_listings_count AS INT64) IS NULL AND calculated_host_listings_count IS NOT NULL THEN 'Texto (calculated_host_listings_count)'
      WHEN calculated_host_listings_count IS NULL THEN 'Nulo (calculated_host_listings_count)'
      WHEN SAFE_CAST(calculated_host_listings_count AS INT64) IS NOT NULL THEN 'Numérico (calculated_host_listings_count)'
    END AS calculated_host_listings_count_data_type,

    -- Clasificación para la columna availability_365
    CASE
      WHEN SAFE_CAST(availability_365 AS INT64) IS NULL AND availability_365 IS NOT NULL THEN 'Texto (availability_365)'
      WHEN availability_365 IS NULL THEN 'Nulo (availability_365)'
      WHEN SAFE_CAST(availability_365 AS INT64) IS NOT NULL THEN 'Numérico (availability_365)'
    END AS availability_365_data_type

  FROM `proyecto5-435216.Proyecto5.reviews`
)

-- Contar cuántas veces aparece cada tipo de dato en las columnas
SELECT
  'host_id' AS column_name,
  host_id_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  host_id_data_type

UNION ALL

SELECT
  'id' AS column_name,
  id_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  id_data_type

UNION ALL

SELECT
  'number_of_reviews' AS column_name,
  number_of_reviews_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  number_of_reviews_data_type

UNION ALL

SELECT
  'last_review' AS column_name,
  last_review_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  last_review_data_type

UNION ALL

SELECT
  'price' AS column_name,
  price_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  price_data_type

UNION ALL

SELECT
  'reviews_per_month' AS column_name,
  reviews_per_month_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  reviews_per_month_data_type

UNION ALL

SELECT
  'calculated_host_listings_count' AS column_name,
  calculated_host_listings_count_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  calculated_host_listings_count_data_type

UNION ALL

SELECT
  'availability_365' AS column_name,
  availability_365_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  availability_365_data_type;
```
### Tabla rooms
```
#FÓRMULA PARA ENCONTRAR NULOS, TEXTO Y NUMÉRICO
WITH classification AS (
  SELECT
    id,
    name,
    neighbourhood,
    latitude,
    longitude,
    room_type,
    minimum_nights,
    
    -- Clasificación para la columna id
    CASE
      WHEN SAFE_CAST(id AS INT64) IS NULL AND id IS NOT NULL THEN 'Texto (id)'
      WHEN id IS NULL THEN 'Nulo (id)'
      WHEN SAFE_CAST(id AS INT64) IS NOT NULL THEN 'Numérico (id)'
    END AS id_data_type,

    -- Clasificación para la columna name
    CASE
      WHEN SAFE_CAST(name AS STRING) IS NULL AND name IS NOT NULL THEN 'Texto (name)'
      WHEN name IS NULL THEN 'Nulo (name)'
      WHEN SAFE_CAST(name AS STRING) IS NOT NULL THEN 'Texto (name)'
    END AS name_data_type,

    -- Clasificación para la columna neighbourhood
    CASE
      WHEN SAFE_CAST(neighbourhood AS STRING) IS NULL AND neighbourhood IS NOT NULL THEN 'Texto (neighbourhood)'
      WHEN neighbourhood IS NULL THEN 'Nulo (neighbourhood)'
      WHEN SAFE_CAST(neighbourhood AS STRING) IS NOT NULL THEN 'Texto (neighbourhood)'
    END AS neighbourhood_data_type,

    -- Clasificación para la columna neighbourhood_group
    CASE
      WHEN SAFE_CAST(neighbourhood_group AS STRING) IS NULL AND neighbourhood_group IS NOT NULL THEN 'Texto (neighbourhood_group)'
      WHEN neighbourhood_group IS NULL THEN 'Nulo (neighbourhood_group)'
      WHEN SAFE_CAST(neighbourhood_group AS STRING) IS NOT NULL THEN 'Texto (neighbourhood_group)'
    END AS neighbourhood_group_data_type,

    -- Clasificación para la columna latitude
    CASE
      WHEN SAFE_CAST(latitude AS FLOAT64) IS NULL AND latitude IS NOT NULL THEN 'Texto (latitude)'
      WHEN latitude IS NULL THEN 'Nulo (latitude)'
      WHEN SAFE_CAST(latitude AS FLOAT64) IS NOT NULL THEN 'Numérico (latitude)'
    END AS latitude_data_type,

    -- Clasificación para la columna longitude
    CASE
      WHEN SAFE_CAST(longitude AS FLOAT64) IS NULL AND longitude IS NOT NULL THEN 'Texto (longitude)'
      WHEN longitude IS NULL THEN 'Nulo (longitude)'
      WHEN SAFE_CAST(longitude AS FLOAT64) IS NOT NULL THEN 'Numérico (longitude)'
    END AS longitude_data_type,

    -- Clasificación para la columna room_type
    CASE
      WHEN SAFE_CAST(room_type AS STRING) IS NULL AND room_type IS NOT NULL THEN 'Texto (room_type)'
      WHEN room_type IS NULL THEN 'Nulo (room_type)'
      WHEN SAFE_CAST(room_type AS STRING) IS NOT NULL THEN 'Texto (room_type)'
    END AS room_type_data_type,

    -- Clasificación para la columna minimum_nights
    CASE
      WHEN SAFE_CAST(minimum_nights AS INT64) IS NULL AND minimum_nights IS NOT NULL THEN 'Texto (minimum_nights)'
      WHEN minimum_nights IS NULL THEN 'Nulo (minimum_nights)'
      WHEN SAFE_CAST(minimum_nights AS INT64) IS NOT NULL THEN 'Numérico (minimum_nights)'
    END AS minimum_nights_data_type

  FROM `proyecto5-435216.Proyecto5.rooms`
)

-- Contar cuántas veces aparece cada tipo de dato en las columnas
SELECT
  'id' AS column_name,
  id_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  id_data_type

UNION ALL

SELECT
  'name' AS column_name,
  name_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  name_data_type

UNION ALL

SELECT
  'neighbourhood' AS column_name,
  neighbourhood_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  neighbourhood_data_type

UNION ALL

SELECT
  'neighbourhood_group' AS column_name,
  neighbourhood_group_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  neighbourhood_group_data_type

UNION ALL

SELECT
  'latitude' AS column_name,
  latitude_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  latitude_data_type

UNION ALL

SELECT
  'longitude' AS column_name,
  longitude_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  longitude_data_type

UNION ALL

SELECT
  'room_type' AS column_name,
  room_type_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  room_type_data_type

UNION ALL

SELECT
  'minimum_nights' AS column_name,
  minimum_nights_data_type AS data_type,
  COUNT(*) AS cantidad
FROM classification
GROUP BY
  minimum_nights_data_type;
```

## 3. Identificar y manejar valores duplicados
### Tabla hosts_final
```
#DUPLICADOS ENTRE LAS DOS COLUMNAS
SELECT 
host_id, host_name,
COUNT (*) AS cantidad
 FROM `proyecto5-435216.Proyecto5.hosts_final`
 GROUP BY host_id, host_name
  HAVING COUNT (*) > 1
```

## 4. Identificar y manejar datos discrepantes en variables categóricas
### Tabla host_final
```
#REEMPLAZAR CARACTERES ESPECIALES, ELIMINAR NULOS Y VALORES NUMÉRICOS
SELECT
  host_name,
  REGEXP_REPLACE(host_name, r'[^a-zA-Z0-9А-яёЁ一-龥々〆〤ぁ-ゖァ-ヺ々〆〤단비빈나소정현선דניאלĀ진]', '') AS host_name_cleaned
FROM
  `proyecto5-435216.Proyecto5.hosts_final`
WHERE
  host_name IS NOT NULL -- Eliminar valores nulos
  AND SAFE_CAST(host_name AS FLOAT64) IS NULL; -- Eliminar valores numéricos
```
### Tabla rooms
```
SELECT
  name,
  REGEXP_REPLACE(name, r'[^a-zA-Z0-9А-яёЁ一-龥々〆〤ぁ-ゖァ-ヺ々〆〤]', '') AS name_cleaned,
  
  neighbourhood,
  REGEXP_REPLACE(neighbourhood, r'[^a-zA-Z0-9А-яёЁ一-龥々〆〤ぁ-ゖァ-ヺ々〆〤]', '') AS neighbourhood_cleaned,
  
  neighbourhood_group,
  REGEXP_REPLACE(neighbourhood_group, r'[^a-zA-Z0-9А-яёЁ一-龥々〆〤ぁ-ゖァ-ヺ々〆〤]', '') AS neighbourhood_group_cleaned,
  
  room_type,
  REGEXP_REPLACE(room_type, r'[^a-zA-Z0-9А-яёЁ一-龥々〆〤ぁ-ゖァ-ヺ々〆〤]', '') AS room_type_cleaned
FROM
  `proyecto5-435216.Proyecto5.rooms`
```

 ## 5. Identificar y manejar datos discrepantes en variables numéricas
### Tabla reviews
```
-- Calcular la mediana de las fechas y rellenar los valores nulos
WITH median_last_review AS (
  SELECT 
    TIMESTAMP_ADD(
      TIMESTAMP('1970-01-01'), 
      INTERVAL CAST(PERCENTILE_CONT(
        TIMESTAMP_DIFF(TIMESTAMP(last_review), TIMESTAMP('1970-01-01'), SECOND), 0.5
      ) OVER () AS INT64) SECOND
    ) AS median_last_review
  FROM `proyecto5-435216.Proyecto5.reviews`
  WHERE SAFE.PARSE_TIMESTAMP('%Y-%m-%d', last_review) IS NOT NULL
  LIMIT 1
)

-- Rellenar los valores nulos con la mediana calculada
SELECT 
  r.*, 
  COALESCE(SAFE.PARSE_TIMESTAMP('%Y-%m-%d', r.last_review), m.median_last_review) AS last_review_1
FROM `proyecto5-435216.Proyecto5.reviews` r
CROSS JOIN median_last_review m;
```

