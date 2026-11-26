# Last Plate – Kiro Specification

**Document Version:** 1.1  
**Status:** For Review  
**Prepared:** 26 November 2026  
**Product:** Last Plate  
**Initiative:** Y2iH – Year To Improve Humanity  
**Development Tool:** Kiro IDE  
**Reference Documents:**
- Last Plate – Product Requirements Document (PRD) v1.1
- Last Plate – Software Architecture Document (SAD) v1.1
- Last Plate – Technical Implementation Plan (TIP) v1.1

---

# 1. Purpose

## 1.1 Objective

This document defines how Kiro will be configured and instructed to implement the Last Plate application.

It establishes project-wide development rules, architectural constraints, specification management, implementation procedures and approval requirements.

The objective is to make Kiro the primary implementation agent while ensuring that all generated code remains consistent with the approved product requirements and architecture.

## 1.2 Kiro's role

Kiro will be responsible for:

- Establishing the frontend and backend projects.
- Implementing application functionality.
- Creating and updating database migrations.
- Implementing REST APIs.
- Developing the user interface.
- Integrating AWS services.
- Writing automated tests.
- Identifying and resolving implementation defects.
- Maintaining technical documentation.
- Preparing the application for deployment.

Kiro must work within the approved project scope and must not independently change product or architectural decisions.

## 1.3 Human oversight

The product owner retains responsibility for:

- Product decisions.
- Requirements approval.
- Architecture approval.
- Implementation milestone approval.
- Reviewing significant technical decisions.
- Accepting completed functionality.
- Final release approval.

Kiro may recommend improvements, but must not silently change approved decisions.

The technical advisor supports requirements clarification, architectural review, specification review and implementation quality assurance.

The product owner retains final decision-making authority.

---

# 2. Source of Truth and Document Hierarchy

The following documents govern implementation:

| Document | Authority | Purpose |
|---|---|---|
| PRD | Product authority | Defines what Last Plate must do |
| SAD | Architecture authority | Defines how the application is structured |
| TIP | Implementation authority | Defines implementation sequence and delivery controls |
| Kiro Specification | Agent execution guidance | Defines how Kiro interprets and implements the approved work |

## 2.1 Conflict resolution

If Kiro identifies a conflict between documents:

1. Stop the affected implementation task.
2. Identify the conflicting requirements.
3. Explain the impact.
4. Recommend a resolution.
5. Wait for approval before changing the baseline.

Kiro must not independently resolve conflicts by choosing whichever option is easiest to implement.

## 2.2 Change management

Changes to approved requirements or architecture must be recorded.

Significant changes must include:

- Description of the proposed change.
- Reason for the change.
- Affected requirements.
- Affected modules.
- Technical implications.
- Testing implications.
- Approval decision.

The PRD, SAD or TIP must be updated when a change affects its content.

Kiro must not treat a proposed improvement as an approved requirement.

---

# 3. Kiro Project Configuration

## 3.1 Project directory

Kiro configuration must be maintained in the repository.

Proposed configuration:

```text
.kiro/
│
├── steering/
│   ├── product.md
│   ├── tech.md
│   ├── structure.md
│   ├── architecture.md
│   ├── coding-standards.md
│   ├── security.md
│   └── development-workflow.md
│
├── specs/
│   ├── 00-project-foundation/
│   ├── 01-authentication-and-security/
│   ├── 02-organisation-management/
│   ├── 03-food-listing-management/
│   ├── 04-food-discovery/
│   ├── 05-donation-management/
│   ├── 06-delivery-and-handover/
│   ├── 07-administration-and-reporting/
│   └── 08-notifications-and-release/
│
└── hooks/
```

Kiro may generate additional metadata or configuration files required by its own workflow. These must be preserved.

The actual specification directory structure must remain compatible with Kiro's native specification management.

## 3.2 Steering files

Steering files establish persistent project instructions.

The following files will be created.

| File | Responsibility |
|---|---|
| `product.md` | Product purpose, users, organisation roles, scope and business objectives |
| `tech.md` | Approved technology stack and dependencies |
| `structure.md` | Repository and package organisation |
| `architecture.md` | Modular monolith, architecture principles and module boundaries |
| `coding-standards.md` | Java, TypeScript, SQL and naming conventions |
| `security.md` | Authentication, authorisation, data protection and security rules |
| `development-workflow.md` | Specification sequence, implementation, testing and approval requirements |

These files must be consistent with the current approved project documents.

Kiro must not generate generic steering documents that contradict the established architecture.

## 3.3 Steering file creation process

The steering files do not automatically exist when the repository is created.

Kiro must therefore follow this onboarding sequence:

1. Read the PRD, SAD, TIP and Kiro Specification.
2. Analyse the repository and identify the required steering instructions.
3. Propose the contents of all seven steering files.
4. Identify any conflicts, missing decisions or duplicated instructions.
5. Present the proposed steering files for review.
6. Wait for explicit approval.
7. Create the approved steering files.
8. Verify that the files are consistent with the project documents.
9. Proceed to Specification 00 only after the steering files have been reviewed and accepted.

Kiro must not start application implementation while the steering-file review is outstanding.

---

# 4. Project-Wide Kiro Instructions

The following rules apply to every implementation task.

## 4.1 General development rules

1. Read the relevant steering files before implementing functionality.
2. Review the existing project structure before creating new files.
3. Follow the approved PRD, SAD and TIP.
4. Prefer straightforward implementations over unnecessary abstractions.
5. Do not introduce unapproved technologies.
6. Do not duplicate existing functionality.
7. Keep changes focused on the current specification.
8. Write tests alongside implementation.
9. Update documentation when behaviour or configuration changes.
10. Report unresolved issues rather than hiding them.
11. Do not implement requirements that have not passed their approval gates.
12. Do not silently change existing business rules.

## 4.2 Backend rules

- Use Java 21.
- Use Spring Boot and Maven.
- Use YAML configuration.
- Use Spring Security for API security.
- Use Spring Data JPA for persistence.
- Use PostgreSQL.
- Use PostGIS for geographical functionality.
- Use database migrations.
- Use DTOs for API input and output.
- Separate domain models from persistence entities where appropriate.
- Use Bean Validation.
- Implement consistent exception handling.
- Use explicit constructors.
- Do not use Lombok.
- Do not create interfaces without a meaningful architectural reason.
- Keep business logic independent of infrastructure implementations.
- Use transactions for operations that require atomic business updates.
- Enforce organisation membership, role and approval requirements in backend business logic.

## 4.3 Frontend rules

- Use React and TypeScript.
- Use Vite.
- Use Tailwind CSS.
- Use shadcn/ui where appropriate.
- Use React Router for navigation.
- Use a shared API communication layer.
- Keep components small and focused.
- Avoid unnecessary global state.
- Implement loading, empty, success and error states.
- Validate user input on the frontend for usability.
- Never rely on frontend validation as the only security or business-rule enforcement.

The interface must be responsive, accessible and visually consistent.

## 4.4 Database rules

- Use PostgreSQL.
- Use PostGIS where geographical queries are required.
- Use version-controlled migrations.
- Apply foreign keys and appropriate constraints.
- Use transactions for multi-step business operations.
- Avoid unnecessary denormalisation.
- Define indexes based on actual query requirements.
- Never modify production data through unreviewed scripts.
- Do not allow one module to directly manipulate another module's data.
- Preserve data integrity when organisation membership or permissions change.
- Protect reserved quantities against concurrent over-allocation.

## 4.5 API rules

- Use `/api/v1` as the API base path.
- Use REST conventions.
- Use JSON for request and response bodies.
- Use appropriate HTTP status codes.
- Validate all incoming requests.
- Implement consistent error responses.
- Use pagination for potentially large result sets.
- Protect all endpoints that require authentication.
- Enforce organisation membership and role permissions on the backend.
- Do not expose private organisation information or exact collection addresses prematurely.

## 4.6 AWS rules

Use the AWS services approved in the SAD:

- Amazon Cognito.
- Amazon RDS for PostgreSQL.
- Amazon S3.
- Amazon SES.
- Appropriate application hosting.
- Amazon CloudWatch.

Kiro must:

- Use least-privilege permissions.
- Keep secrets outside source control.
- Avoid hardcoded AWS credentials.
- Separate local and production configuration.
- Avoid provisioning unnecessary infrastructure.
- Identify expected costs and service prerequisites before deployment.
- Request approval before provisioning or modifying production infrastructure.

---

# 5. Architecture Enforcement

## 5.1 Modular monolith

The backend must remain one deployable Spring Boot application.

Business modules must remain logically separated.

The initial modules are:

1. Identity.
2. Organisation.
3. Food Listing.
4. Discovery.
5. Donation.
6. Delivery.
7. Handover.
8. Trust and Safety.
9. Reporting.

The module structure must follow the ownership and responsibilities defined in the SAD.

## 5.2 Module ownership

Kiro must respect the ownership boundaries defined in the SAD.

Examples:

- Identity owns individual application user accounts and organisation membership.
- Organisation owns organisation profiles, platform roles, verification and approval information.
- Food Listing owns donation listing management.
- Discovery owns food listing search and geographical discovery.
- Donation owns request approval and quantity reservation.
- Delivery owns collection and delivery arrangements.
- Handover owns transfer confirmation.
- Trust and Safety owns incident reporting and related review workflows.
- Reporting owns platform activity and impact reporting.

A module must not directly manipulate another module's persistence tables.

Cross-module operations must use explicitly defined application services or interfaces.

## 5.3 Dependency direction

The domain and application layers must not depend on infrastructure implementations.

Infrastructure must implement the required persistence and external-service boundaries.

Do not introduce an interface for every service or class merely to satisfy a pattern.

## 5.4 Authentication and authorisation boundaries

Amazon Cognito is responsible for user authentication.

The Last Plate application is responsible for organisation membership, platform roles, approval status and application permissions.

Kiro must:

- Validate Cognito-issued tokens through the approved Spring Security configuration.
- Resolve the authenticated application user.
- Load the user's organisation membership.
- Determine the organisation's platform role.
- Check the organisation's approval and suspension status.
- Enforce assigned permissions for the requested operation.
- Prevent users from accessing records outside their authorised organisation context.

Cognito authentication must not be treated as automatic authorisation to perform organisation-specific operations.

## 5.5 Architecture changes

Kiro must request approval before:

- Introducing a new application architecture.
- Introducing microservices.
- Adding a new infrastructure platform.
- Introducing a new database.
- Changing the approved authentication approach.
- Changing module ownership.
- Introducing a new major third-party dependency.

---

# 6. Kiro Specification Management

## 6.1 Specification approach

Each major implementation capability will be managed through an individual Kiro Feature Spec.

The implementation workflow is **Specification-Driven and Approval-Gated**.

The accepted SAD establishes the technical architecture. Kiro must use it as an architectural input instead of independently designing a replacement architecture.

Each Feature Spec must produce the standard Kiro specification artefacts:

- `requirements.md`
- `design.md`
- `tasks.md`

## 6.2 Specification approval process

Each specification follows three phases.

### Phase 1 – Requirements

Kiro must:

- Review the relevant PRD requirements.
- Identify functional requirements.
- Identify non-functional requirements.
- Define user stories.
- Define acceptance criteria.
- Identify dependencies.
- Identify ambiguities and missing information.
- Identify relevant business rules.
- Identify permissions and organisation-role restrictions.

The product owner reviews the requirements before proceeding.

### Phase 2 – Design

Kiro must:

- Follow the accepted SAD.
- Identify affected modules.
- Identify affected entities.
- Define API contracts.
- Describe business workflows.
- Identify security implications.
- Identify transactional requirements.
- Define data validation requirements.
- Define testing requirements.
- Identify any required changes to existing architecture or data structures.

The product owner reviews the design before implementation tasks are approved.

### Phase 3 – Tasks

Kiro must:

- Break work into small implementation tasks.
- Identify task dependencies.
- Identify affected files and modules where possible.
- Include test implementation.
- Include documentation updates.
- Define expected outcomes.
- Identify any manual configuration or AWS setup required.

The product owner reviews the task list before execution.

## 6.3 Approval rules

Kiro must not begin implementation until:

1. Requirements have been reviewed and approved.
2. The technical design has been reviewed and approved.
3. Implementation tasks have been reviewed and approved.

Approval must be explicit.

A request for clarification or a recommendation to proceed does not constitute approval.

## 6.4 Specification completion

A specification is not complete merely because all tasks are marked as done.

Completion requires:

- Relevant acceptance criteria satisfied.
- Automated tests passing.
- Manual acceptance testing completed.
- No unresolved critical defects.
- Documentation updated.
- Changes reviewed and committed.
- Product owner acceptance.

---

# 7. Specification Roadmap

The implementation will be managed using the following specifications.

## Specification 00 – Project Foundation

**Priority:** P0

### Scope

- Repository structure.
- Frontend project initialisation.
- Backend project initialisation.
- Development configuration.
- Database connectivity.
- Database migrations.
- API conventions.
- Exception handling.
- Health endpoint.
- Initial UI layout.
- Development documentation.

### Exit criteria

- The frontend and backend start successfully.
- The backend communicates with the development database.
- Database migrations execute successfully.
- The frontend can communicate with the backend.
- Initial project structure follows the approved architecture.

## Specification 01 – Authentication and Security

**Priority:** P0

### Scope

- Cognito configuration.
- User registration.
- Sign-in.
- Email verification.
- Password recovery.
- JWT validation.
- Spring Security configuration.
- Application user profile management.
- Protected API endpoints.
- Authentication-related security controls.

### Exit criteria

Users can authenticate and protected endpoints validate tokens correctly.

Application authorisation must use the application user and organisation context. Organisation membership and platform permissions are implemented in Specification 02.

## Specification 02 – Organisation Management and Membership

**Priority:** P0

### Scope

- Organisation registration.
- Organisation profile management.
- Service Provider and Service Consumer platform roles.
- One platform role per organisation profile.
- Registered and unregistered organisation support.
- Verification information.
- Administrator review.
- Approval and rejection.
- Additional-information requests.
- Suspension and reactivation.
- Individual user association with organisations.
- Multiple users per organisation.
- Organisation membership management.
- Membership permissions.
- Organisation-level access enforcement.

### Exit criteria

- Administrators can review organisations.
- Both organisation roles require approval before donation operations.
- Users can be associated with organisations.
- Organisation membership and permissions are enforced.
- An organisation cannot operate under both platform roles.
- Only approved organisations can perform authorised operational activities.

## Specification 03 – Food Listing Management

**Priority:** P0

### Scope

- Food listing creation.
- Listing updates.
- Publication and withdrawal.
- Food categories.
- Quantity and units.
- Preparation and packaging details.
- Expiry and deadline information.
- Storage requirements.
- Allergen information.
- Location.
- Delivery arrangement.
- Image upload.
- Service Provider authorisation.

### Exit criteria

Approved Service Providers can publish and manage valid food listings.

## Specification 04 – Food Discovery

**Priority:** P0

### Scope

- Geographical coordinates.
- PostGIS queries.
- Nearby listings.
- Distance filtering.
- Category filtering.
- Deadline filtering.
- Delivery arrangement filtering.
- Listing details.
- Address privacy.
- Service Consumer authorisation.

### Exit criteria

Approved Service Consumers can find available food based on location and relevant filters.

## Specification 05 – Donation Management

**Priority:** P0

### Scope

- Donation request creation.
- Requested quantities.
- Service Provider approval.
- Service Provider rejection.
- Quantity reservation.
- Cancellation.
- Reservation release.
- Request status transitions.
- Transactional integrity.
- Audit events.
- Delivery-fee proposal and agreement rules where applicable.

### Exit criteria

Donation requests can be managed without allowing over-allocation.

Cancellation, expiry and reservation-release rules must be explicitly defined and approved in this specification before implementation.

The delivery-fee proposal and acceptance sequence must also be agreed before implementation.

## Specification 06 – Delivery and Handover

**Priority:** P0

### Scope

- Service Consumer collection.
- Free Service Provider delivery.
- Paid Service Provider delivery.
- Delivery fee agreement.
- Handover records.
- Actual quantity transferred.
- Service Provider confirmation.
- Service Consumer confirmation.
- Discrepancy reporting.
- Dispute handling.

### Exit criteria

Both parties can record and confirm the physical transfer of food.

The implementation must follow the approved delivery-fee and handover workflows.

## Specification 07 – Administration and Reporting

**Priority:** P0 for essential administration; P1 for reporting and dashboard enhancements.

### P0 scope – Essential administration and trust management

- Administrator access and permissions.
- Organisation approval and rejection.
- Requests for additional verification information.
- Organisation suspension and reactivation.
- Report and incident review.
- Basic dispute investigation.
- Audit records of important administrative actions.

### P1 scope – Impact reporting and dashboard enhancements

- Administrator dashboard enhancements.
- Platform activity statistics.
- Food listing statistics.
- Donation request statistics.
- Completed handover statistics.
- Recorded food quantity reporting.
- Service Provider and Service Consumer participation reporting.
- Category and time-based reporting.
- Food recovery reporting.

### Exit criteria

**P0:**

- Administrators can manage organisation approvals.
- Administrators can suspend and reactivate organisations.
- Administrators can investigate reported incidents and disputes.
- Important administrative actions are auditable.

**P1:**

- Impact statistics reflect actual recorded platform activity.
- Reports do not count pending or rejected requests as completed donations.
- Recorded quantities reflect actual handover records.
- Meal estimates, if included, use a documented and defensible conversion method.

The P0 administrative capabilities must be completed before the MVP is considered operationally complete. P1 reporting enhancements must not delay the core donation workflow.

## Specification 08 – Notifications and Release

**Priority:** P0

### Scope

- SES integration.
- Transactional email notifications.
- Notification failure handling.
- Backend unit and integration tests.
- Frontend tests.
- End-to-end tests.
- Security checks.
- Production configuration.
- AWS deployment.
- Demonstration data.
- Production validation.

### Exit criteria

- The application is deployed.
- Core workflows are operational.
- Required email notifications are implemented.
- Email failures do not reverse committed business transactions.
- Critical tests pass.
- Demonstration workflows are verified.

---

# 8. Business Rule Enforcement

The following rules are mandatory and must be enforced in backend business logic.

## 8.1 Organisation rules

- An organisation must have exactly one platform role: Service Provider or Service Consumer.
- An organisation cannot register under both roles using the same organisation profile.
- Individual users must be associated with an organisation to perform organisation-specific donation operations.
- Multiple individual users may belong to the same organisation.
- Only approved organisations can perform restricted operational activities.
- Registered and unregistered community feeding organisations must be supported.
- Organisation approval must be controlled by an administrator.
- Suspended organisations must lose access to restricted functionality.
- Users must not access another organisation's private records without permission.
- Organisation membership and permissions must be checked by the backend.

## 8.2 Food listing rules

- Only authorised Service Provider users can publish listings.
- Required food information must be validated.
- Withdrawn and expired listings must not be available for new requests.
- Available quantities must not become negative.
- Exact addresses must be protected until the appropriate workflow stage.
- Service Consumers cannot publish food listings.

## 8.3 Discovery rules

- Only approved Service Consumers can request access to donation listings.
- Available listings must be discoverable according to the approved search and filtering rules.
- Exact collection addresses must only be disclosed to authorised recipients after request approval.
- Service Providers cannot submit donation requests.

## 8.4 Donation rules

- A Service Provider must approve each donation request.
- Approval must reserve the requested quantity.
- Concurrent approvals must not cause over-allocation.
- Rejected requests must not reserve quantities.
- Eligible cancellations must release reserved quantities.
- Status transitions must follow the approved donation lifecycle.
- Only authorised organisation users can submit or approve requests on behalf of their organisations.

## 8.5 Delivery rules

- Collection and delivery arrangements must be explicit.
- Delivery fees must be agreed by both parties.
- A fee change requires renewed acceptance.
- Payments occur outside the platform for the MVP.
- The application must record the agreed delivery arrangement and fee where applicable.

## 8.6 Handover rules

- Actual quantity transferred must be recorded.
- Both parties must confirm the handover.
- A donation must not be marked completed prematurely.
- Discrepancies must be recorded for investigation.

## 8.7 Food safety rules

- Food safety declarations must be captured from the Service Provider.
- Relevant dates, storage requirements and allergens must be recorded where applicable.
- The application must not claim that it independently certifies food safety.
- The application must not automatically treat expired or questionable food as safe.

---

# 9. Testing and Verification Requirements

Kiro must implement tests as part of each specification.

## 9.1 Backend

Use:

- JUnit 5.
- Mockito.
- Spring Boot Test.

Tests must cover:

- Business rules.
- Validation.
- Authentication and authorisation.
- Organisation membership.
- Organisation approval restrictions.
- Persistence.
- Transaction handling.
- Error handling.
- Integration between modules.

## 9.2 Frontend

Use appropriate React testing tools to validate:

- Component behaviour.
- Form validation.
- Loading states.
- Error states.
- Navigation.
- API integration.
- Role-appropriate user experiences.

Frontend restrictions must not replace backend authorisation checks.

## 9.3 End-to-end testing

Use Playwright to validate the complete user journey.

The critical end-to-end journey must cover:

1. Individual user registration.
2. Organisation registration or association.
3. Organisation role selection.
4. Organisation approval.
5. Food listing publication by an authorised Service Provider.
6. Food discovery by an approved Service Consumer.
7. Donation request submission.
8. Service Provider approval.
9. Quantity reservation.
10. Collection or delivery arrangement.
11. Delivery-fee agreement where applicable.
12. Handover.
13. Two-party confirmation.
14. Completed donation reporting.

## 9.4 Testing rules

- Do not remove tests merely to make a build pass.
- Do not weaken assertions to hide defects.
- Do not claim tests passed if they were not executed.
- Report skipped or failing tests.
- Add regression tests when fixing defects.
- Prioritise concurrency testing for quantity reservations.
- Test that Service Consumers cannot publish listings.
- Test that Service Providers cannot request donations.
- Test that unapproved and suspended organisations cannot perform restricted operations.
- Test that users cannot access another organisation's private data.

---

# 10. Kiro Agent Operating Rules

## 10.1 Implementation discipline

Kiro must work on the current approved specification.

It must not:

- Implement unrelated future features.
- Redesign the whole application during a small task.
- Replace approved dependencies without approval.
- Change database structures without migrations.
- Modify another module's responsibilities without justification.
- Create unnecessary files or duplicate classes.
- Introduce mock data as a substitute for working functionality in production.
- Claim a feature is complete when only its UI has been implemented.
- Bypass specification approval to save time.
- Change accepted business rules without approval.

## 10.2 Parallel implementation

Parallel agents may be used for independent tasks.

Examples include:

- Independent frontend components.
- Independent unit test suites.
- Documentation preparation.
- Separate modules with already-agreed API contracts.

Parallel agents must not independently modify shared architecture, shared database schemas or the same API contracts without coordination.

Parallel implementation must not bypass requirements, design or task approval.

## 10.3 Hooks and automation

Hooks may be introduced where they provide clear value.

Potential examples:

- Run relevant tests after important file changes.
- Check formatting or static analysis.
- Remind the agent to update tests.
- Validate documentation after a specification task is completed.

Hooks must not be allowed to perform destructive operations or deploy production changes without explicit approval.

Hooks are optional implementation aids, not prerequisites for starting development.

## 10.4 Custom agents and additional tooling

Custom agents, MCP servers and additional extensions may be considered when there is a demonstrated need.

They must not be introduced simply because the functionality exists in Kiro.

The initial implementation should prioritise Kiro Specs, steering and controlled task execution.

---

# 11. Approval Gates

The following approvals are mandatory.

| Gate | Required review |
|---|---|
| G1 | Steering files and project instructions |
| G2 | Repository and project structure |
| G3 | Authentication and security design |
| G4 | Organisation, membership and database entities |
| G5 | Donation reservation and cancellation logic |
| G6 | Delivery and handover workflow |
| G7 | AWS infrastructure and deployment |
| G8 | Final end-to-end acceptance |

Kiro must stop and request review when a task reaches a defined approval gate.

Approval to proceed with one specification does not automatically approve changes outside that specification.

---

# 12. Credit and Time Management

The project has an allocated Kiro credit balance of 4,000 credits.

Kiro usage must be monitored throughout implementation.

Rules:

1. Use focused prompts.
2. Avoid repeatedly regenerating approved documents.
3. Reuse existing project context.
4. Avoid unnecessary parallel agents.
5. Review generated work before requesting extensive revisions.
6. Prioritise P0 functionality.
7. Monitor actual credit consumption.
8. Do not sacrifice testing and correctness merely to conserve credits.
9. Keep specification tasks focused and avoid repeatedly redesigning already-approved work.

The project target is Saturday, 28 November 2026.

If time or credits become constrained, defer P2 and P3 functionality rather than compromising core workflows.

---

# 13. Git and Version Control

Kiro must follow the repository conventions.

- Commit related changes in logical units.
- Use descriptive commit messages.
- Do not commit credentials or secrets.
- Do not commit generated build artefacts.
- Do not exclude the `.kiro/` directory.
- Do not rewrite shared Git history without approval.
- Keep the repository buildable at milestone boundaries.
- Update README instructions when setup or deployment procedures change.
- Do not push changes to the public repository without the required approval.

The repository must remain suitable for public competition submission.

---

# 14. Definition of Done

A Kiro task is complete only when:

- The approved requirement is implemented.
- The implementation follows the accepted architecture.
- Required validation is present.
- Relevant security checks are present.
- Automated tests pass.
- The frontend and backend are integrated where applicable.
- No known critical defect remains.
- Documentation is updated where necessary.
- The code changes are available for review.

A specification is complete only when:

- All approved acceptance criteria are satisfied.
- Required automated tests have passed.
- Manual acceptance testing has been completed.
- Outstanding defects and limitations are documented.
- The product owner has reviewed and accepted the result.

---

# 15. Initial Kiro Instruction

When the repository has been created and the project documents have been added, Kiro will receive the following initial instruction.

## Project onboarding instruction

> You are the primary implementation agent for Last Plate, a Y2iH product being developed for Kiroween 2026.
>
> Before writing application code, read and analyse the following project documents:
>
> - Product Requirements Document (PRD).
> - Software Architecture Document (SAD).
> - Technical Implementation Plan (TIP).
> - Kiro Specification.
>
> Treat these documents as the project's source of truth.
>
> Do not redesign the architecture, introduce unapproved technologies, change business rules or expand the product scope.
>
> **Stage 1 – Project analysis**
>
> Analyse the documents and repository structure.
>
> Identify the project-wide instructions that need to be maintained through Kiro steering files.
>
> Prepare proposed contents for:
>
> - `product.md`
> - `tech.md`
> - `structure.md`
> - `architecture.md`
> - `coding-standards.md`
> - `security.md`
> - `development-workflow.md`
>
> Identify any conflicts, missing decisions, duplicated instructions or areas requiring clarification.
>
> Present the proposed steering files for review.
>
> Do not create the final steering files or begin application implementation until they have been reviewed and explicitly approved.
>
> **Stage 2 – Steering configuration**
>
> After approval, create the steering files under `.kiro/steering/`.
>
> Verify that the files accurately reflect the approved project documents and do not introduce new requirements or architectural decisions.
>
> Report the files created and any remaining issues.
>
> **Stage 3 – Project Foundation**
>
> Only after the steering files have been approved and created, begin Specification 00 – Project Foundation.
>
> Produce the requirements, design and implementation task artefacts using the Specification-Driven, Approval-Gated workflow.
>
> Identify ambiguities, missing decisions and conflicts before requesting approval.
>
> Present the proposed requirements, design and tasks for review.
>
> Wait for explicit approval before implementing any tasks.
>
> **Stage 4 – Implementation**
>
> After approval, implement the work incrementally.
>
> Write and execute relevant tests, report the files created or modified, provide test results and identify remaining issues.
>
> Do not claim success unless the relevant functionality has been implemented and verified.
>
> Follow the same approval process for every subsequent specification.
>
> The product owner retains final approval authority throughout the project.

---

# 16. Document Control

| Item | Value |
|---|---|
| Document | Kiro Specification |
| Version | 1.1 |
| Status | For Review |
| Supersedes | Kiro Specification v1.0 |
| Product | Last Plate |
| Reference PRD | v1.1 |
| Reference SAD | v1.1 |
| Reference TIP | v1.1 |
| Development tool | Kiro IDE |
| Target MVP completion | 28 November 2026 |

This document becomes the active Kiro implementation guidance once reviewed and accepted.

Changes to project-wide instructions, specification priorities, approval requirements or implementation controls must be reviewed against the PRD, SAD and TIP.