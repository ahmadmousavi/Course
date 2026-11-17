<!--
Sync Impact Report
Version change: 1.0.0 -> 1.1.0
Modified principles: II (ADR recording for significant project-wide decisions); V (separate build from feature validation)
Added guidance: initial architecture assessment is a snapshot; speckit-analyze gate before implementation
Removed sections: none
Follow-up TODOs: confirm original ratification date; confirm ADR location/format if needed
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
scope or behavior. Project-wide architectural decisions with cross-feature or lasting
architectural impact MUST be recorded in an ADR when appropriate, and the relevant
feature plan MUST reference that ADR. A feature plan alone does not replace an ADR for
such a decision.

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
`dotnet build MyApi/MyApi.csproj` MUST succeed. The plan MUST separately identify any
feature-specific tests and other validation required by the acceptance criteria, and
those checks MUST be run and reported. This does not establish a project-wide test
framework or a mandatory test-first policy.

## Architecture and Decisions Requiring Confirmation

The initial repository assessment found a single `net10.0` ASP.NET Core Web API project
with a controller, a `WeatherForecast` model, and OpenAPI registration. No database
provider, data-access layer, test project, or authentication configuration was found in
the project's source files at that assessment.

This assessment is an initial snapshot, not a permanent description of the repository.
When planning a feature that depends on architecture or project capabilities, the current
repository MUST be re-inspected and the evidence in that feature's plan updated; decisions
MUST NOT rely on this snapshot alone.

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
- **ADR convention:** the repository does not establish an ADR location or format; confirm
  the convention before creating an ADR if an applicable decision arises.

Until a relevant decision is confirmed, feature specs and plans MUST identify the
uncertainty instead of selecting an implementation by assumption.

## Development Workflow and Quality Gates

Features MUST use the Spec Kit artifacts to make intent and decisions reviewable:

- `spec.md` defines user-visible behavior and testable acceptance criteria.
- `plan.md` records the technical approach, evidence, validation method, and any decisions
  requiring confirmation.
- `tasks.md` breaks approved work into actionable tasks with the relevant project paths.
- Important project-wide architectural decisions MUST be recorded in an ADR when
  appropriate; the related `plan.md` MUST reference it. Use an established repository
  ADR convention when one exists. If none exists, record the convention as requiring
  confirmation rather than inventing a location or format.
- After `spec.md`, `plan.md`, and `tasks.md` are available, `/speckit-analyze` MUST be run
  before `/speckit-implement`. Its report MUST be reviewed for consistency and coverage
  across those artifacts. Critical findings MUST be resolved before implementation;
  other findings MUST be resolved or have an explicit approved disposition.
- Before implementation is considered complete, the validation requirements from
  Principle V MUST be run and their results reported. The project build command is
  mandatory; feature-specific tests and other checks are determined by the plan.

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

**Version**: 1.1.0 | **Ratified**: TODO(RATIFICATION_DATE): confirm original adoption date | **Last Amended**: 2026-11-17
