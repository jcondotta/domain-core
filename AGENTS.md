# Repository Guidelines

This is a standalone Java 25 Maven library extracted from the banking-system monorepo.

- `src/main/java/com/jcondotta/domain/`: framework-independent domain primitives, IDs, events, exceptions, validation, and repository contracts.
- `src/test/java/com/jcondotta/domain/`: unit tests matching production packages.
- Root `pom.xml`: independent artifact coordinates, test dependencies, and build plugin versions.

Keep production code free of Spring, persistence, messaging, transport, and banking-context dependencies. Preserve the existing `com.jcondotta.domain` packages and public API during this extraction. Do not add abstractions or dependencies without a demonstrated need.

Use Java 25, standard Java formatting, JUnit Jupiter, and AssertJ. Keep tests focused on observable behavior and domain invariants.

Run `mvn clean verify` from the repository root. Inspect `mvn dependency:tree -Dscope=compile` when production dependencies change.

Treat the production code and tests as evidence of current behavior. Preserve unrelated user changes.
