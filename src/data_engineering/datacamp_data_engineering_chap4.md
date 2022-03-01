# Streamlined Data Ingestion with pandas
#data

## Introduction to Flat Files
### Pandas
- Flat files
	- data stored as plain text
	- one row per line
	- columns seperated by a delimieter
- Pandas can read flat files and convert it to DataFrame

### Handling errors and missing data
- pandas automatically infers column data types
	- `pd.info()`
- Lines with error
	- `error_bad_lines=False` to skip inseparable records
	- `warn_bad_lines=True` to see when records are skipped

## Introduction to Databases
- SQLAlchemy  `create_engine` makes engine to handle db connection

### SQL
- select
- where [condition]
- filtering numbers: =, >, <, <>
- filtering text: =
- AND / OR

### More compile SQL queries
- Getting distinct values
	- `SELECT DISTINCT [col name] from [table];`
- Aggregate func
	- SUM, AVG, MAX, MIN, COUNT
- GROUP BY

### JOIN
- records have unique identifiers, or keys
- default join only returns records whose key values appear in both tables
- make sure join keys are the same data type or nothing will match

## JSON
- common web data format
- not tabular: records don’t have to all have the same set of attrs
- collections of objects
- `pd.read_json` 
	- `orient` keyword arg to flag uncommon JSON data layouts
- record oriented
- columns oriented: space-efficient
- split oriented:

### Oriented
* ‘split’ : dict like {index -> [index], columns -> [columns], data -> [values]}
* ‘records’ : list like [{column -> value}, … , {column -> value}]
* ‘index’ : dict like {index -> {column -> value}}
* ‘columns’ : dict like {column -> {index -> value}}
* ‘values’ : just the values array

### API
- Defines how a application communicates with other programs

### Nested JSONs
- Json normalize
- 실제에서는 nested하게 되어있는 경우가 많다
- [pandas.json_normalize — pandas 1.4.1 documentation](https://pandas.pydata.org/docs/reference/api/pandas.json_normalize.html)

### Combining multiple datasets
- append: append rows
	- ignore_index=True
- merge: add columns
