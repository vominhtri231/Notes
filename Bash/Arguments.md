# Argument

## Position parameters

Using `"$1"` to get the first parameter and so on.  
Using `$@` to get the parameter list

## Named parameters

Using `getopts` to parse the named parameters

```shell
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
