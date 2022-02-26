# Data Engineering

## Introduction to Data Engineering
### Data Engineer
- Streamline data acquisition
- Cloud technology
- Develop scalable data architecture
- Setup processes to bring data together
- Clean corruption data

### Data Engineering Tools
- Database
	- SQL, NoSQL
- Processing
	- clean, aggregate, join
	- Spark
- Scheduling
	- jobs with intervals
	- resolve dependency requirement
	- Airflow

### Cloud Computing
- self-host data-center problem
	- cost
	- peak and quite time usage gap
	- reliability
- Big 3
	- Storage
		- AWS S3, Azure Blob, Google Cloud
	- Computation: perform job
		- AWS EC2, Azure Virtual Machines, Google Compute Engine
	- Databases
		- AWS RDS, Azure SQL Database, Google Cloud SQL

## Data Engine Toolbox
### Databases
- Database: collection of organized data for rapid search and retrieval
	- Structured: schema 
	- Semi Structured: json
	- Unstructured: schemaless, videos, photos
- SQL: relational databases
	- MySQL, PostgreSQL
- NoSQL: Non-relational databases
	- Structured or unstructured
	- MongoDB, 

```python
# Complete the SELECT statement
data = pd.read_sql("""
SELECT first_name, last_name FROM "Customer"
ORDER BY last_name, first_name
""", db_engine)

# Show the first 3 rows of the DataFrame
print(data.head(3))

# Show the info of the DataFrame
print(data.info())
```


### Parallel computing
- problem: memory and processing power
- idea: split task into subtasks and distribute them over several computers
- risks: overhead due to communication
	- 오버헤드(overhead)는 어떤 처리를 하기 위해 들어가는 간접적인 처리 시간 · 메모리 등을 말한다. 예를 들어 A라는 처리를 단순하게 실행한다면 10초 걸리는데, 안전성을 고려하고 부가적인 B라는 처리를 추가한 결과 처리시간이 15초 걸렸다면, 오버헤드는 5초가 된다. 또한 이 처리 B를 개선해 B’라는 처리를 한 결과, 처리시간이 12초가 되었다면, 이 경우 오버헤드가 3초 단축되었다고 말한다
- multiprocessing frameworks: dask

```python
# Function to apply a function over multiple cores
@print_timing
def parallel_apply(apply_func, groups, nb_cores):
    with Pool(nb_cores) as p:
        results = p.map(apply_func, groups)
    return pd.concat(results)

# Parallel apply using 1 core
parallel_apply(take_mean_age, athlete_events.groupby('Year'), 1)

# Parallel apply using 2 cores
parallel_apply(take_mean_age, athlete_events.groupby('Year'), 2)

# Parallel apply using 4 cores
parallel_apply(take_mean_age, athlete_events.groupby('Year'), 4)
```

```python
import dask.dataframe as dd

# Set the number of partitions
athlete_events_dask = dd.from_pandas(athlete_events, npartitions=4)

# Calculate the mean Age per Year
print(athlete_events_dask.groupby('Year').Age.mean().compute())

```


### Parallel computing frameworks
- Apache Hadoop
	- HDFS: distributed filesystem on multiple computers
	- MapReduce: distributing subtasks into several computers, Hard to use
- Hive
	- Use Hive SQL to transform into a job that can operate on a several computers
- Apache Spark
	- avoid expensive disk writes between jobs
	- Keep as much as possible in memory
	- Resilient distributed datasets(RDDs)
		- similar to list of tuples
		- can perform transformations, actions
	- PySpark

```python
# Print the type of athlete_events_spark
print(type(athlete_events_spark))

# Print the schema of athlete_events_spark
print(athlete_events_spark.printSchema())

# Group by the Year, and find the mean Age
print(athlete_events_spark.groupBy('Year').mean('Age'))

# Group by the Year, and find the mean Age
print(athlete_events_spark.groupBy('Year').mean('Age').show())

```

### Workflow scheduling frameworks
- DAGs: Directed Acyclic Graph
- Linux cron, Spotify Luigi, Apache Airflow
- Airflow: DAGs, Python

```python
# Create the DAG object
dag = DAG(dag_id="car_factory_simulation",
          default_args={"owner": "airflow","start_date": airflow.utils.dates.days_ago(2)},
          schedule_interval="0 * * * *")

# Task definitions
assemble_frame = BashOperator(task_id="assemble_frame", bash_command='echo "Assembling frame"', dag=dag)
place_tires = BashOperator(task_id="place_tires", bash_command='echo "Placing tires"', dag=dag)
assemble_body = BashOperator(task_id="assemble_body", bash_command='echo "Assembling body"', dag=dag)
apply_paint = BashOperator(task_id="apply_paint", bash_command='echo "Applying paint"', dag=dag)

# Complete the downstream flow
assemble_frame.set_downstream(place_tires)
assemble_frame.set_downstream(assemble_body)
assemble_body.set_downstream(apply_paint)

```

## ETL
### Extract
- storage/database to memory
- plain test
- json(JavaScript Object Notation): Semi-structured
- Data on the Web: Requests, Response, API
- Data in databases
	- OLAP: Online analytical processing
	* OLTP: Online transaction processing

```python
# Function to extract table to a pandas DataFrame
def extract_table_to_pandas(tablename, db_engine):
    query = "SELECT * FROM {}".format(tablename)
    return pd.read_sql(query, db_engine)

# Connect to the database using the connection URI
connection_uri = "postgresql://repl:password@localhost:5432/pagila" 
db_engine = sqlalchemy.create_engine(connection_uri)

# Extract the film table into a pandas DataFrame
extract_table_to_pandas("film", db_engine)

# Extract the customer table into a pandas DataFrame
extract_table_to_pandas("customer", db_engine)

```

### Transform
- selection, translation, validation, splitting, joining

```python
# Get the rental rate column as a string
rental_rate_str = film_df.rental_rate.astype("str")

# Split up and expand the column
rental_rate_expanded = rental_rate_str.str.split(".", expand=True)

# Assign the columns to film_df
film_df = film_df.assign(
    rental_rate_dollar=rental_rate_expanded[0],
    rental_rate_cents=rental_rate_expanded[1],
)
```

```python
# Use groupBy and mean to aggregate the column
ratings_per_film_df = rating_df.groupBy('film_id').agg({'rating': 'mean'})

# Join the tables using the film_id column
film_df_with_ratings = film_df.join(
    ratings_per_film_df,
    film_df.film_id==ratings_per_film_df.film_id
)

# Show the 5 first results
print(film_df_with_ratings.show(5))

```

### Loading
- Analytics
	- Aggregate queries
	- Column-oriented
- Applications
	- Lots of transactions
	- Row-oriented
- Massively Parallel Processing Databases
	- Amazon Redshift

```# Finish the connection URI
connection_uri = "postgresql://repl:password@localhost:5432/dwh"
db_engine_dwh = sqlalchemy.create_engine(connection_uri)

# Transformation step, join with recommendations data
film_pdf_joined = film_pdf.join(recommendations)

# Finish the .to_sql() call to write to store.film
film_pdf_joined.to_sql("film", db_engine_dwh, schema="store", if_exists="replace")

# Run the query to fetch the data
pd.read_sql("SELECT film_id, recommended_film_ids FROM store.film", db_engine_dwh)

```
