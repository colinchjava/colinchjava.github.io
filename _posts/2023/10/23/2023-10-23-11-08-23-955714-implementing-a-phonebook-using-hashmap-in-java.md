---
layout: post
title: "Implementing a phonebook using HashMap in Java"
description: " "
date: 2023-10-23
tags: [HashMap]
comments: true
share: true
---

In this blog post, we will explore how to implement a phonebook using the `HashMap` data structure in Java. A phonebook is a collection that allows us to store and retrieve phone numbers based on the associated names. The `HashMap` provides an efficient way to perform these operations with constant time complexity (O(1)).

Let's get started!

## Table of Contents
- [Creating a Phonebook](#creating-a-phonebook)
- [Adding Contacts](#adding-contacts)
- [Searching for Contacts](#searching-for-contacts)
- [Updating Contacts](#updating-contacts)
- [Removing Contacts](#removing-contacts)
- [Conclusion](#conclusion)

## Creating a Phonebook

First, we need to create a new `HashMap` instance to serve as our phonebook. We will use the person's name as the key and their corresponding phone number as the value.

```java
import java.util.HashMap;

public class Phonebook {

    private HashMap<String, String> contacts;

    public Phonebook() {
        contacts = new HashMap<>();
    }

    // Other methods can be implemented here
}
```

In the above code, we have defined a `Phonebook` class with a `HashMap` instance named `contacts`.

## Adding Contacts

To add a contact to the phonebook, we simply need to put the name and phone number into the `contacts` map using the `put()` method.

```java
public void addContact(String name, String phoneNumber) {
    contacts.put(name, phoneNumber);
}
```

## Searching for Contacts

To search for a contact in the phonebook, we can use the `get()` method of `HashMap` by providing the name of the contact as the key.

```java
public String searchContact(String name) {
    return contacts.get(name);
}
```

The above method returns the phone number associated with the given name, or `null` if the contact does not exist in the phonebook.

## Updating Contacts

To update a contact's phone number in the phonebook, we can simply reassign the value associated with the given name.

```java
public void updateContact(String name, String newPhoneNumber) {
    contacts.put(name, newPhoneNumber);
}
```

## Removing Contacts

To remove a contact from the phonebook, we can use the `remove()` method of `HashMap` by providing the name of the contact as the key.

```java
public void removeContact(String name) {
    contacts.remove(name);
}
```

## Conclusion

In this blog post, we have learned how to implement a phonebook using the `HashMap` data structure in Java. We explored adding, searching, updating, and removing contacts from the phonebook. Using `HashMap` provides an efficient way to manage a phonebook with constant time complexity for most operations.

Make sure to check out the official [Java HashMap documentation](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/HashMap.html) for more information and advanced usage.

Happy coding! #Java #HashMap