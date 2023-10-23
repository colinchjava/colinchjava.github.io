---
layout: post
title: "Implementing a word frequency counter using HashMap in Java"
description: " "
date: 2023-10-23
tags: [HashMap]
comments: true
share: true
---

In this blog post, we will explore how to implement a word frequency counter using the HashMap data structure in Java. The word frequency counter is a common task in natural language processing, where the goal is to count the occurrences of each word in a given text.

### Creating the HashMap

First, let's create a HashMap to store the words and their corresponding frequencies. We will use the word as the key and the frequency as the value:

```java
import java.util.HashMap;

public class WordFrequencyCounter {
    private HashMap<String, Integer> wordFrequency;

    public WordFrequencyCounter() {
        wordFrequency = new HashMap<>();
    }
}
```

### Counting the Word Frequencies

Next, let's implement a method to count the word frequencies. We will split the input text into individual words using the `split()` method and iterate over each word. If the word already exists in the HashMap, we will increment its frequency count. Otherwise, we will add a new entry with a frequency count of 1:

```java
public void countWords(String text) {
    String[] words = text.split("\\s+");

    for (String word : words) {
        word = word.toLowerCase();

        if (wordFrequency.containsKey(word)) {
            int frequency = wordFrequency.get(word);
            wordFrequency.put(word, frequency + 1);
        } else {
            wordFrequency.put(word, 1);
        }
    }
}
```

### Retrieving the Word Frequencies

To retrieve the word frequencies, we can create a method that returns the HashMap:

```java
public HashMap<String, Integer> getWordFrequencies() {
    return wordFrequency;
}
```

### Example Usage

Now, let's see an example of how to use the `WordFrequencyCounter` class:

```java
public class Main {
    public static void main(String[] args) {
        WordFrequencyCounter frequencyCounter = new WordFrequencyCounter();
        String text = "This is a sample text sample to test the word frequency counter.";

        frequencyCounter.countWords(text);
        HashMap<String, Integer> wordFrequencies = frequencyCounter.getWordFrequencies();

        for (String word : wordFrequencies.keySet()) {
            int frequency = wordFrequencies.get(word);
            System.out.println(word + ": " + frequency);
        }
    }
}
```

Output:
```
this: 1
is: 1
a: 1
sample: 2
text: 1
to: 1
test: 1
the: 1
word: 1
frequency: 1
counter.: 1
```

### Conclusion

In this blog post, we have implemented a word frequency counter using the HashMap data structure in Java. The HashMap allows us to efficiently store the word frequencies by using the word as the key and the frequency as the value. This implementation can be useful in various natural language processing tasks, such as text analysis and information retrieval.

Please check out the code on [GitHub](https://github.com/example/word-frequency-counter) for the complete implementation and feel free to customize it according to your specific requirements.

#java #HashMap