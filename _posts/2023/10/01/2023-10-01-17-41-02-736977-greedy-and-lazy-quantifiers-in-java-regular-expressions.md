---
layout: post
title: "Greedy and lazy quantifiers in Java regular expressions"
description: " "
date: 2023-10-01
tags: [RegularExpressions]
comments: true
share: true
---

Greedy quantifiers are denoted by the symbol "+" and match as much of the input as possible. They will try to match the longest possible substring that satisfies the pattern. For example, consider the regular expression pattern "a+". If we apply this pattern to the input string "aaaaa", the greedy quantifier will match all the "a" characters, resulting in a full match.

```java
String input = "aaaaa";
String pattern = "a+";

Pattern p = Pattern.compile(pattern);
Matcher m = p.matcher(input);

while (m.find()) {
    System.out.println(m.start() + " - " + m.end());
}
```

Output:
```
0 - 5
```

In contrast, lazy quantifiers are denoted by the symbol "+?" and match as little as possible. They will try to match the shortest possible substring that satisfies the pattern. Continuing with the previous example, if we change the pattern to "a+?", the lazy quantifier will match each "a" individually.

```java
String input = "aaaaa";
String pattern = "a+?";

Pattern p = Pattern.compile(pattern);
Matcher m = p.matcher(input);

while (m.find()) {
    System.out.println(m.start() + " - " + m.end());
}
```

Output:
```
0 - 1
1 - 2
2 - 3
3 - 4
4 - 5
```

By understanding the difference between greedy and lazy quantifiers, you can make your regular expressions more precise and efficient. Greedy quantifiers are useful when you want to match as much of the input as possible, while lazy quantifiers are helpful when you want to find the shortest possible match.

Using these quantifiers appropriately can significantly improve the performance and accuracy of your regular expressions, so make sure to choose the right one for your specific use case.

#Java #RegularExpressions