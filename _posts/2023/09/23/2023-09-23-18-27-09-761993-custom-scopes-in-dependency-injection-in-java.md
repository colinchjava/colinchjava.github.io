---
layout: post
title: "Custom scopes in Dependency Injection in Java."
description: " "
date: 2023-09-23
tags: [DependencyInjection]
comments: true
share: true
---

Dependency Injection is a powerful design pattern that promotes loose coupling and enhances testability and maintainability in Java applications. In Dependency Injection, the control of creating and managing objects is shifted to a framework, typically through the use of Inversion of Control (IoC) containers.

One of the key aspects of Dependency Injection is managing the lifecycle of objects and controlling their scope. While IoC containers usually provide default scopes like Singleton and Prototype, there might be cases where we need to define our own custom scopes to meet specific requirements.

In this blog post, we will explore how to create and use custom scopes in Dependency Injection in Java. Let's dive in!

## Understanding Scopes in Dependency Injection

Scopes define the lifecycle of an object managed by the IoC container. They define how long an instance of a particular object should exist and how it should be shared among different components.

The commonly used scopes in Dependency Injection are:

1. **Singleton**: In this scope, a single instance of the object is created and shared across all components requesting it.

2. **Prototype**: In this scope, a new instance of the object is created each time it is requested.

## Creating Custom Scopes

To create a custom scope in Dependency Injection, we need to define a scope annotation and a corresponding scope implementation.

First, let's define the scope annotation:

```java
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;

@Retention(RetentionPolicy.RUNTIME)
public @interface CustomScope {
}
```

The `@Retention` annotation is used to ensure that the custom scope annotation is accessible at runtime.

Next, let's create the scope implementation:

```java
import org.springframework.beans.factory.ObjectFactory;
import org.springframework.beans.factory.config.Scope;

import java.util.HashMap;
import java.util.Map;

public class CustomScopeImplementation implements Scope {

    private final Map<String, Object> scopedObjects = new HashMap<>();
    private final Map<String, Runnable> destructionCallbacks = new HashMap<>();

    @Override
    public Object get(String name, ObjectFactory<?> objectFactory) {
        if (!scopedObjects.containsKey(name)) {
            scopedObjects.put(name, objectFactory.getObject());
        }
        return scopedObjects.get(name);
    }

    @Override
    public Object remove(String name) {
        destructionCallbacks.remove(name);
        return scopedObjects.remove(name);
    }

    @Override
    public void registerDestructionCallback(String name, Runnable callback) {
        destructionCallbacks.put(name, callback);
    }

    @Override
    public Object resolveContextualObject(String key) {
        return null;
    }

    @Override
    public String getConversationId() {
        return null;
    }
}
```

In the custom scope implementation, we maintain two maps - `scopedObjects` to store the created instances of objects and `destructionCallbacks` to register callbacks when an object is removed from the scope.

## Using Custom Scopes

To use the custom scope in the application, we need to register the custom scope annotation and scope implementation with the IoC container.

```java
import org.springframework.context.annotation.ScopeMetadata;
import org.springframework.context.annotation.ScopeMetadataResolver;
import org.springframework.core.annotation.AnnotationAttributes;
import org.springframework.core.annotation.MergedAnnotation;
import org.springframework.core.annotation.MergedAnnotations;
import org.springframework.util.Assert;

import java.lang.annotation.Annotation;

public class CustomScopeMetadataResolver implements ScopeMetadataResolver {

    @Override
    public ScopeMetadata resolveScopeMetadata(BeanDefinition definition) {
        Assert.notNull(definition, "Bean definition must not be null");
        ScopeMetadata scopeMetadata = new ScopeMetadata();
        MergedAnnotations mergedAnnotations = MergedAnnotations.from(definition.getBeanClass(), MergedAnnotations.SearchStrategy.TYPE_HIERARCHY);
        MergedAnnotation<Annotation> mergedAnnotation = mergedAnnotations.get(CustomScope.class);
        if (mergedAnnotation.isPresent()) {
            AnnotationAttributes attributes = mergedAnnotation.asAnnotationAttributes();
            scopeMetadata.setScopeName(attributes.getString("value"));
        } else {
            scopeMetadata.setScopeName(BeanDefinition.SCOPE_SINGLETON);
        }
        return scopeMetadata;
    }
}
```

In this custom scope metadata resolver, we check if the custom scope annotation is present on the bean definition. If present, we set the scope name from the annotation attributes. If not present, we default to the Singleton scope.

Finally, wire everything together in the Spring configuration file:

```xml
<bean class="com.example.CustomScopeImplementation" scope="custom"/>
<bean class="com.example.CustomScopeMetadataResolver"/>
```

In the above snippet, we register our custom scope implementation and the custom scope metadata resolver.

## Conclusion

In this blog post, we explored how to create and use custom scopes in Dependency Injection in Java. Custom scopes allow you to define more granular control over the lifecycle and sharing of objects managed by the IoC container.

By creating custom scopes, you can better align your application's object lifecycle with your specific requirements. This enhances code modularity and maintainability in complex Java applications.

#Java #DependencyInjection #CustomScopes