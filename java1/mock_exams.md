# Mock Exams

These mock exams are designed for review, not as a guarantee of certification readiness. Use a timer, do not look up answers during the attempt, and review every missed question by returning to the relevant chapter.

## Format

- **Mini exam:** 20 questions in 30 minutes.
- **Full review set:** 60 questions in 120 minutes.
- **Passing target:** 75% for first pass, 85% before moving on.

## Mini exam A

1. Which statement about `String` is true?
   - A. It is mutable.
   - B. It is immutable.
   - C. It cannot be used as a map key.
   - D. It is a primitive type.
2. Which collection rejects duplicate elements by contract?
   - A. `List`
   - B. `Set`
   - C. `Queue`
   - D. `Deque`
3. What does try-with-resources require?
   - A. Resource implements `AutoCloseable`.
   - B. Resource is static.
   - C. Resource is serializable.
   - D. Resource is synchronized.
4. Which interface is a functional interface?
   - A. One with any number of default methods and exactly one abstract method.
   - B. One with two abstract methods.
   - C. One with no methods only.
   - D. One that extends `Object`.
5. Which API should be used for new date/time code?
   - A. `java.util.Date`
   - B. `java.util.Calendar`
   - C. `java.time`
   - D. `java.sql.Date` for all date values.
6. What prevents SQL injection in JDBC?
   - A. `Statement` with concatenation.
   - B. `PreparedStatement` with parameters.
   - C. Catching `SQLException`.
   - D. Using `select *`.
7. Which keyword prevents subclassing?
   - A. `static`
   - B. `volatile`
   - C. `final`
   - D. `transient`
8. Which operation is terminal in a stream?
   - A. `filter`
   - B. `map`
   - C. `sorted`
   - D. `collect`
9. Which class is appropriate for atomic counters?
   - A. `AtomicInteger`
   - B. `StringBuilder`
   - C. `HashMap`
   - D. `Optional`
10. What is the safest default for class fields?
    - A. `public`
    - B. package-private mutable fields
    - C. `private`, preferably `final` when possible
    - D. `protected` everywhere

## Mini exam A answers

1. B
2. B
3. A
4. A
5. C
6. B
7. C
8. D
9. A
10. C

## Review method

For each wrong answer:

1. Identify the chapter.
2. Explain why the correct answer is correct.
3. Explain why each distractor is wrong.
4. Write a small code sample proving the rule.
