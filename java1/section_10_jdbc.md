# JDBC

## Overview

JDBC is Java's standard API for relational database access. It provides connections, statements, prepared statements, result sets, transactions, and metadata.

## Connections

Use a connection pool in real applications. The raw `DriverManager` style is useful for small examples.

```java
try (Connection connection = DriverManager.getConnection(url, user, password)) {
    System.out.println(connection.getMetaData().getDatabaseProductName());
}
```

## Prepared statements

Prepared statements prevent SQL injection and let the database reuse execution plans.

```java
String sql = "select id, email from users where id = ?";
try (PreparedStatement statement = connection.prepareStatement(sql)) {
    statement.setLong(1, userId);
    try (ResultSet rs = statement.executeQuery()) {
        if (rs.next()) {
            return new User(rs.getLong("id"), rs.getString("email"));
        }
        return null;
    }
}
```

Never concatenate untrusted input into SQL.

## Transactions

```java
connection.setAutoCommit(false);
try {
    debit(connection, from, amount);
    credit(connection, to, amount);
    connection.commit();
} catch (SQLException e) {
    connection.rollback();
    throw e;
} finally {
    connection.setAutoCommit(true);
}
```

Keep transactions short and define isolation requirements intentionally.

## Result mapping

Map database rows to domain objects at the boundary. Keep SQL column names explicit instead of relying on `select *`.

## Resource management

`Connection`, `Statement`, and `ResultSet` must be closed. Try-with-resources is the standard approach.

## Exercises

1. Implement a repository method using `PreparedStatement`.
2. Add transaction handling around two related updates.
3. Explain how connection pooling changes application architecture.
