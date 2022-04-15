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

## Control Statements

### IF

```bash
if [ CONDITION ]; then
    COMMAND
elif [ CONDITION ]; then
    COMMAND
else
    COMMAND
fi
```
- Warning
    - Spaces between `[` and `]`
    - Don't forget `;`
- Flags
    - `-eq`: equal
    - `-ne`: not equal
    - `-gt`: greater than
    - `-ge`: greater than or equal
    - `-lt`: less than
    - `-le`: less than or equal
    - `-z`: empty
    - `-e`: exists
    - `-s`: exists and not empty
    - `-r`: readable
    - `-w`: writable
- `&&`: AND
- `||`: OR
- Structure
    1. `if [ $x -gt 5 ] && [ $x -lt 15 ]; then`
    2. `if [[ $x -gt 5  && $x -lt 15 ]]; then`
    3. `if [ $x -gt 5 -a $x -lt 15 ]; then`

### For & While

```bash
#for loop
for x in 1 2 3
do
    echo $x
done
```

```bash
# while loop
x=1
while [ $x -le 10 ];
do
    echo $x
    x=$((x+1))
done
```

- `for` loop
    - `for x in 1 2 3`
    - `for x in {1..5..2}` # start..stop..increment
    - `for ((x=2;X,=4;x+=2))`
- glob expansions
    - `for book in books/*`
    - `for book in $(ls books/ | grep -i 'air')`

### CASE

```bash
case 'STRINGVAR' in
    PATTERN1)
        COMMAND1;;
    PATTERN2)
        COMMAND2;;
    *)
        DEFALUT COMMAND;;
esac
```
- Alternative to `if` when there's a multiple conditions

## Functions

```bash
function function_name {
    # function code
    return # result
}
```

```bash
# ex)
temp_f = 30
function convert_temp_f_to_c {
    temp_c=$(echo "scale=2; ($1 - 32) * 5 / 9" | bc)
    echo $temp_c
}
```

### Arguments, return values, and scope

- `$1`: First argument
- `$@`, '$*': All arguments
- `$#`: Number of arguments
- `$?`: Return value
- Scope: Global, Local
    - All variables are global by default
- `return`: only meant to determine if the function is successful
    - `return 0`: successful
    - `return 1`: failed

```bash
# Return structure in shell script
function convert_temp_f_to_c {
    temp_c=$(echo "scale=2; ($1 - 32) * 5 / 9" | bc)
    echo $temp_c

converted=$(convert_temp_f_to_c 30)
echo $converted
```

### Cron

- Chronos
- `crontab`: driver of `cronjob`
- `cronjob`: a task that runs periodically
    - `5 1 * * * bash my_script.sh`: run every day at 1:05
    - `15 14 * * 7 bash my_script.sh`: run every Sunday at 14:15
    - `15,30,45 * * * * bash my_script.sh`: run at 15, 30, 45 minutes
    - `*/15 * * * * bash my_script.sh`: run every 15 minutes
