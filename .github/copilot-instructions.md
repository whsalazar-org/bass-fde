# Copilot Instructions for Spring Boot + DB2 Backend Development

This repository uses **Spring Boot** for backend services and **IBM DB2** as the relational database, accessed through **JDBC**-based data access patterns.

## Core engineering expectations

- Prefer **Java + Spring Boot** idioms and established framework conventions over custom infrastructure.
- Use **constructor injection** only. Do not use field injection.
- Keep code organized by clear backend layers:
  - `controller` for HTTP endpoints
  - `service` for business logic
  - `repository` for database access
  - `model` / `domain` / `dto` for data structures
- Favor readable, maintainable code over clever abstractions.
- Keep classes focused and small when possible.

## Database access rules

- Use **parameterized SQL only**. Never build SQL by concatenating user input into query strings.
- Prefer **Spring JdbcTemplate** or **NamedParameterJdbcTemplate** for application data access unless the task explicitly requires lower-level JDBC APIs.
- Isolate SQL inside repository classes. Controllers and services should not contain SQL.
- Use explicit column selection instead of `SELECT *` unless there is a very strong reason not to.
- Be careful with DB2-specific SQL syntax and data types.
- When schema qualification matters, use the correct DB2 schema explicitly.
- Map `ResultSet` rows in dedicated mapper methods or `RowMapper` implementations for reuse and consistency.

## Transactions and error handling

- Put transaction boundaries in the **service layer** unless there is a clear reason otherwise.
- Use Spring transaction management rather than manual transaction handling where possible.
- Fail fast with clear exceptions.
- Do not swallow SQL or persistence exceptions silently.
- Log useful operational context, but never log secrets, passwords, or full credential strings.

## API design expectations

- Use conventional Spring MVC patterns for REST endpoints.
- Validate incoming request payloads using Jakarta Bean Validation where appropriate.
- Return clear HTTP status codes and structured responses.
- Keep controllers thin; business logic belongs in services.

## Configuration and secrets

- Never hardcode database credentials, tokens, or secrets.
- Use Spring configuration via `application.yml`, `application.properties`, environment variables, or secret-management integrations.
- Prefer configuration properties for database connection settings.
- Assume credentials must be redacted in generated examples, logs, and documentation.

## Testing expectations

- Add or update tests whenever introducing or changing behavior.
- Prefer:
  - unit tests for service logic
  - focused integration tests for repository/database behavior
  - controller tests for request/response behavior when appropriate
- If DB2-specific behavior is important, call that out explicitly in tests or comments.
- Mock only at the boundaries where it improves clarity; avoid over-mocking trivial flows.

## Code generation preferences

When generating Spring Boot backend code:

- Prefer a simple, conventional package structure.
- Generate repository methods with clear SQL and explicit parameter binding.
- Prefer DTOs for API boundaries instead of exposing internal persistence models directly.
- Include error handling, validation, and tests when adding new endpoints.
- If a requirement is ambiguous, choose the most maintainable and conventional Spring Boot approach.

## Documentation expectations

When adding docs or examples:

- Show where configuration belongs.
- Mention DB2/JDBC assumptions explicitly.
- Keep setup steps concrete and developer-friendly.
- Prefer copy-pasteable examples that are safe by default.

## Avoid

- Hardcoded credentials
- SQL string concatenation with input values
- Business logic inside controllers
- Database access in controllers
- Field injection
- Over-engineered abstractions for simple CRUD flows
