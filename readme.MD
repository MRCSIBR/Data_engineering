
### Python for Data Engineering:
Cheatsheet for Python in data engineering along with some commonly used SQL queries:

#### Libraries:
- **Pandas**: For data manipulation and analysis.
- **NumPy**: For numerical computing.
- **SQLAlchemy**: For SQL toolkit and Object-Relational Mapping (ORM).

#### Data Handling:
- **Reading Data**:
  ```python
  import pandas as pd
  data = pd.read_csv('file.csv')  # Reading CSV
  data = pd.read_json('file.json')  # Reading JSON
  ```

- **Data Exploration**:
  ```python
  data.head()  # View first few rows
  data.describe()  # Summary statistics
  data.info()  # Information about columns and data types
  ```

- **Data Cleaning**:
  ```python
  data.isnull().sum()  # Check for missing values
  data.fillna(value)  # Fill missing values
  data.dropna()  # Drop rows with missing values
  ```

- **Data Transformation**:
  ```python
  data['new_column'] = data['column1'] + data['column2']  # Create new column
  data['column'].apply(function)  # Apply function to a column
  ```

- **Data Manipulation**:
  ```python
  data.groupby('column').agg({'other_column': 'mean'})  # Grouping and aggregation
  data.pivot_table(values='value', index='index', columns='columns')  # Pivot tables
  ```

- **Data Visualization**:
  ```python
  import matplotlib.pyplot as plt
  data.plot(kind='bar')  # Creating a bar plot
  plt.show()
  ```

#### SQL Queries:

##### Common SQL Queries:

- **Select Query**:
  ```sql
  SELECT column1, column2 FROM table_name WHERE condition;
  ```

- **Insert Query**:
  ```sql
  INSERT INTO table_name (column1, column2) VALUES (value1, value2);
  ```

- **Update Query**:
  ```sql
  UPDATE table_name SET column1 = value1 WHERE condition;
  ```

- **Delete Query**:
  ```sql
  DELETE FROM table_name WHERE condition;
  ```

- **Join Queries**:
  ```sql
  SELECT * FROM table1 INNER JOIN table2 ON table1.key = table2.key;
  ```

- **Aggregate Functions**:
  ```sql
  SELECT COUNT(column) FROM table_name;
  SELECT AVG(column) FROM table_name;
  SELECT MAX(column) FROM table_name;
  SELECT MIN(column) FROM table_name;
  ```

- **Group By and Having**:
  ```sql
  SELECT column1, COUNT(*) FROM table_name GROUP BY column1 HAVING COUNT(*) > 1;
  ```

- **Subqueries**:
  ```sql
  SELECT column FROM table_name WHERE column IN (SELECT column FROM other_table);
  ```

These snippets are just a starting point. Data engineering involves a wide range of tasks, so always refer to documentation or resources for more specific use cases and functions.
