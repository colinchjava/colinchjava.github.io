---
layout: post
title: "Matching specific URL patterns with Java regular expressions"
description: " "
date: 2023-10-01
tags: [Tech, JavaRegularExpressions]
comments: true
share: true
---

URL patterns play a crucial role in web development, allowing us to match and handle various URLs effectively. Java provides powerful regular expressions (regex) capabilities that allow us to define and match complex patterns.

In this article, we'll explore how to use Java regular expressions to match specific URL patterns. We'll cover common scenarios such as matching protocol, domain, path, and query parameters.

## 1. Matching the Protocol

To match the protocol of a URL (e.g., `http`, `https`, `ftp`), we can use the following Java regular expression:

```java
String url = "http://www.example.com";

if (url.matches("^https?://.*")) {
    System.out.println("Protocol matched!");
}
```

The regular expression `^https?://.*` checks if the URL starts with `http://` or `https://`, followed by any characters.

## 2. Matching the Domain

To match the domain of a URL, we can use the following Java regular expression:

```java
String url = "http://www.example.com";

if (url.matches("^https?://([a-zA-Z]+\\.)?example\\.com.*")) {
    System.out.println("Domain matched!");
}
```

The regular expression `^https?://([a-zA-Z]+\\.)?example\\.com.*` checks if the URL starts with `http://` or `https://`, followed by an optional subdomain (`[a-zA-Z]+\\.`), then the domain `example.com`, and any characters after that.

## 3. Matching the Path

To match the path of a URL, we can use the following Java regular expression:

```java
String url = "http://www.example.com/products/1234";

if (url.matches("^https?://([a-zA-Z]+\\.)?example\\.com/[a-zA-Z0-9]+.*")) {
    System.out.println("Path matched!");
}
```

The regular expression `^https?://([a-zA-Z]+\\.)?example\\.com/[a-zA-Z0-9]+.*` checks if the URL starts with `http://` or `https://`, followed by an optional subdomain, the domain `example.com`, a slash `/`, and one or more alphanumeric characters in the path.

## 4. Matching Query Parameters

To match query parameters in a URL, we can use the following Java regular expression:

```java
String url = "http://www.example.com/products?id=1234&category=electronics";

if (url.matches("^https?://([a-zA-Z]+\\.)?example\\.com/products\\?id=[0-9]+&category=[a-zA-Z]+.*")) {
    System.out.println("Query parameters matched!");
}
```

The regular expression `^https?://([a-zA-Z]+\\.)?example\\.com/products\\?id=[0-9]+&category=[a-zA-Z]+.*` checks if the URL starts with `http://` or `https://`, followed by an optional subdomain, the domain `example.com`, `/products`, and specific query parameters (`id` should be numeric and `category` should be alphabetic).

## Conclusion

Java regular expressions provide a powerful toolset for matching specific URL patterns. By using regex, we can easily handle various URL scenarios such as matching protocols, domains, paths, and query parameters. Being familiar with regular expressions empowers us to manipulate and process URLs effectively in our Java applications.

#Tech #JavaRegularExpressions