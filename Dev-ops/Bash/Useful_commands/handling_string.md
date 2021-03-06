# Commands for handling string

## sed

The command for edit the stream

* --regexp-extended, -E, -r : use extended regular expression, which is more modern
* -e: for specify the expression, usually can be omit, but can be useful if there are emultiple expressions

```sh
sed -e '/^[^*]/d' -e 's/*  \(.*\)/(\1)/'
```

* --in-place[=SUFFIX] , -i[SUFFIX]: edit file in place, makes backup if suffix is supplied

Useful expressions:

* Replace `s`

```sh
sed 's/{{find}}/{{replace}}/' # do replacement once
sed 's/{{find}}/{{replace}}/g' # do replacement until there is no matches
sed 's/{{find}}/{{replace}}/2' # do replacement for the second match only
sed 's/{{find}}/{{replace}}/2g' # do replacement from the second match

# Eg:  "anything between a and b" -> "a b"
sed -E 's/^.*between (.*) and (\.*) .*$/\1 \2/'
```

* Delete `d:`

```sh
sed '/{{line-pattern}}/d' # delete the line pattern
sed '3d' # delete the 3rd line
```

## awk

The column-based stream processor.  
It use variable from $1 -> $n for mapping column 1->n; $0 for the entire row; $NF for the last column.

```sh
awk '($1>=2 && $1<10) {print $3}' 
# print the 3 column if the first column is greater than 2 and less than 10
```

`awk` command use AWK language for manipulating data. The language is a sequence of 'pattern {action}' pairs. By default the pattern would match all and the action would print all.

* -F: specify different separator (The default separator is space)

## grep

Command for matching expression

* -o : print the matching result, each to a sepratate line

## wc

The command for counting lines, words, bytes, etc.  
Useful flags: -l for lines, -w for word, -c for bytes, -m for characters

## `sort` and `uniq`

`sort` can sort the lines, and uniq could output the unique lines of **sorted** input

```sh
sort | uniq     # Display each line once
sort | uniq -u  # Display only unique lines
sort | uniq -d  # Display only duplicate lines
sort | uniq -c  # Display each line with frequency

sort -k 3n      # sort by the third column as number 
```

## paste

Command for merging lines

Useful flags: 

* -s for merge into a single line
* -d for specify the delimiter
