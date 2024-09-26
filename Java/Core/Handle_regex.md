# # Handle regex

## Matcher

```java
Pattern pattern = Pattern.compile(regex);
Matcher matcher = pattern.match(matchingString);

// find the the next matched string, return true if successful
matcher.find(); 

// To get all matched string
while (matcher.find()) {
    matcher.group(0); 
}

// get group index 1
matcher.group(1);

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
s.replaceAll(regex, replaceString);
s.replaceFirst(regex, replaceString);

// if you only need to replace string rather than regex, you should use replace instead
s.replace(matchingString, replaceString)
```
