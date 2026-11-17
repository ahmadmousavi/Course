<!--
Sync Impact Report
Version change: uninitialized template -> 1.0.0
Modified principles: template placeholders replaced by evidence-based MyApi principles
Added sections: Architecture and Decisions Requiring Confirmation; Development Workflow and Quality Gates
Removed sections: none; template sections retained and named
Follow-up TODOs: confirm original ratification date; resolve decisions listed below when relevant
-->

# MyApi Constitution

## Core Principles

### I. Evidence-Based Architecture

The default is to extend the existing `MyApi` ASP.NET Core Web API project and its
controller-based request pipeline. A layered or multi-project architecture MUST NOT be
introduced without an explicit decision recorded in the feature plan. New dependencies
MUST be justified by a requirement and recorded in the plan.

### II. Explicit Design Decisions

Spec Kit plans MUST distinguish repository evidence from proposed design choices. Any
unsettled decision that affects architecture, persistence, authentication, or testing MUST
be marked as requiring confirmation; it MUST NOT be silently treated as an approved
convention. Implementation MUST wait for confirmation when the decision materially affects
scope or behavior.

### III. Stable and Described API Behavior

Requirements and plans MUST identify the affected HTTP routes and externally visible
request, response, and authorization behavior. Breaking changes to an existing API
contract MUST be explicitly approved before implementation. New API behavior MUST use the
project's existing ASP.NET Core controller and OpenAPI mechanisms unless an approved plan
specifies otherwise.

### IV. Safe Configuration

Secrets MUST NOT be embedded in source code or committed in configuration files.
Environment-specific settings MUST remain separate from application behavior. A feature
that needs secrets or protected configuration MUST record the required configuration
approach in its plan; this constitution does not prescribe an unobserved secret-management
provider.

### V. Verifiable Changes

Each feature spec MUST have observable acceptance criteria, and its plan MUST state how
those criteria will be verified. For changes to this project,
`dotnet build MyApi/MyApi.csproj` MUST succeed. Tests MUST be added when required by the approved test
strategy; no test framework or test-first policy is assumed until that strategy is
confirmed.

## Architecture and Decisions Requiring Confirmation

The inspected project is a single `net10.0` ASP.NET Core Web API project with a
controller, a `WeatherForecast` model, and OpenAPI registration. No database provider,
data-access layer, test project, or authentication configuration was found in the
project's source files.

The following decisions remain open and MUST be confirmed before a feature depends on
them:

- **Project architecture:** whether to retain the single-project, controller-based
  structure or adopt layered or multi-project organization.
- **Data access:** whether persistence is needed and, if so, the storage technology and
  access pattern.
- **Testing:** test framework and scope, and whether test-first development is required.
- **Authentication and authorization:** whether API endpoints are public or protected,
  and which policy is required.
- **API versioning:** the compatibility and versioning policy, if future changes require
  one.

Until a relevant decision is confirmed, feature specs and plans MUST identify the
uncertainty instead of selecting an implementation by assumption.

## Development Workflow and Quality Gates

Features MUST use the Spec Kit artifacts to make intent and decisions reviewable:

- `spec.md` defines user-visible behavior and testable acceptance criteria.
- `plan.md` records the technical approach, evidence, validation method, and any decisions
  requiring confirmation.
- `tasks.md` breaks approved work into actionable tasks with the relevant project paths.
- Before implementation is considered complete, the required validation from the plan
  MUST be run and its result reported. The project build command in Principle V is
  mandatory; additional test commands depend on the confirmed testing strategy.

## Governance

This constitution governs feature specs, plans, tasks, and implementation. Compliance
MUST be checked during planning and before implementation is reported complete. Any
exception or amendment requires explicit project-owner approval and MUST be recorded by
updating this constitution with `/speckit-constitution`.

The constitution uses semantic versioning: increment MAJOR for incompatible changes to
principles, MINOR when adding a principle or materially expanding governance, and PATCH
for clarifications that do not change obligations. The original ratification date is not
present in the repository and requires confirmation; the date MUST be recorded in ISO
`YYYY-MM-DD` format once confirmed.

**Version**: 1.0.0 | **Ratified**: TODO(RATIFICATION_DATE): confirm original adoption date | **Last Amended**: 2026-11-17
