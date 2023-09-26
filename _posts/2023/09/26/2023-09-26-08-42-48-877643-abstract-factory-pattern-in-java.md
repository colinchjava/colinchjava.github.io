---
layout: post
title: "Abstract factory pattern in Java"
description: " "
date: 2023-09-26
tags: [java, designpattern]
comments: true
share: true
---

The Abstract Factory Pattern is a creational design pattern that provides an interface for creating families of related or dependent objects without specifying their concrete classes. It allows the creation of objects that follow a common interface but belong to different classes.

## Example Scenario

Let's consider a scenario where we have a GUI application with different themes such as LightTheme and DarkTheme. Each theme consists of multiple components like buttons, labels, and text fields. We want to ensure that all the components created follow a common interface, but their actual implementation differs based on the theme selected.

## Implementation

```java
// Abstract component interface
interface Component {
    void render();
}

// Concrete component implementations
class LightButton implements Component {
    @Override
    public void render() {
        System.out.println("Rendering light theme button");
    }
}

class DarkButton implements Component {
    @Override
    public void render() {
        System.out.println("Rendering dark theme button");
    }
}

class LightLabel implements Component {
    @Override
    public void render() {
        System.out.println("Rendering light theme label");
    }
}

class DarkLabel implements Component {
    @Override
    public void render() {
        System.out.println("Rendering dark theme label");
    }
}

// Abstract factory interface
interface ThemeFactory {
    Component createButton();
    Component createLabel();
}

// Concrete factory implementations
class LightThemeFactory implements ThemeFactory {
    @Override
    public Component createButton() {
        return new LightButton();
    }

    @Override
    public Component createLabel() {
        return new LightLabel();
    }
}

class DarkThemeFactory implements ThemeFactory {
    @Override
    public Component createButton() {
        return new DarkButton();
    }

    @Override
    public Component createLabel() {
        return new DarkLabel();
    }
}

// Client class for creating components using the abstract factory
class ThemeClient {
    private Component button;
    private Component label;

    public ThemeClient(ThemeFactory themeFactory) {
        button = themeFactory.createButton();
        label = themeFactory.createLabel();
    }

    public void renderComponents() {
        button.render();
        label.render();
    }
}

// Usage example
public class Main {
    public static void main(String[] args) {
        ThemeFactory lightThemeFactory = new LightThemeFactory();
        ThemeFactory darkThemeFactory = new DarkThemeFactory();

        ThemeClient lightThemeClient = new ThemeClient(lightThemeFactory);
        ThemeClient darkThemeClient = new ThemeClient(darkThemeFactory);

        lightThemeClient.renderComponents();
        darkThemeClient.renderComponents();
    }
}
```

## Explanation

In the code snippet above, we have an abstract `Component` interface that defines the contract for all components in our GUI application. We then have concrete implementations of `Button` and `Label` for both the Light and Dark themes.

The `ThemeFactory` interface defines the abstract factory contract with methods for creating buttons and labels. We then have concrete implementations of the factory for each theme.

The `ThemeClient` class serves as the client that creates components using the abstract factory. It takes a `ThemeFactory` as a parameter and can render the components created by calling their `render` methods.

In the `Main` class, we create instances of `ThemeFactory` for the Light and Dark themes, and then create `ThemeClient` instances using these factories. Finally, we call the `renderComponents` method to render the components based on the respective themes.

## Conclusion

The Abstract Factory Pattern provides a way to create families of related objects without having to specify their concrete classes. It enables flexibility and extensibility in creating objects that adhere to a common interface but have different implementations. By using this pattern, we can easily switch between different themes in our GUI application without making substantial changes to the code.

#java #designpattern