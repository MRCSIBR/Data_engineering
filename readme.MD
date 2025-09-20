

# Cheatsheet de Ingeniería de Datos con Python

Guía rápida de Python para ingeniería de datos con consultas SQL esenciales:

## Bibliotecas Esenciales

- **Pandas**: Manipulación y análisis de datos
- **NumPy**: Computación numérica
- **SQLAlchemy**: Toolkit SQL y ORM (Mapeo Objeto-Relacional)
- **PySpark**: Procesamiento distribuido de datos a gran escala
- **Dask**: Computación paralela
- **Apache Airflow**: Orquestación de flujos de trabajo
- **requests**: Interacción con APIs
- **psycopg2**: Conector para PostgreSQL
- **pymongo**: Conector para MongoDB

## Manejo de Datos con Pandas

### Lectura de Datos
```python
import pandas as pd

# Lectura de archivos
df = pd.read_csv('archivo.csv')           # CSV
df = pd.read_json('archivo.json')          # JSON
df = pd.read_excel('archivo.xlsx')        # Excel
df = pd.read_parquet('archivo.parquet')   # Parquet
df = pd.read_sql('SELECT * FROM tabla', con)  # Desde BD
```

### Exploración de Datos
```python
df.head(10)           # Primeras 10 filas
df.tail(5)            # Últimas 5 filas
df.describe()         # Estadísticas descriptivas
df.info()             # Información de columnas y tipos
df.shape              # Dimensiones (filas, columnas)
df.columns            # Nombres de columnas
df.dtypes             # Tipos de datos
df.isnull().sum()     # Valores nulos por columna
```

### Limpieza de Datos
```python
# Manejo de valores nulos
df.fillna(0)                         # Rellenar con 0
df.fillna(df.mean())                 # Rellenar con media
df.dropna()                          # Eliminar filas con nulos
df.dropna(subset=['columna'])        # Eliminar nulos en columna específica

# Eliminación de duplicados
df.drop_duplicates()                 # Eliminar filas duplicadas
df.drop_duplicates(subset=['columna']) # Eliminar duplicados en columna

# Conversión de tipos
df['columna'] = df['columna'].astype('int32')  # Cambiar tipo de dato
```

### Transformación de Datos
```python
# Crear nuevas columnas
df['nueva_columna'] = df['col1'] + df['col2']
df['nueva_columna'] = df['col'].apply(lambda x: x*2)

# Funciones personalizadas
def transformar(valor):
    return valor.upper()

df['columna'] = df['columna'].apply(transformar)

# Mapeo de valores
mapeo = {'A': 1, 'B': 2, 'C': 3}
df['columna_num'] = df['columna'].map(mapeo)
```

### Manipulación Avanzada
```python
# Agrupación y agregación
df.groupby('categoria').agg({
    'ventas': 'sum',
    'clientes': 'count'
})

# Tablas dinámicas
df.pivot_table(
    values='ventas',
    index='region',
    columns='producto',
    aggfunc='sum'
)

# Combinar DataFrames
pd.concat([df1, df2])              # Concatenar
pd.merge(df1, df2, on='id')         # Unir (JOIN)
df1.join(df2, on='id')              # Unir por índice
```

### Visualización de Datos
```python
import matplotlib.pyplot as plt

df.plot(kind='line', x='fecha', y='valor')  # Gráfico de líneas
df.plot(kind='bar', x='categoria', y='total') # Gráfico de barras
df.hist(column='edad')                      # Histograma
df.boxplot(column='salario')                # Diagrama de caja

plt.title('Título del Gráfico')
plt.xlabel('Eje X')
plt.ylabel('Eje Y')
plt.show()
```

## Trabajo con Bases de Datos

### Conexión con SQLAlchemy
```python
from sqlalchemy import create_engine

# PostgreSQL
engine = create_engine('postgresql://user:password@localhost:5432/dbname')

# MySQL
engine = create_engine('mysql+pymysql://user:password@localhost/dbname')

# SQLite
engine = create_engine('sqlite:///database.db')
```

### Operaciones SQL
```python
# Ejecutar consultas
result = engine.execute("SELECT * FROM tabla WHERE condicion")
data = result.fetchall()  # Obtener todos los resultados

# Leer directamente a DataFrame
df = pd.read_sql("SELECT * FROM tabla", engine)

# Escribir DataFrame a BD
df.to_sql('nombre_tabla', engine, if_exists='replace', index=False)

# Transacciones
with engine.begin() as conn:
    conn.execute("UPDATE tabla SET columna = valor WHERE condicion")
```

## Consultas SQL Esenciales

### Operaciones Básicas
```sql
-- Selección
SELECT columna1, columna2 FROM tabla WHERE condicion;

-- Inserción
INSERT INTO tabla (columna1, columna2) VALUES (valor1, valor2);

-- Actualización
UPDATE tabla SET columna1 = valor1 WHERE condicion;

-- Eliminación
DELETE FROM tabla WHERE condicion;
```

### Joins
```sql
-- INNER JOIN
SELECT * FROM tabla1 
INNER JOIN tabla2 ON tabla1.id = tabla2.id;

-- LEFT JOIN
SELECT * FROM tabla1 
LEFT JOIN tabla2 ON tabla1.id = tabla2.id;

-- RIGHT JOIN
SELECT * FROM tabla1 
RIGHT JOIN tabla2 ON tabla1.id = tabla2.id;

-- FULL OUTER JOIN
SELECT * FROM tabla1 
FULL OUTER JOIN tabla2 ON tabla1.id = tabla2.id;
```

### Funciones de Agregación
```sql
SELECT COUNT(*) FROM tabla;                    -- Contar registros
SELECT AVG(columna) FROM tabla;                 -- Promedio
SELECT MAX(columna) FROM tabla;                 -- Máximo
SELECT MIN(columna) FROM tabla;                 -- Mínimo
SELECT SUM(columna) FROM tabla;                 -- Suma
SELECT STDDEV(columna) FROM tabla;              -- Desviación estándar
```

### Agrupación y Filtrado
```sql
-- GROUP BY
SELECT categoria, COUNT(*) FROM tabla 
GROUP BY categoria;

-- HAVING (filtrar grupos)
SELECT categoria, COUNT(*) as total FROM tabla 
GROUP BY categoria 
HAVING COUNT(*) > 10;

-- ORDER BY
SELECT * FROM tabla 
ORDER BY columna DESC;  -- ASC para ascendente
```

### Subconsultas y CTEs
```sql
-- Subconsulta
SELECT columna FROM tabla 
WHERE columna IN (SELECT columna FROM otra_tabla WHERE condicion);

-- CTE (Common Table Expression)
WITH cte AS (
    SELECT columna, COUNT(*) as total 
    FROM tabla 
    GROUP BY columna
)
SELECT * FROM cte WHERE total > 5;
```

## Codificaciones de Base de Datos

Las codificaciones son cruciales para el almacenamiento eficiente de datos:

- **UTF-8**: Codificación estándar que soporta múltiples idiomas (recomendada)
- **UTF-16**: Codificación de ancho variable para todos los caracteres Unicode
- **ISO-8859-1**: Soporte para idiomas de Europa Occidental
- **ASCII**: Codificación básica para caracteres en inglés
- **Latin-1**: Similar a ISO-8859-1, ampliamente utilizada

## Consejos Adicionales

1. **Optimización de memoria**:
   ```python
   # Especificar tipos de datos al leer
   dtypes = {'columna1': 'int32', 'columna2': 'category'}
   df = pd.read_csv('archivo.csv', dtype=dtypes)
   ```

2. **Procesamiento de grandes datasets**:
   ```python
   # Usar chunks para archivos grandes
   chunk_iter = pd.read_csv('archivo_grande.csv', chunksize=10000)
   for chunk in chunk_iter:
       procesar(chunk)
   ```

3. **Manejo de fechas**:
   ```python
   df['fecha'] = pd.to_datetime(df['fecha_columna'])
   df['año'] = df['fecha'].dt.year
   df['mes'] = df['fecha'].dt.month
   ```

4. **Conexiones seguras**:
   ```python
   # Usar variables de entorno para credenciales
   import os
   user = os.getenv('DB_USER')
   password = os.getenv('DB_PASSWORD')
   engine = create_engine(f'postgresql://{user}:{password}@localhost/dbname')
   ```

Esta cheatsheet cubre las operaciones más comunes en ingeniería de datos. Siempre consulta la documentación oficial para casos específicos y mejores prácticas.
