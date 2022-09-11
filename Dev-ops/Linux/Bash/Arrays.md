# Arrays

Bash supports one-dimensional numerical arrays and associate arrays (as like map). Element in a arrays don't have to have the same type but can't be an array (no multiple-dimensional arrays).

## Declaration

```sh
# declare a numerical array
## explicitly
declare -a my_array=( "a" "b" "c" )
## implicitly
my_array=( "a" "b" "c" )

# an associate array must be declared explicitly using -A flag
declare -A my_associate_array
```

## Access array

For numeric arrays, you can use the negative index to access from the bottom of the array

```sh
echo {my_array[1]}
echo {my_associate_array["abc"]}
echo {my_array[-1]}

# all elements in an array
echo "${my_array[@]}"
# all index of an array
echo "${!my_array[@]}"
# length of the array
echo "${#my_array[@]}"
```

## Edit array

```sh
# Set element at an index
my_array[3]="abc"
my_associate_array["a_key"]="abc"

# Add to last for numeric array
my_array+=("xyz")

# Delete an element
unset my_array[3]
unset my_associate_array["a_key"]
```

## Sub array for numeric array

```sh
# Sub array from 2
my_array[@]:2

# Sub array from 2 to 4
my_array[@]:2:4
```
