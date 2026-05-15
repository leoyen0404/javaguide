# Appendices

## Appendix A: Development tools

- JDK 11 or newer for compiling and running examples.
- IDE such as IntelliJ IDEA, Eclipse, VS Code, or NetBeans.
- Build tool such as Maven or Gradle for dependencies and test execution.
- Git for version control.
- JDK tools such as `javac`, `java`, `jar`, `javadoc`, `javap`, `jcmd`, and `jstack`.

## Appendix B: Standard project layout

```text
project/
  pom.xml or build.gradle
  src/main/java
  src/main/resources
  src/test/java
  src/test/resources
```

## Appendix C: Java version awareness

This guide targets Java SE 11. If you use newer features such as records, sealed classes, pattern matching, switch expressions, or virtual threads, label them clearly and configure your build accordingly.

## Appendix D: Troubleshooting checklist

- Does the code compile with the intended JDK?
- Are classpath or module path entries correct?
- Are resources closed?
- Are dependencies present at runtime?
- Are tests order-independent?
- Is the failure deterministic or timing-dependent?

## Appendix E: Glossary

- **API:** A public contract for using code.
- **Bytecode:** JVM instruction format compiled from Java source.
- **Classpath:** Runtime/search path for classes and resources.
- **Heap:** JVM memory area for objects.
- **Immutability:** Object state cannot change after construction.
- **JIT:** Just-in-time compiler that optimizes hot bytecode.
- **Module:** Named unit declaring dependencies and exported packages.
