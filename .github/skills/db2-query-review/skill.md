---
name: DB2 Query Review
description: Review and improve DB2 SQL and JDBC-based persistence code for safety, correctness, maintainability, performance, and alignment with Spring Boot repository conventions.
---

# DB2 Query Review

Use this skill when reviewing or refining **DB2 SQL**, **JdbcTemplate code**, **NamedParameterJdbcTemplate code**, or lower-level **JDBC persistence logic** in a Spring Boot backend.

## Goal

Evaluate database access code and improve it for:

- SQL safety
- correctness
- readability
- maintainability
- DB2 compatibility
- operational robustness

## Primary review areas

When using this skill, inspect the persistence code for the following:

### 1. SQL safety
- All user-controlled values must be passed as bound parameters.
- Never concatenate request or UI input directly into SQL.
- Dynamic SQL must be tightly controlled and assembled only from trusted fragments.
- Avoid hidden injection risks in sorting, filtering, or pagination logic.

### 2. Query clarity
- Prefer explicit column lists over `SELECT *`.
- Keep SQL readable and consistently formatted.
- Use clear aliases only when they improve readability.
- Keep repository methods focused on one query purpose.

### 3. Mapping correctness
- Check that selected columns match row-mapping code exactly.
- Watch for fragile positional assumptions.
- Validate null handling carefully.
- Verify type conversions for DB2 numeric, character, date, and timestamp fields.

### 4. DB2-specific considerations
Review for likely DB2 issues such as:

- schema qualification requirements
- `CHAR` padding behavior
- `VARCHAR` and trimming assumptions
- timestamp/date conversion behavior
- decimal/numeric conversion issues
- pagination syntax compatibility
- case sensitivity or naming assumptions
- default schema reliance

If the exact DB2 version/platform is unknown, prefer conservative and explicit recommendations.

### 5. Spring data access quality
- Prefer `JdbcTemplate` or `NamedParameterJdbcTemplate` for typical repository logic.
- Keep raw JDBC boilerplate to cases where it is truly necessary.
- Use reusable `RowMapper` patterns when repeated mapping exists.
- Keep transaction boundaries out of the repository unless there is a clear reason otherwise.

### 6. Error handling and observability
- Avoid swallowing database exceptions.
- Surface meaningful context without leaking credentials or secrets.
- Ensure logging is useful but safe.
- Flag places where failures will be hard to diagnose in production.

### 7. Performance and maintainability
Check for:

- unnecessary repeated queries
- over-fetching columns
- unclear filtering behavior
- large result set risks
- query duplication across repositories
- difficult-to-test SQL construction

Do not over-optimize prematurely, but call out obvious risks.

## Review output format

When using this skill, provide review feedback in this order:

1. **What is good**
   - note safe or well-structured parts first
2. **Issues found**
   - list concrete problems
3. **Recommended changes**
   - propose specific improvements
4. **Revised implementation**
   - if asked or appropriate, provide improved SQL/code
5. **DB2 assumptions or unknowns**
   - identify anything that depends on schema/version/platform behavior

## Suggested fixes

Typical improvements include:

- converting string-built SQL to parameterized SQL
- replacing `SELECT *` with explicit columns
- extracting reusable row mappers
- clarifying null handling
- moving business logic out of repository methods
- splitting overly broad repository methods into focused ones
- improving method names to match query behavior

## Testing guidance

If query behavior changes, recommend or add tests that verify:

- parameter binding behavior
- empty and non-empty results
- null handling
- date/time mapping
- update counts
- DB2-specific edge cases if relevant

## Avoid

- generic review comments with no concrete action
- recommending patterns inconsistent with the repository's existing Spring Boot conventions
- speculative performance claims without visible evidence
- changing business behavior unless the task explicitly asks for it
