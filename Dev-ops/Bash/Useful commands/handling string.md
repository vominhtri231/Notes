# Command for handling string

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

The column-based stream processor

```sh
awk '($1>=2 && $1<10) {print $3}' 
# print the 3 column if the first column is greater than 2 and less than 10

awd -F ',' ... 
# use comma instead of space as separator
```

## paste

Command for merging lines
Useful flags: -s for merge into a single line, -d for specify the delimiter
