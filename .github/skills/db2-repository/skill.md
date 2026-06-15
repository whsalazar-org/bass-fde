---
name: DB2 Repository Implementation
description: Implement or update a Spring Boot repository that accesses IBM DB2 using JDBC or JdbcTemplate with safe SQL, clear mapping, and appropriate tests.
---

# DB2 Repository Implementation

Use this skill when working on persistence code for a Spring Boot backend that connects to **IBM DB2** using **JDBC**, **JdbcTemplate**, or **NamedParameterJdbcTemplate**.

## Goal

Create or modify database access code that is:

- safe
- idiomatic for Spring Boot
- easy to maintain
- explicit about SQL and mapping behavior
- covered by appropriate tests

## Preferred approach

Unless the task explicitly requires raw JDBC, prefer:

- `JdbcTemplate` for straightforward positional-parameter queries
- `NamedParameterJdbcTemplate` when named parameters improve readability
- reusable `RowMapper` implementations or dedicated mapping methods

## Implementation checklist

When implementing a repository:

1. Identify the domain object or DTO being loaded/saved.
2. Determine whether the repository should:
   - fetch one record
   - fetch many records
   - insert
   - update
   - delete
   - perform pagination or filtering
3. Write explicit SQL with named or positional parameters.
4. Avoid `SELECT *`; select only required columns.
5. Map DB2 result columns deliberately and consistently.
6. Keep SQL and mapping logic inside the repository layer.
7. Return types that fit the use case clearly:
   - single object / optional object
   - list
   - update count
   - generated key or identifier if needed
8. Handle empty-result behavior intentionally.
9. Add or update tests.

## DB2-specific guidance

Be careful with:

- schema-qualified table names when required
- DB2 date/time/timestamp handling
- `CHAR` vs `VARCHAR` behavior
- numeric conversions
- DB2 pagination syntax if needed in the target environment
- null handling from JDBC result sets

If the DB2 environment/version is unclear, prefer the most conservative and explicit SQL possible.

## SQL safety rules

- Always use parameter binding.
- Never concatenate user input into SQL.
- Never place request data directly into query strings.
- Keep dynamic SQL limited and structured; if needed, assemble only trusted SQL fragments and still bind values separately.

## Repository structure guidance

A typical repository implementation should include:

- a repository class under a `repository` package
- constructor injection for `JdbcTemplate` or `NamedParameterJdbcTemplate`
- SQL statements as private constants or clearly scoped strings
- one or more row-mapping helpers
- focused public methods named by behavior

Example method categories:

- `findById(...)`
- `findByExternalId(...)`
- `findAllByStatus(...)`
- `create(...)`
- `update(...)`
- `deleteById(...)`

## Service interaction guidance

Repository classes should:

- focus only on persistence concerns
- not contain HTTP concerns
- not contain controller-specific response shaping
- not own cross-step business workflows that belong in services

## Testing guidance

Add tests appropriate to the level of change:

### For repository logic
Prefer integration-style tests when practical, especially when:

- SQL is non-trivial
- mapping behavior is important
- DB2-specific behavior matters

### At minimum validate
- correct parameter binding
- correct row mapping
- empty-result handling
- update/insert behavior
- null/value conversion behavior where relevant

## Output expectations

When using this skill, produce:

- the repository code
- any needed mapper/helper code
- any required configuration adjustments
- tests
- brief notes on DB2 assumptions if they affect implementation

## Avoid

- putting SQL in controllers or services
- exposing raw `ResultSet` handling outside the repository
- ambiguous column mapping
- `SELECT *`
- unsafe string-built SQL
- hidden transactional side effects
