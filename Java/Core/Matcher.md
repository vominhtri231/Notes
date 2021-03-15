## Matcher

```java
Pattern pattern = Pattern.compile(regex);
Matcher macher = pattern.match(matchingString);

// find the the next matched string, return true if successfull
matcher.find(); 

// To get all matched string
while (matcher.find()) {
        matcher.group(0); 
}

// The group index is the number of open bracket
// Eg: With  regex: "(//d+) ([a-z])" 
//    - group 0 is the whold message
//    - group 1 is //d+
//    - group 2 is [a-z]
macher.group(0); 

// relace matched string
matcher.replaceAll(replaceString);
matcher.replaceFirst(replaceString);

// Indexes of the matched string
matcher.first();
matcher.last();
```

## String ultilities that use matcher under the hook

```java
s.split(regex)
s.replaceAll(regex,replaceString);
s.replaceFirst(regex,replaceString);
```
