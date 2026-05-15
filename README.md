# Java Guide

A structured, practical guide for learning **Java SE 11** from fundamentals through production-ready application design. The project has been reconstructed from a sparse outline into a navigable handbook with topic chapters, examples, practice material, exam review aids, and project guidance.

## Who this guide is for

- New Java developers who need a clear learning path.
- Developers from other languages who want Java SE 11 fluency.
- OCP Java SE 11 candidates who need review checklists and practice questions.
- Teams that want shared references for Java style, testing, security, and design.

## How to use the guide

1. Start with the [main guide index](java1/ultimate_guide.md).
2. Read chapters in order if you are new to Java, or jump directly to a topic from the table below.
3. Compile and run the code snippets locally with JDK 11+.
4. Use the [cheat sheets](java1/cheat_sheets.md), [practice questions](java1/practice_questions.md), and [mock exams](java1/mock_exams.md) after each study block.
5. Build the projects in [real-world examples](java1/real_world_examples.md) and compare them with the [case studies](java1/case_studies.md).

## Guide map

| Phase | Chapters | Goal |
| --- | --- | --- |
| Foundation | [Core Java](java1/section_1_core_java.md), [Java SE 11 Features](java1/section_2_java_se_11_features.md), [Essential APIs](java1/section_3_essential_apis.md) | Write correct basic programs and understand the platform. |
| Everyday Java | [Exception Handling](java1/section_5_exception_handling.md), [I/O](java1/section_6_io_operations.md), [Collections](java1/section_7_collections_framework.md), [Generics](java1/section_8_generics.md), [Lambdas](java1/section_9_lambdas.md) | Build maintainable applications using the standard library. |
| Advanced Java | [Concurrency](java1/section_4_concurrency.md), [JDBC](java1/section_10_jdbc.md), [Annotations](java1/section_11_annotations.md), [Reflection](java1/section_12_reflection.md), [JVM Internals](java1/section_13_jvm_internals.md) | Understand runtime behavior, integration, and advanced language tools. |
| Professional Practice | [JUnit](java1/section_14_unit_testing_with_junit.md), [Security](java1/section_15_security.md), [Design Patterns](java1/section_16_design_patterns.md), [Best Practices](java1/section_17_best_practices.md) | Ship tested, secure, readable, production-quality Java. |

## Repository contents

- `java1/ultimate_guide.md` — main index, learning outcomes, and study plan.
- `java1/section_*.md` — topic chapters with explanations, examples, pitfalls, and exercises.
- `java1/practice_questions.md` and `java1/mock_exams.md` — review questions and exam-style drills.
- `java1/cheat_sheets.md` — compact syntax and API reference.
- `java1/real_world_examples.md` and `java1/case_studies.md` — applied project walkthroughs.
- `java1/reference_material.md`, `java1/apis_documentation.md`, and `java1/appendices.md` — supplemental references.

## Local study setup

Install a JDK 11 or newer and verify:

```bash
java --version
javac --version
```

Compile a single-file example:

```bash
javac Example.java
java Example
```

For larger projects, use Maven or Gradle and keep source code in the standard layout:

```text
src/main/java
src/test/java
```

## Contribution standards

When adding content, prefer:

- Java SE 11 compatible examples unless a newer version is explicitly labeled.
- Small runnable snippets over pseudocode.
- Clear distinction between language rules, library conventions, and best practices.
- Exercises with expected reasoning, not only final answers.
