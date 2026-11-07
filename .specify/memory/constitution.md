<!--
Sync Impact Report (temporary review material; remove before committing)
Version change: unversioned scaffold -> 1.0.0 (initial adoption)
Modified principles: unfilled scaffold slots replaced with:
- I. Specification-Driven Development
- II. Offline-First Training
- III. Clear Layer and Infrastructure Boundaries
- IV. Authorization and Data Isolation
- V. Focused Verification and Simplicity
Added sections: Technology and Training Constraints; Development Workflow and Quality Gates
Removed sections: none; scaffold example comments removed
Follow-up TODOs: none
-->
# ContosoDashboard Constitution

## Core Principles

### I. Specification-Driven Development

Every feature MUST have a specification describing user outcomes, scope, acceptance criteria,
and relevant authorization rules before implementation begins. Implementation plans and tasks
MUST trace back to that specification. Ambiguous requirements MUST be clarified or recorded as
explicit assumptions before dependent work proceeds. Behavior changes MUST update affected
specifications and documentation. This makes the training exercise reproducible and reviewable.

### II. Offline-First Training

The application MUST remain usable locally without a cloud subscription, cloud credentials,
or a required remote service after documented development prerequisites are installed.
Training data MUST be fictional, and mock authentication MUST remain explicitly labeled as
training-only. New infrastructure-dependent features MUST provide a local implementation.
Cloud migration examples MUST remain optional and MUST NOT be represented as production-ready
deployments. These constraints preserve training availability and prevent misleading security claims.

### III. Clear Layer and Infrastructure Boundaries

Pages MUST handle presentation and delegate business operations to services. Services MUST own
business rules and authorization decisions; persistence MUST use the Data layer and EF Core.
Models MUST describe domain data without depending on UI components. New replaceable infrastructure
dependencies, including file storage, MUST be exposed through interfaces and wired through dependency
injection so business logic does not depend on a local or cloud implementation. Existing suitable
services and patterns MUST be reused rather than creating parallel abstractions.

### IV. Authorization and Data Isolation

Protected pages MUST require authentication. Every service operation that accesses protected data
MUST verify the caller's permitted role, ownership, or project membership as defined by the feature
specification. UI visibility and caller-supplied record identifiers MUST NOT substitute for service
authorization. Input MUST be validated at the boundary that consumes it. File-based features MUST
validate permitted types and size limits, generate unique storage identifiers before persistence,
and prevent user-controlled paths from escaping the configured storage directory. Sensitive data,
credentials, and file contents MUST NOT be included in logs.

### V. Focused Verification and Simplicity

Each behavior change MUST include repeatable verification tied to its acceptance criteria.
Bug fixes MUST include a regression check that demonstrates the original failure. Changes to
authorization, persistence, or infrastructure contracts MUST include integration checks for
allowed, denied, and failure paths as applicable. Automated checks MUST be used where available;
manual checks MUST record steps and expected outcomes when automation is unavailable. Changes
MUST remain scoped to the requirement, and added dependencies or abstractions MUST have a
documented need. Failures MUST surface actionable errors rather than being silently swallowed.

## Technology and Training Constraints

- The baseline stack is ASP.NET Core 8.0, Blazor Server, C#, Entity Framework Core, and SQL Server
	LocalDB. UI changes MUST preserve the existing Bootstrap 5.3 and Bootstrap Icons conventions.
- Technology replacements MUST be justified in an implementation plan and reviewed before adoption.
- Local filesystem storage MUST be the default for file-based training features. Storage and
	database failure handling MUST avoid orphaned files or records, or provide documented cleanup.
- Setup instructions MUST identify required tools, local configuration, and reproducible startup
	steps. Secrets and machine-specific credentials MUST NOT be committed.
- Documentation MUST retain the training-only disclaimer and known limitations. Real production
	data and public production deployment are outside the governed training application's scope.

## Development Workflow and Quality Gates

1. Define the feature specification and clarify acceptance criteria, boundaries, and access rules.
2. Produce a plan and actionable tasks. Review compliance with each core principle before coding.
3. Implement the smallest scoped change using existing architecture and conventions.
4. Run `dotnet build ContosoDashboard/ContosoDashboard.csproj` from the repository root, plus
	 focused checks for changed behavior. Test projects, when present, MUST pass their relevant
	 `dotnet test` checks. Environment blockers MUST be recorded; blocked checks MUST NOT be
	 reported as passing.
5. For affected UI workflows, verify normal and empty/error states and desktop/mobile layouts.
	 For protected workflows, verify unauthenticated access, authorized access, and unauthorized
	 record access with the relevant mock users.
6. Before acceptance, review specification traceability, authorization, failure handling, test
	 evidence, and documentation. Any unresolved failure or exception MUST be recorded with its
	 impact and an explicit acceptance decision by the project maintainer or training facilitator.

## Governance

This constitution takes precedence over conflicting project practices. Feature specifications,
plans, tasks, and reviews MUST check compliance with its principles. The README supplies operational
guidance but MUST NOT be used to override these rules.

Amendments MUST document the proposed change, rationale, affected principles, and any migration or
documentation work. The project maintainer or training facilitator MUST approve an amendment before
it is adopted. Changes MUST preserve the original ratification date and update the last-amended date.
Dependent documents MUST be checked for consistency and follow-up changes tracked separately.

Versions MUST follow MAJOR.MINOR.PATCH: MAJOR for incompatible principle removals or redefinitions,
MINOR for new principles or materially expanded requirements, and PATCH for non-semantic wording
or clarification changes. Version 1.0.0 records this constitution's initial adoption.

Every feature acceptance review MUST identify any noncompliance. Exceptions MUST name the violated
rule, rationale, scope, approver, and follow-up action; implicit exceptions are not permitted.
The temporary Sync Impact Report MUST be removed before committing an amended constitution.

**Version**: 1.0.0 | **Ratified**: 2026-11-07 | **Last Amended**: 2026-11-07
