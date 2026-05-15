# Reflection

## Overview

Reflection lets code inspect and sometimes modify classes, fields, constructors, methods, annotations, and generic metadata at runtime. It is powerful but should be used carefully because it weakens compile-time guarantees.

## Inspecting classes

```java
Class<?> type = String.class;
System.out.println(type.getName());
for (Method method : type.getDeclaredMethods()) {
    System.out.println(method.getName());
}
```

## Creating instances and invoking methods

```java
Constructor<Person> ctor = Person.class.getConstructor(String.class);
Person person = ctor.newInstance("Ada");
Method greet = Person.class.getMethod("greet");
String message = (String) greet.invoke(person);
```

Reflective calls wrap target exceptions in `InvocationTargetException`; inspect the cause to understand the real failure.

## Access and modules

Reflection respects access checks unless access is suppressed. In modular applications, strong encapsulation can also block reflective access unless packages are opened.

## Use cases

Reflection is appropriate for:

- Frameworks that instantiate application classes.
- Test utilities and serialization libraries.
- Annotation-driven discovery.
- Tools that inspect code structure.

Avoid reflection for ordinary application flow when interfaces, factories, or dependency injection are clearer.

## Performance and safety

Reflective calls are harder for tools and humans to trace. Cache metadata, validate assumptions early, and keep reflective code isolated behind small APIs.

## Exercises

1. Write a utility that prints public method names of a class.
2. Instantiate a class by constructor name and handle all checked exceptions.
3. Explain how reflection interacts with private fields and module boundaries.
