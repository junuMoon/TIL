# Data Processing in Shell

## Introduction to Shell

- [ls](https://linuxgazette.net/issue48/fischer.html): list files
	- In its earliest form it was called listf and was available on the Massachusetts Institute of Technology's Compatible Time Sharing System (CTSS)
	- In 1965, listf was extended to recognize ``*'' as a way to list all files that matched a specific pattern
	- When Bell Labs dropped out of Multics development in 1969 and work began on Unix, only the abbreviated name of list, ls, was retained.
- cd: change directory
- pwd: print working directory
- cp: copy
- mv: move
- rm: remove
- rmdir: remove directory
- cat: [Why "cat" command is known as "cat"?](https://coderanch.com/t/111284/os/cat-command-cat)
	- concatenate: 사슬 같이 잇다
- less:
	- terminal pager program to view the contents one screen at a time
	- `less` does not need to read the entire file before starting, allowing for immediate viewing regardless of file size.
	- more는 위에서 아래 방향으로만 출력 되지만, 지나간 내용을 다시 볼 수 없지만, less는 한 번에 보여지는 만큼만 읽어서 출력하기 때문에 대용량의 파일을 열어 볼 때 빠르게 사용 할 수 있다.
	-  The name came from the joke of doing "backwards more."
	- To help remember the difference between less and more, a common joke is to say, "less > more," implying that less has greater functionality than more. A similar saying is that "less is more, more or less".
- head: print the top N number of data
- tail: print the last N number of data
- cut: cut is a command-line utility that allows you to cut parts of lines from specified files or piped data and print the result to standard output. It can be used to cut parts of a line by delimiter, byte position, and character.
	- 텍스트 파일을 다양한 방법으로 분리할 수 있음
- history
- !2
- [grep](https://www.makeuseof.com/how-grep-got-its-name-the-history-behind-greps-creation/)
	- Gloabl Regular Expression Print
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
