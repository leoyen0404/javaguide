# Unit Testing with JUnit

## Overview

Unit tests verify small units of behavior quickly and deterministically. Java SE does not include JUnit, but JUnit 5 is the modern standard for Java unit testing.

## Test structure

A good unit test follows Arrange, Act, Assert.

```java
class CalculatorTest {
    @Test
    void addsTwoNumbers() {
        Calculator calculator = new Calculator();

        int result = calculator.add(2, 3);

        assertEquals(5, result);
    }
}
```

## Naming

Use descriptive names that explain behavior:

- `withdrawRejectsNegativeAmount`
- `parserReturnsEmptyWhenInputIsBlank`
- `repositoryUsesPreparedStatementParameters`

## Assertions

JUnit 5 assertions include `assertEquals`, `assertTrue`, `assertThrows`, `assertAll`, and timeout assertions.

```java
IllegalArgumentException ex = assertThrows(IllegalArgumentException.class,
        () -> account.deposit(-1));
assertEquals("amount must be positive", ex.getMessage());
```

## Test doubles

Use fakes, stubs, and mocks to isolate behavior when real dependencies are slow, nondeterministic, or external. Avoid over-mocking value objects and simple data structures.

## Parameterized tests

Parameterized tests reduce duplication for input/output tables.

```java
@ParameterizedTest
@CsvSource({"1,2,3", "2,3,5"})
void adds(int a, int b, int expected) {
    assertEquals(expected, new Calculator().add(a, b));
}
```

## Test quality

- Tests should be independent and order-insensitive.
- Avoid sleeping in tests; control time with injected clocks.
- Use temporary directories for file-system tests.
- Keep unit tests fast and push full-stack checks into integration tests.

## Exercises

1. Write tests for a validation class using `assertThrows`.
2. Refactor a time-dependent class to accept `Clock`.
3. Create a parameterized test for a string normalizer.
