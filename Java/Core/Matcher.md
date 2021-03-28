## Matcher
```java
Pattern pattern = Pattern.compile(regex);
Matcher macher = pattern.match(matchingString);

// find the the next matched string, return true if successful
matcher.find(); 

// To get all matched string
while (matcher.find()) {
        matcher.group(0); 
}

// The group index is the number of open bracket(s)
// Eg: With  regex: "(//d+) ([a-z])" 
//    - group 0 is the whole message
//    - group 1 is //d+
//    - group 2 is [a-z]
macher.group(0); 

// replace matched string
matcher.replaceAll(replaceString);
matcher.replaceFirst(replaceString);

// Indexes of the matched string
matcher.first();
matcher.last();
```

## String utilities that use matcher under the hook
```java
s.split(regex)
s.replaceAll(regex,replaceString);
s.replaceFirst(regex,replaceString);

// if you only need to replace string rather than regex, you should use replace instead
s.replace(matchingString,replaceString)
```
