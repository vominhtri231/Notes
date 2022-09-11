# Read

The command for reading an input into variables.

```sh
IFS=' ' read a b <<< "abcdef 12345"
# a=abcdef b=12345
```

```sh
while IFS= read -r text
do
    # read input file by line and saved each line into variable text 
done < "$inputFile"
```
