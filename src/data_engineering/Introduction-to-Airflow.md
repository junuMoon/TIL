# Introduction to Airflow

- Data engineering: taking any action involving data and making it a *reliable, repeatable, and maintainable* process
- Workflow: a series of steps to accomplish a given data engineering task

## Airflow

- A framework for automating data engineering workflows
- Implements workflows as DAGs: Directed Acyclic Graphs

```python
etl_dag = DAG(
    dag_id='etl_pipeline',
    default_args={
        'owner': 'junu',
        'start_date': datetime(2020, 1, 1),
        'retries': 1,
        'retry_delay': timedelta(minutes=5),
    },
    schedule_interval='@once',
)
```

- Running a workflow in Airflow

```bash
airflow run <dag_id> <task_id> <start_date>
```
### DAG

- Directed: an inherent flow representing dependencies between components
- Acyclic: not loop / cycle / repeat
- Graph: relationship
- DAG: workflow made up of components(tasks) with dependencies to be executed

## Implementing Airflow DAGs

### Operators

- Represent a single task in a workflow
- Run independently
    - Not guaranteed to run in the same location / environment
- Various operators perform different tasks
    - Can be difficult to run tasks with elevated privileges(실행 권한 i.e, root/admin)

```python
from airflow.operators.bash_operator import BashOperator

bash_task = BashOperator(
    task_id='load_data',
    bash_command='echo "Loading data..."',
    dag=etl_dag,
)
```

### Tasks

- Instances of operators 
- Define a given order of task completion
    - Upstream: before, `<<`
    - Downstream: after, `>>`

```python
task1 = BashOperator(
    task_id='task1',
    bash_command='echo "Task 1"',
    dag=etl_dag,
)

task2 = BashOperator(
    task_id='task2',
    bash_command='echo "Task 2"',
    dag=etl_dag,
)

task1 >> task2
```

#### Bitwise Operators

- `&` (Binary AND) : bit 단위로 and 연산을 합니다. 
- `|` (Binary OR) : bit 단위로 or 연산을 합니다. 
- `^` (Binary XOR) : bit 단위로 xor연산을 합니다. 
- `~` (Binary NOT) : bit 단위로 not연산을 합니다.(1의 보수) 
- `<<` (Binary left Shift) : bit 단위로 왼쪽으로 비트단위 밀기 연산을 합니다. 
- ``>>` (Binary right Shift) : bit 단위로 오른쪽으로 비트단위 밀기 연산을 합니다.

### PythonOperator

- Execute a Python script
- Can pass arguments to the script
- Use `op_kwargs` dictionary for keyword arguments

```python
from airflow.operators.python_operator import PythonOperator

def check_tier(tier):
    print(f'당신은 {tier} 입니다.')

python_task = PythonOperator(
    task_id='print_tier',
    python_callable=check_tier,
    op_kwargs={'tier': '브론즈 4'},
    dag=lol_dag,
)
```

### Other Operators

- `EmailOperator`: Send an email
    - Can contains HTML content, attachments, etc.
- `S3Operator`: Upload/Download files from S3

### Scheduling

- Run a task at a specific time with a specific interval
- State of DAG: running, success, failure
- Attrs: `start_date`, `end_date`, `schedule_interval` ...
- Presets of `schedule_interval`: `None`, `@once`, `@yearly`, `@monthly`, `@weekly`, `@daily`, `@hourly`
- Issue: scheduler run a task at `start_date` + `schedule_interval`

```python
etl_dag = DAG(
    dag_id='etl_pipeline',
    default_args=default_args,
    schedule_interval='30 12 * * 3'
)
```

## Maintaining and monitoring Airflow

### Sensors

- An operator that waits for a condition to be met before continuing
    - Creation of a file, Upload to S3, Response from a web request, etc
    - `FileSensor`, `ExternalTaskSensor`, `HttpSensor`, `SqlSensor`, etc
- Can define how often to check for the condition
- Are assigned to tasks
- Usecase 
    - Uncertain if a task should run
    - If failure not immediate desired -> `mode=reschedule`
    - To add task repetition without loops

#### Sensor attrs

- `mode`
    - `poke`: default, check every time the task is run
    - `reschedule`: check every time the task is run, but reschedule the task if the condition is not met
- `poke_interval`: how often to check for the condition
- `timeout`: how long to wait for the condition to be met
- Also includes normal operator attirbutes

```python
from airflow.sensors.file_sensor import FileSensor

file_sensor_task = FileSensor(
    task_id='file_sense',
    filepath='salesdata.csv',
    poke_interval=300,
    dag=sales_report_dag
)

init_sales_cleanup >> file_sensor_task >> generate_report
```

### Executors

- different executros handle running the tasks differently
- Can determine executor via `airflow.cfg` file
- `SequentialExecutor`: Runs one task at a time
    - While functional, not recommended for production due to the limitations of task resources
- `LocalExecutor`: Runs on a single system
    - Treats tasks as processes
    - *parallelism* defined by the user
    - Can utilize all resources
- `CeleryExecutor`: Multiple worker systems can be defined
    - More complicate so that more powerful
- 