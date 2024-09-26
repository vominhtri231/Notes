# Regex

## Captured group

For capturing different part of the matched content.

**Group index**

The group index is the number of open bracket(s) of the captured group
 E.G. Regex`(d+) ([a-z])`

- group 0 is the whole message
* group 1 is //d+
- group 2 is [a-z]

**Non-captured group**

If needed the bracket but don't want to capture it, we can use non-captured group syntax `?:`. This could reduce the memory overhead because the non-captured group don't store the matched content.

E.G. Regex `(d+) (?:abc|def)?` -> The group 2 is non-captured


