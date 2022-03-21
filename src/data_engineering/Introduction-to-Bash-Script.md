# Bash

- Bourne Again Shell
- Group bash commands in `.sh` file to save and run

## Sed

## Standard streams & Arguments

- STDIN(Standard Input): A stream of data into the program
- STDOUT(Standard output): A stream of data out of the program
- STDERR(Standard Error): Errors in your program
- ARGV(Argument): `$` notation means args
	- $1: first arg
	- $@: all args
	- $#: how many args

## Variables

- Assign vars as `var1="Moon"` and use var as `echo $var1`
	- Bash doesn't have mercy for space between `=`
- Single quotes = literal statement
- Double quotes = literal statement except using `$` and backticks
- Backticks
	- Shell within a shell
	- Captures STDOUT back into a variable
	- Parenthesis is used more now as `$(date)`

### Numeric Variables

```bash
model1=84
model2=33
echo "Total score: $(echo "$model1 + $model2" | bc )"
echo "Avg. score: $(echo "($model1 + $model2) / 2" | bc )"
```

### Arrays

- Use space to seperate elements
- `arr=(1 2 3)`
- `echo ${arr[2]}`
- `echo ${arr[@]}`
- `echo ${#arr[@]}`
- `echo ${#arr[@]:N:M}`
	- `N` is starting index and `M` is how many elements to return
- Append to an array `arr[@]+=(10)`
- Associative array, similar to dict
	- `declare -A cities=([city_name]="New York" [population]=1440)`
	- `$cities[city_name]`
	- `echo ${!cities[@]}`


