---
name: Spring CRUD Endpoint
description: Add or update a Spring Boot REST endpoint with controller, service, DTOs, validation, persistence integration, and tests using the repository's established backend conventions.
---

# Spring CRUD Endpoint

Use this skill when implementing or modifying a **Spring Boot REST API endpoint** for create, read, update, or delete operations.

## Goal

Deliver a complete backend slice that is:

- idiomatic for Spring Boot
- aligned with repository conventions
- properly layered
- validated at the API boundary
- tested appropriately
- ready to connect to repository/database logic

## Default architecture

Unless the repository already uses a different established pattern, organize changes across these layers:

- `controller` for HTTP request/response handling
- `service` for business logic and orchestration
- `repository` for persistence access
- `dto` for API request/response payloads
- `model` or `domain` for internal data structures as needed

## Endpoint design rules

When adding or changing an endpoint:

- choose conventional REST naming and HTTP verbs
- keep controllers thin
- place business logic in services
- delegate persistence to repositories
- validate incoming payloads at the boundary
- return clear status codes and predictable response shapes

## Typical mappings

Use conventional patterns unless the repo already defines alternatives:

- `POST /resources` → create
- `GET /resources/{id}` → fetch by id
- `GET /resources` → list/filter
- `PUT /resources/{id}` → replace/update
- `PATCH /resources/{id}` → partial update
- `DELETE /resources/{id}` → delete

## Request/response guidance

Prefer explicit DTOs for API contracts.

### Request DTOs
Use request DTOs to:

- validate required fields
- constrain input shape
- separate external API contracts from persistence models

### Response DTOs
Use response DTOs to:

- return only intended fields
- avoid leaking internal persistence concerns
- keep responses stable over time

## Validation guidance

Use Jakarta Bean Validation where appropriate, such as:

- `@NotNull`
- `@NotBlank`
- `@Size`
- `@Email`
- numeric constraints
- date or format constraints

Validate at the controller boundary using Spring conventions.

## Service-layer guidance

Service methods should:

- express the business use case clearly
- coordinate repository calls
- define transaction boundaries when needed
- enforce domain/business rules
- avoid HTTP-specific concerns

## Repository integration guidance

If persistence is part of the task:

- call existing repository methods where possible
- otherwise add or update repository methods following repo standards
- keep SQL and JDBC concerns out of controllers and services
- use the DB2 repository skill when implementing DB2-backed persistence behavior

## Error handling guidance

Handle common cases intentionally:

- missing resource
- duplicate or conflicting resource
- invalid input
- persistence or downstream failure

Return appropriate HTTP status codes and avoid vague error responses.

## Testing guidance

Update or add tests for the changed behavior.

### Controller tests
Cover things like:

- routing
- request validation
- status codes
- response payload shape

### Service tests
Cover things like:

- business rules
- branching behavior
- repository interaction where meaningful

### Integration tests
Use when endpoint behavior depends on real persistence, serialization, or configuration behavior.

## Implementation checklist

When using this skill:

1. identify the resource and operation
2. define or update request/response DTOs
3. add or update controller method
4. add or update service method
5. integrate repository logic if needed
6. add validation
7. add or update tests
8. verify status codes and response shape
9. document assumptions if they affect consumers

## Output expectations

Produce a complete, reviewable change set that includes:

- endpoint implementation
- DTOs
- service updates
- repository integration if needed
- validation
- tests

## Avoid

- putting business logic in controllers
- returning persistence entities directly as API contracts unless the repo explicitly does that already
- skipping validation for structured input
- mixing SQL or JDBC logic into controllers
- changing endpoint conventions without a clear reason
