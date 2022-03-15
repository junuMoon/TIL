# Data Processing in Shell

## Introduction to Shell

- ls
- cd
- pwd
- cp
- mv
- rm
- rmdir
- cat
- less
- head
- tail
- cut
- history
- !2
- grep -
- paste: merge
- sort
- uniq
- wc
- echo
- for in do done
- $@

## Data Processing in Shell
### Download Data
- Curl: Client for URLs
	- -L: redirect
	- -o/-O: save
	- -C: continue
- Wget: World Wide Web and get
	- download recursively
	- -bqc
	- `-i a.txt`
	- `—wait={seconds}`

### Data Handling
- csvkit
	- in2csv
	- csvlook
	- csvstat
	- csvcut
	- csvgrep
	- csvstack
	- csvsort

## Database Operations on the Command Line

- Pulling data: sql2csv
	- sqlite: `sqlite:///dbname.db`
	- postgre, mysql: `postgres:///dbname`, `mysql:///dbname`
- Manipulating data
	- csvsql
	- creates an in-memory SQL Database -> suitable for small to medium files only
	- `csvsql --query "query" out_file_name.csv`
- Pushing data using csvsql
	- `csvsql --db "dbengine" --insert in_file_name.csv`
	- `--no-inference`: Disable type inference
	- `--no-constraints`: Generate a schema wihtout length limits or null checks

## Data Pipeline on the command line

### Data job automation

- scheduler: runs jobs on a set schedule
- cron: time based job-scheduler native to linux
- crontab: central file to keep track of cron jobs
- add a job to crontab: `* * * * *  python python_file.py`
