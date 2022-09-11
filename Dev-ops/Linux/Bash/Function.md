# Function

## Declare function

```sh
my_function() {
    ...
}

function my_function() {
    ...
}
```

## Variable scope

In bash, by default any variable is global unless it is declared as a local variable. A local variable is only accessible in the function containing it.

```sh
function my_function(){
    local a=1; # only accessible in the function
    b=2 # accessible everywhere 
}
```

## Passing arguments

Just like [script arguments](./Arguments.md), you could access the function argument via $1,$2,etc.

```sh
function my_function(){
    local a=$1
}

my_function "1"
```

## Return value

Unlike other programing language, Bash does not allow you to return a value when called. The `return` keyword works more or less like the `exit` keyword of the script, which returns a status code.

```sh
my_function () {
  echo "some result"
  return 55
}

my_function
echo $?
```
