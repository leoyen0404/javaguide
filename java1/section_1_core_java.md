# Core Java Concepts

## Big picture

Core Java is the set of language rules that every other topic depends on: types, expressions, control flow, methods, classes, objects, packages, modules, and the rules for inheritance and access. Learn these rules until you can predict compiler behavior without running the program.

## Types and variables

Java is statically typed: every expression has a compile-time type. Primitive values store raw values; reference variables store references to objects.

| Category | Examples | Notes |
| --- | --- | --- |
| Integer primitives | `byte`, `short`, `int`, `long` | Integer literals are `int` unless suffixed with `L` or assignable by constant narrowing. |
| Floating primitives | `float`, `double` | Floating literals are `double` unless suffixed with `F`. Use `BigDecimal` for money. |
| Other primitives | `char`, `boolean` | `boolean` is not numeric and cannot be converted to `int`. |
| References | `String`, arrays, classes, interfaces, enums | Can be `null` unless guarded by design or validation. |

```java
int count = 42;
long population = 7_800_000_000L;
String name = "Duke";
var localName = name.toUpperCase(); // Java 10+, local variables only
```

## Operators and expressions

Java evaluates expressions using precedence, associativity, and numeric promotion rules. Prefer parentheses when intent might be unclear.

```java
int x = 10;
int y = 3;
System.out.println(x / y);      // 3, integer division
System.out.println(x / 3.0);    // 3.333..., double division
System.out.println(++x);        // increment then read
System.out.println(x++);        // read then increment
```

Important rules:

- `==` compares primitive values or reference identity; use `.equals` for logical object equality.
- `&&` and `||` short-circuit; `&` and `|` also work on booleans but evaluate both sides.
- String concatenation with `+` converts operands left-to-right.

## Control flow

Use `if`, `switch`, loops, `break`, `continue`, and `return` to control execution. Keep branch bodies small and extract methods when nesting becomes hard to read.

```java
for (int i = 1; i <= 3; i++) {
    if (i % 2 == 0) {
        System.out.println("even " + i);
    } else {
        System.out.println("odd " + i);
    }
}
```

Java SE 11 uses the traditional `switch` statement; switch expressions with `yield` are from later Java versions and should not be used in Java 11-only code.

## Methods

A method signature includes the method name and parameter types, not the return type. Overloading chooses among methods at compile time.

```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}
```

Guidelines:

- Make methods do one thing and name them with verbs.
- Validate public method arguments at the boundary.
- Prefer returning values over mutating hidden state when practical.

## Classes and objects

Classes describe state and behavior. Objects are runtime instances.

```java
public class Account {
    private final String id;
    private long cents;

    public Account(String id, long openingBalanceCents) {
        this.id = id;
        this.cents = openingBalanceCents;
    }

    public void deposit(long amountCents) {
        if (amountCents <= 0) throw new IllegalArgumentException("amount must be positive");
        cents += amountCents;
    }

    public long balanceCents() {
        return cents;
    }
}
```

Encapsulation means callers use behavior instead of directly editing fields. It protects invariants such as "balance changes only through validated operations."

## Inheritance, interfaces, and polymorphism

Inheritance models an "is-a" relationship. Interfaces model capabilities or contracts.

```java
interface Payable {
    long amountDueCents();
}

class Invoice implements Payable {
    private final long amount;

    Invoice(long amount) {
        this.amount = amount;
    }

    @Override
    public long amountDueCents() {
        return amount;
    }
}
```

Use inheritance sparingly. Composition is often safer because it avoids fragile base-class coupling.

## Packages and modules

Packages organize classes and provide a namespace. Java modules, introduced in Java 9, declare explicit dependencies and exported packages in `module-info.java`.

```java
module com.example.billing {
    exports com.example.billing.api;
    requires java.sql;
}
```

## Common pitfalls

- Confusing reference equality (`==`) with logical equality (`equals`).
- Using floating point for currency.
- Creating mutable public fields.
- Catching broad exceptions instead of validating specific inputs.
- Treating inheritance as a code-sharing tool rather than a substitutability contract.

## Exercises

1. Create a `Money` class that stores cents as `long`, validates input, and formats dollars.
2. Write an interface `DiscountPolicy` and two implementations.
3. Demonstrate method overloading with `int`, `long`, and `Integer` arguments; explain which overload is selected.
