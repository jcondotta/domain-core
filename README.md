# Domain Core

Framework-independent Java building blocks for domain models. This project is an initial extraction of `domain-core` from the banking-system monorepo. It preserves the existing `com.jcondotta.domain` package names and API while establishing an independent Maven build.

## Contents

- Entity, aggregate root, and domain collection base types.
- Typed entity and aggregate IDs, plus event IDs.
- Domain event metadata and event contracts.
- Common domain exceptions and precondition validation.
- Aggregate repository port.

The library has no production dependencies on Spring, persistence frameworks, or banking-specific modules. Test dependencies are JUnit Jupiter and AssertJ.

## Build

Requires JDK 25 and Maven 3.9 or later.

```sh
mvn clean verify
```

## Maven coordinates

```xml
<dependency>
    <groupId>io.github.jcondotta</groupId>
    <artifactId>domain-core</artifactId>
    <version>0.1.0-SNAPSHOT</version>
</dependency>
```

This initial copy is not yet published and the banking-system project has not migrated to these coordinates. Package names and public APIs are intentionally unchanged for the extraction review.
