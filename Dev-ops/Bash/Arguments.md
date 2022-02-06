# Argument

## Position parameters

Using `$1` to get the first parameter and so on.  
Using `$?` to get the last command return code (0 if success)  
Using `$@` to get the parameter list  
Using `$#` to number of arguments
Using `$$` to get the program PID

## Named parameters

Using `getopts` to parse the named parameters

```sh
file='default-file'
dir='default-dir'
while getopts f:d: params
do
  case $params in
    f) file="$OPTARG";;
    d) dir="$OPTARG";; 
  esac
done
shift "$((OPTIND - 1 ))"# shift parameters to last parameters
```
