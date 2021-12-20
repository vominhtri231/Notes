# Commands for handling string

## sed

The command for edit the stream

### Useful flags

* --regexp-extended, -E : use extended regular expression, which more modern
* --in-place[=SUFFIX] , -i[SUFFIX]: edit file in place, makes backup if suffix is supplied

### Examples

* Replace string

```sh
sed 's/{{find}}/{{replace}}/' # do replacement once
sed 's/{{find}}/{{replace}}/g' # do replacement until there is no matches
```

* Delete line match regular expression

```sh
sed '/{{line-pattern}}/d'
```

## wc

The command for counting lines, words, bytes, etc.  
Useful flags: -l for lines, -w for word, -c for bytes, -m for characters

## `sort` and `uniq`

`sort` can sort the lines, and uniq could output the unique lines of sorted input

```sh
sort | uniq     # Display each line once
sort | uniq -u  # Display only unique lines
sort | uniq -d  # Display only duplicate lines
sort | uniq -c  # Display each line with frequency

sort -k 3n      # sort by the third column as number 
```

## awk

The column-based stream processor.  
It use variable from $1 -> $n for mapping column 1->n; $0 for the entire row; $NF for the last column.

```sh
awk '($1>=2 && $1<10) {print $3}' 
# print the 3 column if the first column is greater than 2 and less than 10
```

### AWK language

`awk` command use AWK language for manipulating data. The language is a sequence of 'pattern {action}' pairs. By default the pattern would match all and the action would print all.

### Useful flag

* -F: specify different separator (The default separator is space)

## paste

Command for merging lines
Useful flags: -s for merge into a single line, -d for specify the delimiter
