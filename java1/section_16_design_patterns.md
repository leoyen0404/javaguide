# Design Patterns

## Overview

Design patterns are named solutions to recurring design problems. Use them to communicate and simplify, not to add ceremony. Java's language features and libraries often provide lightweight alternatives.

## Creational patterns

### Factory Method

Encapsulates object creation behind a method.

```java
interface NotificationSender {
    void send(String message);
}

class NotificationSenderFactory {
    NotificationSender create(String channel) {
        switch (channel) {
            case "email": return new EmailSender();
            case "sms": return new SmsSender();
            default: throw new IllegalArgumentException("unknown channel");
        }
    }
}
```

### Builder

Useful for objects with many optional fields and invariants.

## Structural patterns

### Adapter

Converts one interface into another expected by client code. Common when integrating legacy systems or third-party libraries.

### Decorator

Adds behavior around another implementation of the same interface, such as caching, logging, or validation.

## Behavioral patterns

### Strategy

Selects interchangeable behavior at runtime.

```java
interface PricingStrategy {
    long price(Order order);
}
```

### Observer

Notifies listeners about events. Be careful with listener lifecycle to avoid memory leaks.

### Template Method

Defines an algorithm skeleton in a superclass while subclasses customize steps. Prefer composition if subclassing creates tight coupling.

## Pattern selection checklist

- Does the pattern remove duplication or clarify intent?
- Can a simple method, lambda, or interface solve the problem?
- Does the pattern protect a real variation point?
- Will future maintainers understand the abstraction?

## Exercises

1. Implement a strategy for shipping cost calculation.
2. Wrap a repository with a caching decorator.
3. Replace an over-engineered singleton with dependency injection.
