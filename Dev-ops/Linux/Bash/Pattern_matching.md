# Pattern matching

Bash has there own [pattern system](https://www.gnu.org/software/bash/manual/html_node/Pattern-Matching.html), which quite similar to regex.
If you want to use regex, use could enable it via the command:`shopt -s extglob`.

## Matching

```sh
"abc abc" =~ (.* .+) # return true
"abcdefg" =~ (.* .+) # return false
```

## Search and replace

```sh
a_variable="abc abc abc"
${a_variable//' '/'_'} # replace all appearances, return 'abc_abc_abc'
${a_variable/' '/'_'} # replace the first appearance, return 'abc_abc abc'
```
