# Find

Command for search for files, directories, etc

```sh
# find all files/directories whose name contains `abc`
find . -name '*abc*'

# find all folders named `src`
find . -name 'src' -type d 

# find all files with path
find . -path '**/src/.java' -type f

# find all files end with `.tmp` and delete them
find . -name '*.tmp' -exec rm {} \;
find . -name '*.tmp' -delete
```

## Useful flag

* `-path` : specify the path
* `-name`: specify the name
* `-type`: specify the type (d - directory, f - file)
* `-maxdepth`: specify the maximum depth
* `-mindepth`: specify the minimum depth
* `-not`: reverse the condition
