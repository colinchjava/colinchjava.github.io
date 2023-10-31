---
layout: post
title: "Radio buttons in Java AWT"
description: " "
date: 2023-10-31
tags: []
comments: true
share: true
---

In this blog post, we will explore how to use radio buttons in Java AWT (Abstract Window Toolkit) to create interactive user interfaces. Radio buttons are a type of button that allows users to select only one option from a group of options.

## Table of Contents
1. [Introduction to Java AWT](#introduction-to-java-awt)
2. [Creating Radio Buttons](#creating-radio-buttons)
3. [Handling Radio Button Events](#handling-radio-button-events)
4. [Conclusion](#conclusion)
5. [References](#references)

## Introduction to Java AWT

Java AWT is a GUI toolkit included in the Java Development Kit (JDK) for creating desktop applications. It provides a set of classes and components to build user interfaces that are platform-independent.

## Creating Radio Buttons

To create radio buttons in Java AWT, we need to use the `Checkbox` class with the `CheckboxGroup` class. The `CheckboxGroup` class is used to group multiple radio buttons together, so that only one can be selected at a time.

Here's an example code snippet that demonstrates how to create radio buttons:

```java
import java.awt.*;
import java.awt.event.*;

public class RadioButtonExample extends Frame {
    private CheckboxGroup checkboxGroup;

    public RadioButtonExample() {
        setTitle("Radio Button Example");
        setSize(300, 200);

        checkboxGroup = new CheckboxGroup();

        Checkbox radioBtn1 = new Checkbox("Option 1", checkboxGroup, false);
        Checkbox radioBtn2 = new Checkbox("Option 2", checkboxGroup, false);
        Checkbox radioBtn3 = new Checkbox("Option 3", checkboxGroup, false);

        setLayout(new FlowLayout());

        add(radioBtn1);
        add(radioBtn2);
        add(radioBtn3);

        setVisible(true);
    }

    public static void main(String[] args) {
        new RadioButtonExample();
    }
}
```

In the above code, we create three radio buttons (`radioBtn1`, `radioBtn2`, and `radioBtn3`) and assign them to the `CheckboxGroup` (`checkboxGroup`). The boolean parameter in the `Checkbox` constructor determines whether the radio button is initially selected or not.

## Handling Radio Button Events

To handle radio button events, we can use the `ItemListener` interface, which is implemented by the `Checkbox` class. The `ItemListener` interface provides the `itemStateChanged` method, which is called when the state of the radio button changes.

Here's an example code snippet that demonstrates how to handle radio button events:

```java
import java.awt.*;
import java.awt.event.*;

public class RadioButtonExample extends Frame implements ItemListener {
    private CheckboxGroup checkboxGroup;

    public RadioButtonExample() {
        setTitle("Radio Button Example");
        setSize(300, 200);

        checkboxGroup = new CheckboxGroup();

        Checkbox radioBtn1 = new Checkbox("Option 1", checkboxGroup, false);
        Checkbox radioBtn2 = new Checkbox("Option 2", checkboxGroup, false);
        Checkbox radioBtn3 = new Checkbox("Option 3", checkboxGroup, false);

        radioBtn1.addItemListener(this);
        radioBtn2.addItemListener(this);
        radioBtn3.addItemListener(this);

        setLayout(new FlowLayout());

        add(radioBtn1);
        add(radioBtn2);
        add(radioBtn3);

        setVisible(true);
    }

    public void itemStateChanged(ItemEvent e) {
        Checkbox selectedRadioBtn = (Checkbox) e.getItemSelectable();
        String option = selectedRadioBtn.getLabel();
        System.out.println("Selected option: " + option);
    }

    public static void main(String[] args) {
        new RadioButtonExample();
    }
}
```

In the above code, we implement the `ItemListener` interface and override the `itemStateChanged` method to perform custom actions when the radio button selection changes. Here, we simply print the selected option to the console.

## Conclusion

In this blog post, we explored how to use radio buttons in Java AWT to create interactive user interfaces. We learned how to create radio buttons using the `Checkbox` and `CheckboxGroup` classes, and how to handle radio button events using the `ItemListener` interface.

Using radio buttons can enhance the user experience and provide an intuitive way for users to make selections from a group of options.

## References

- [Java AWT Documentation](https://docs.oracle.com/javase/8/docs/api/java/awt/package-summary.html)
- [Java Checkbox Documentation](https://docs.oracle.com/javase/8/docs/api/java/awt/Checkbox.html)
- [Java CheckboxGroup Documentation](https://docs.oracle.com/javase/8/docs/api/java/awt/CheckboxGroup.html)