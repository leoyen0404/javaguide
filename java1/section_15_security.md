# Security

## Overview

Secure Java code validates inputs, protects secrets, uses cryptography correctly, controls dependencies, and fails safely. Security is a design property, not a final checklist.

## Input validation

Validate untrusted input at boundaries: HTTP controllers, CLI arguments, files, queues, and database rows from external systems.

```java
static String requireSafeUsername(String username) {
    if (username == null || !username.matches("[A-Za-z0-9_]{3,30}")) {
        throw new IllegalArgumentException("invalid username");
    }
    return username;
}
```

## SQL injection prevention

Use prepared statements, never string concatenation with untrusted values.

```java
PreparedStatement ps = connection.prepareStatement("select * from users where email = ?");
ps.setString(1, email);
```

## Secrets

Do not hard-code credentials, tokens, or private keys. Load secrets from environment-specific secret stores and keep them out of logs, stack traces, and version control.

## Cryptography

Use standard providers and high-level constructions. Avoid inventing cryptographic algorithms.

Guidelines:

- Use `SecureRandom` for security-sensitive randomness.
- Use password hashing algorithms designed for passwords, supplied by vetted libraries or platform services.
- Use authenticated encryption modes when encrypting data.
- Manage keys separately from encrypted data.

## Deserialization

Do not deserialize untrusted Java object streams. Prefer explicit data formats and schema validation.

## File and path safety

Normalize and validate user-provided paths before file access to prevent path traversal.

```java
Path base = Path.of("uploads").toAbsolutePath().normalize();
Path target = base.resolve(userInput).normalize();
if (!target.startsWith(base)) {
    throw new SecurityException("path traversal rejected");
}
```

## Dependency hygiene

Keep dependencies updated, review transitive dependencies, and use vulnerability scanning in CI. Remove unused libraries to shrink attack surface.

## Exercises

1. Refactor unsafe SQL into a prepared statement.
2. Add path traversal protection to a file download method.
3. Identify what should and should not appear in security logs.
