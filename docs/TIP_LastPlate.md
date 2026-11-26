# Last Plate – Technical Implementation Plan (TIP)

**Document Version:** 1.1  
**Status:** For Review  
**Prepared:** 26 November 2026  
**Target MVP Completion:** 28 November 2026  
**Product:** Last Plate  
**Initiative:** Y2iH – Year To Improve Humanity  
**Reference Documents:** PRD v1.1 and SAD v1.1

---

# 1. Introduction

## 1.1 Purpose

This Technical Implementation Plan defines how the Last Plate MVP will be developed, tested and deployed.

It translates the approved Product Requirements Document (PRD) and Software Architecture Document (SAD) into an actionable development sequence.

The plan will guide development activities and the Kiro implementation process.

## 1.2 Implementation objectives

The implementation must deliver:

1. A working platform connecting organisations with surplus food to community feeding organisations.
2. Secure user authentication and organisation approval.
3. Individual user accounts associated with organisations.
4. Organisation membership and permission management.
5. Food donation listing and discovery.
6. Donation requests with Service Provider approval.
7. Reliable quantity reservation and availability management.
8. Collection and delivery arrangements.
9. Handover confirmation by both parties.
10. Essential administrative and trust-management capabilities.
11. Basic impact reporting capabilities.
12. Email notifications for important workflow events.
13. A publicly accessible application suitable for the Kiroween 2026 competition.

## 1.3 Delivery target

The target is a functional MVP by Saturday, 28 November 2026.

This is an aggressive delivery target. Implementation must prioritise complete core workflows, reliable business rules and a polished user experience over optional functionality.

Production hardening beyond the competition requirements will be treated as future work.

---

# 2. Approved Technical Baseline

Implementation must follow the accepted SAD.

| Area | Approved technology or approach |
|---|---|
| Architecture | Modular Monolith |
| Backend architecture | Layered Architecture with Clean Architecture principles |
| Frontend | React + TypeScript |
| Frontend tooling | Vite |
| UI styling | Tailwind CSS |
| UI components | shadcn/ui |
| Backend | Java 21 + Spring Boot |
| Backend build | Maven |
| API | REST |
| Authentication | Amazon Cognito |
| Database | PostgreSQL |
| Geographical queries | PostGIS |
| Database migrations | Version-controlled migrations |
| File storage | Amazon S3 |
| Email | Amazon SES |
| Testing | JUnit 5, Mockito, Spring Boot Test, frontend tests and Playwright |
| Deployment | AWS-first |

## 2.1 Architectural restrictions

The implementation must not introduce the following without explicit approval:

- Microservices.
- Kubernetes.
- Kafka.
- Redis.
- Elasticsearch.
- A separate Python backend.
- An AI/LLM subsystem.
- In-platform messaging.
- Integrated payment processing.

The backend remains one deployable Spring Boot application.

## 2.2 Organisation and application access model

The implementation must distinguish between organisation platform roles and individual user accounts.

The two organisation platform roles are:

- **Service Provider:** An organisation that makes surplus food available to other organisations.
- **Service Consumer:** An organisation that receives food donations to support community feeding activities.

An organisation must have exactly one of these platform roles.

Individual users register and authenticate through their own accounts and are associated with an organisation. Multiple individual users may belong to the same organisation.

Application permissions must be determined using the authenticated user, organisation membership, organisation platform role, organisation approval status and assigned permissions.

The application must not rely solely on Cognito token claims to determine organisation permissions.

Independent individual food-provider accounts are outside the MVP scope.

---

# 3. Repository and Project Structure

## 3.1 Repository

The project will use one Git repository containing the frontend, backend, documentation and Kiro configuration.

Proposed structure:

```text
last-plate/
│
├── .kiro/
│   ├── specs/
│   ├── steering/
│   └── hooks/
│
├── frontend/
│
├── backend/
│
├── docs/
│   ├── requirements/
│   ├── architecture/
│   ├── implementation/
│   └── decisions/
│
├── scripts/
│
├── .gitignore
├── LICENSE
├── README.md
└── CONTRIBUTING.md
```

The `.kiro/` directory must be committed to the public GitHub repository, in accordance with the competition requirements.

The repository must also include an open-source licence and useful setup instructions.

## 3.2 Project conventions

- Use descriptive names for packages, classes, methods and variables.
- Keep business modules organised by feature.
- Use explicit constructors rather than Lombok.
- Use YAML for Spring Boot configuration.
- Keep secrets outside source control.
- Use DTOs for API communication.
- Keep database entities separate from API response models.
- Use database migrations instead of relying on automatic schema generation.
- Keep frontend API communication in a shared service layer.
- Avoid unnecessary abstractions and duplicate implementations.
- Keep organisation membership and application permissions explicit.
- Enforce authorisation on the backend, not only through frontend navigation or visibility.

The final Java package namespace must be confirmed before project initialisation. The provisional namespace in the SAD is `za.co.y2ih.lastplate`.

---

# 4. Implementation Strategy

## 4.1 Development approach

Development will be incremental and milestone-driven.

Each milestone must produce a working, testable result.

Kiro must not be instructed to implement the entire platform in a single task.

The implementation cycle will be:

1. Review the relevant approved product requirements and architecture.
2. Generate or review the relevant Kiro specification.
3. Review and approve the specification requirements.
4. Review and approve the proposed technical design.
5. Review and approve the implementation tasks.
6. Allow Kiro to implement the approved tasks.
7. Review generated code and architecture.
8. Execute automated tests.
9. Perform manual acceptance testing.
10. Commit the completed work after approval.
11. Proceed to the next approved specification.

Requirements, design and implementation tasks must be reviewed before implementation begins.

## 4.2 Parallel development

Parallel work may be used when tasks are genuinely independent.

For example:

- Frontend layout development can proceed alongside backend project setup.
- UI components can be developed while independent database migrations are being prepared.
- Documentation can be updated while independent tests are being implemented.

However, tasks involving shared API contracts, database structures and business workflows must be coordinated.

Kiro must not allow two agents to independently redefine the same API contract, database entity or business rule.

Parallel work must not bypass the specification and approval process.

## 4.3 Implementation priority

Priorities will be classified as follows:

| Priority | Meaning |
|---|---|
| P0 – Critical | Required for the core platform to function safely and correctly |
| P1 – High | Required for a complete and credible MVP but not a prerequisite for the core donation transaction |
| P2 – Medium | Useful improvement if time permits |
| P3 – Future | Explicitly outside the current MVP |

P0 functionality must be completed before optional improvements are considered.

---

# 5. Implementation Milestones

## M1 – Project Foundation

**Priority:** P0

**Target:** 25–26 November

### Objectives

Establish the development environment, repository and application foundations.

### Backend tasks

- Initialise Spring Boot application.
- Configure Java 21 and Maven.
- Establish feature-based module structure.
- Configure YAML application profiles.
- Configure PostgreSQL connectivity.
- Configure database migration tooling.
- Establish global exception handling.
- Establish standard API response and error conventions.
- Add initial health endpoint.

### Frontend tasks

- Initialise React and TypeScript using Vite.
- Configure Tailwind CSS.
- Configure shadcn/ui.
- Establish frontend routing.
- Establish shared application layout.
- Create reusable UI foundations.
- Establish API communication configuration.

### Repository tasks

- Create GitHub repository.
- Add `.gitignore`.
- Add MIT licence, subject to final repository licensing review.
- Add README.
- Commit `.kiro/` configuration.
- Add initial project documentation.

### Acceptance criteria

- Frontend starts successfully.
- Backend starts successfully.
- Backend connects to the development database.
- Database migrations execute successfully.
- Frontend can communicate with the backend.
- Repository contains the required project structure and documentation.

**Deliverable:** Running frontend and backend foundations.

---

## M2 – Authentication and Organisation Management

**Priority:** P0

**Target:** 26 November

### Objectives

Allow individual users to register, authenticate and establish their organisation profiles.

### Authentication tasks

- Configure Amazon Cognito user pool.
- Configure application client and callback URLs.
- Implement frontend sign-in and registration.
- Implement email verification.
- Implement password recovery.
- Configure Spring Security JWT validation.
- Establish application user profile management.
- Implement organisation membership.
- Implement membership and permission management.
- Protect backend endpoints.
- Load the user's organisation context for authorisation.
- Enforce organisation role and approval restrictions.

### Organisation tasks

- Implement organisation registration.
- Support the Service Provider and Service Consumer organisation roles.
- Enforce one platform role per organisation profile.
- Support registered and unregistered community feeding organisations.
- Capture organisation information and contact details.
- Support multiple individual users associated with an organisation.
- Implement verification information submission.
- Implement administrator approval and rejection.
- Implement additional-information-required status.
- Implement organisation suspension and reactivation.
- Enforce organisation approval before operational access.

### Acceptance criteria

- Users can register and authenticate.
- Invalid or expired tokens are rejected.
- Authenticated users can access only permitted functionality.
- Individual user accounts can be associated with organisations.
- Multiple users can be associated with the same organisation.
- An organisation cannot operate as both a Service Provider and Service Consumer under the same profile.
- Organisations can be submitted for review.
- Administrators can approve, reject or request additional information.
- Both organisation roles require approval before donation operations.
- Unapproved organisations cannot publish or request donations.
- Suspended organisations cannot perform restricted operations.
- Organisation permissions are enforced by the backend.

**Deliverable:** Working authentication, organisation onboarding and membership management.

---

## M3 – Food Listing Management

**Priority:** P0

**Target:** 26–27 November

### Objectives

Allow approved Service Providers to publish available surplus food.

### Tasks

- Implement food listing domain model.
- Implement food listing creation.
- Implement listing modification.
- Implement listing publication.
- Implement listing withdrawal.
- Capture food category and description.
- Capture available quantity and measurement unit.
- Capture preparation and packaging information.
- Capture use-by or best-before information where applicable.
- Capture storage requirements and allergens where known.
- Capture collection deadline.
- Capture approximate and exact location information.
- Capture collection or delivery arrangement.
- Capture optional delivery fee.
- Integrate S3 image storage.
- Validate listing information before publication.
- Enforce Service Provider permissions.

### Acceptance criteria

- Approved Service Providers can create food listings.
- Required information is validated.
- Listings can be edited or withdrawn.
- Food images can be uploaded securely.
- Available quantities are represented correctly.
- Expired or withdrawn listings are not offered as available donations.
- Unapproved or suspended organisations cannot publish listings.
- Service Consumers cannot publish food listings.

**Deliverable:** Functional food donation management.

---

## M4 – Food Discovery

**Priority:** P0

**Target:** 26–27 November

### Objectives

Allow approved Service Consumers to find available food donations.

### Tasks

- Implement geographical data storage.
- Configure PostGIS.
- Implement nearby listing searches.
- Implement distance-based filtering.
- Implement category filtering.
- Implement deadline filtering.
- Implement delivery-arrangement filtering.
- Implement listing detail views.
- Apply exact-address privacy rules.
- Implement pagination or bounded result sets.
- Enforce Service Consumer permissions.

### Acceptance criteria

- Approved Service Consumers can discover available listings.
- Nearby results are ordered by proximity.
- Filters return appropriate results.
- Unavailable and expired listings are excluded.
- Exact collection addresses are not exposed prematurely.
- Exact addresses are disclosed only to authorised recipients after request approval.
- Discovery works without requiring an interactive map.
- Service Providers cannot submit donation requests.

**Deliverable:** Working nearby food discovery.

---

## M5 – Donation Requests and Quantity Reservation

**Priority:** P0

**Target:** 27 November

### Objectives

Allow Service Consumers to request donations and Service Providers to approve or reject requests.

### Tasks

- Implement donation request model.
- Implement request submission.
- Capture requested quantity.
- Capture proposed collection or delivery arrangement.
- Capture proposed delivery fee where applicable.
- Implement Service Provider request dashboard.
- Implement request approval.
- Implement request rejection.
- Implement quantity reservation.
- Implement approved cancellation and reservation-release rules.
- Implement request status transitions.
- Record important workflow events.
- Prevent unauthorised changes to approved requests.

### Transactional requirements

The quantity reservation process must be protected against concurrent requests.

Approving a request and reserving its quantity must happen as one database transaction.

The implementation must prevent:

- Reserving more than the available quantity.
- Approving duplicate or invalid requests.
- Reserving food from withdrawn or expired listings.
- Releasing quantities that were never reserved.
- Changing an approved quantity without the appropriate business process.
- Allowing a user to approve a request on behalf of an organisation without the required permissions.

Cancellation rules must define who can cancel, when cancellation is permitted, how expired requests are handled and when reserved quantities are released. These rules must be agreed in the relevant feature specification before implementation.

### Delivery-fee requirements

Where a Service Provider charges a delivery fee:

- The proposed fee must be visible to the Service Consumer before agreement.
- The Service Consumer must explicitly accept the fee.
- An agreed fee must not be changed unilaterally.
- A fee change must require renewed recipient consent.
- Payment remains outside the platform.

The detailed sequence for proposing, accepting and confirming delivery arrangements must be defined in the relevant feature specification and approved before implementation.

### Acceptance criteria

- Service Consumers can submit requests for available donations.
- Service Providers can approve or reject requests.
- Approved quantities are reserved correctly.
- Concurrent requests cannot over-allocate food.
- Rejected requests do not reserve quantities.
- Eligible cancellations release reserved quantities.
- Request history and status changes are recorded.
- Delivery-fee acceptance is recorded where applicable.
- Organisation membership and permissions are enforced throughout the workflow.

**Deliverable:** Complete donation request and approval workflow.

---

## M6 – Delivery, Collection and Handover

**Priority:** P0

**Target:** 27 November

### Objectives

Support the physical transfer of food between Service Providers and Service Consumers.

### Tasks

- Implement collection arrangement.
- Implement free Service Provider delivery.
- Implement Service Provider delivery with a fee.
- Capture proposed and agreed delivery fee.
- Require recipient acceptance of the fee.
- Prevent unilateral fee changes after agreement.
- Implement handover records.
- Capture actual quantity transferred.
- Implement Service Provider confirmation.
- Implement Service Consumer confirmation.
- Implement discrepancy handling.
- Implement dispute status.
- Record handover and status-change events.

### Acceptance criteria

- Collection and delivery arrangements are recorded.
- Delivery fees are explicitly agreed by both parties.
- Payment remains outside the platform.
- Handover records contain the required information.
- Both parties can confirm the handover.
- Actual quantities are recorded.
- Discrepancies can be flagged.
- A donation is not marked completed without the required confirmations.
- Handover actions are restricted to authorised organisation users.

**Deliverable:** Functional collection, delivery and handover workflow.

---

## M7 – Administration, Trust and Impact Reporting

**Priority:** P0 for essential administration; P1 for impact reporting and dashboard enhancements

**Target:** 27 November

### Objectives

Provide the essential administrative and trust-management capabilities required to operate the MVP, together with basic impact reporting.

### P0 – Essential administration and trust management

- Implement administrator access and permissions.
- Implement administrator dashboard for operational tasks.
- Display pending organisation applications.
- Display approved and suspended organisations.
- Implement organisation approval and rejection actions.
- Implement requests for additional verification information.
- Implement organisation suspension and reactivation.
- Implement report submission and review.
- Implement basic dispute and incident review.
- Record administrative actions in audit logs.
- Restrict administrative functions to authorised administrators.

### P1 – Basic impact reporting and dashboard enhancements

- Total food listings.
- Total donation requests.
- Total approved requests.
- Total completed handovers.
- Total recorded food quantity handed over.
- Participating Service Providers.
- Participating Service Consumers.
- Basic category and time-based reporting.
- Dashboard summaries for operational activity.

Meal estimates must only be introduced where a documented and defensible conversion method exists.

### Acceptance criteria

**P0 acceptance criteria**

- Administrators can manage organisation approvals.
- Administrators can suspend and reactivate organisations.
- Administrators can investigate reported incidents and disputes.
- Important administrative actions are auditable.
- Administrative functions are protected by backend authorisation.
- Organisation approval restrictions are consistently enforced.

**P1 acceptance criteria**

- Impact figures reflect recorded platform activity.
- Reports do not count pending or rejected requests as completed donations.
- Recorded food quantities reflect actual handover records.
- Reporting can distinguish Service Providers and Service Consumers.
- Any meal estimates use a documented conversion methodology.

**Deliverable:** Essential administration and trust-management capabilities, with basic impact reporting.

---

## M8 – Notifications, Testing and Release

**Priority:** P0

**Target:** 28 November

### Email tasks

- Configure Amazon SES.
- Implement notification service.
- Implement organisation registration notifications.
- Implement organisation approval and rejection notifications.
- Implement donation request notifications.
- Implement request decision notifications.
- Implement collection and delivery notifications.
- Implement handover notifications.
- Handle email delivery failures.

Notification intent must be recorded in a manner that preserves the successful business transaction. Email delivery must be handled separately from the committed transaction, with appropriate failure handling and retry capability.

An email failure must not reverse a successfully committed donation transaction.

### Testing tasks

- Execute backend unit tests.
- Execute backend integration tests.
- Execute frontend tests.
- Execute API security tests.
- Execute end-to-end tests.
- Test quantity reservation under concurrent requests.
- Test organisation approval restrictions.
- Test organisation membership and permissions.
- Test cancellation and reservation release.
- Test delivery-fee agreement.
- Test handover confirmation.
- Test administrative permissions.
- Test exact-address privacy.
- Test notification failure handling.

### Release tasks

- Configure production environment.
- Provision and configure required AWS resources.
- Apply production database migrations.
- Configure Cognito production settings.
- Configure S3 access policies.
- Configure SES sending.
- Configure frontend and backend hosting.
- Configure HTTPS and application URLs.
- Configure CloudWatch logging.
- Load demonstration data.
- Create judge-accessible demonstration accounts.
- Validate the application from a clean browser session.
- Prepare the competition demonstration.

### Acceptance criteria

- The production application is accessible.
- Users can complete the core workflows.
- Critical security and business-rule tests pass.
- Emails are sent for required events.
- Email failures do not corrupt successful business transactions.
- Demonstration accounts work.
- No critical defects remain in the core workflows.
- The application is suitable for the competition demonstration.

**Deliverable:** Deployed Last Plate MVP.

---

# 6. Delivery Schedule

The following is the proposed delivery schedule. It is a target plan rather than a guarantee of completion.

| Date | Primary focus | Expected outcome |
|---|---|---|
| Wednesday, 25 November | Foundation and initial project setup | Repository, project structure and application foundations |
| Thursday, 26 November | Foundation completion, authentication, organisation management, listings and discovery | Users can onboard and approved organisations can publish and discover food |
| Friday, 27 November | Requests, reservations, handovers and essential administration | Main donation workflow and operational administration are functional |
| Saturday, 28 November | Integration, testing, deployment and presentation | Complete demonstrable MVP |

Sunday, 29 November may be used as a contingency buffer if necessary.

## 6.1 Critical delivery dependencies

The following dependencies must be addressed early:

1. AWS account access and permissions.
2. Cognito configuration and application URLs.
3. PostgreSQL provisioning and PostGIS availability.
4. Frontend and backend deployment decisions.
5. S3 bucket and access configuration.
6. SES sending permissions and verification requirements.

AWS account setup, service quotas, email-sending restrictions and deployment configuration may introduce delays.

These dependencies must not be left until the final day.

---

# 7. Kiro Implementation Management

## 7.1 Specification strategy

Kiro specifications will be created in manageable units.

Proposed specification sequence:

| ID | Kiro specification | Dependency |
|---|---|---|
| 00 | Project Foundation | None |
| 01 | Authentication and Security | 00 |
| 02 | Organisation Management and Membership | 01 |
| 03 | Food Listing Management | 02 |
| 04 | Food Discovery | 03 |
| 05 | Donation Requests and Reservations | 03, 04 |
| 06 | Delivery and Handover | 05 |
| 07 | Administration and Reporting | 02, 05, 06 |
| 08 | Notifications and Release | Core modules |

The final specification boundaries may be adjusted if Kiro identifies a better implementation sequence. Changes must remain consistent with the approved PRD and SAD and must be reviewed before adoption.

## 7.2 Kiro operating rules

Kiro must:

- Read the approved project steering files before implementation.
- Follow the accepted PRD and SAD.
- Preserve the approved architecture.
- Avoid introducing unapproved dependencies.
- Use existing code and conventions rather than duplicating functionality.
- Implement meaningful tests alongside functionality.
- Report files created or modified.
- Report tests executed and their results.
- Identify unresolved issues.
- Avoid silently changing business requirements.
- Request clarification when requirements conflict or are incomplete.
- Follow the requirements → design → tasks specification sequence.
- Wait for approval before implementing a feature.
- Avoid marking tasks complete merely because code has been generated.

## 7.3 Human approval gates

The following checkpoints require review before proceeding:

| Gate | Approval required |
|---|---|
| G1 | Project structure and technology configuration |
| G2 | Authentication and authorisation design |
| G3 | Organisation, membership and database entity relationships |
| G4 | Donation reservation and cancellation logic |
| G5 | Handover and delivery-fee agreement workflow |
| G6 | Production infrastructure and deployment |
| G7 | Final acceptance testing |

The product owner retains final approval authority.

Changes to approved business rules, technology choices, architecture, database design, security controls or infrastructure require explicit approval.

Git commits, pushes, destructive operations and production deployments must also follow the agreed approval process.

---

# 8. Quality Assurance and Definition of Done

A feature is considered complete only when:

1. It satisfies the approved requirements.
2. Its implementation follows the accepted architecture.
3. Backend validation is implemented.
4. Security and permission checks are implemented.
5. Relevant automated tests pass.
6. Error conditions are handled appropriately.
7. The frontend is integrated with the actual backend.
8. The feature has been manually tested.
9. Relevant documentation is updated.
10. The changes have been reviewed and approved.
11. The approved changes are committed to Git.

## 8.1 MVP release criteria

The Last Plate MVP must demonstrate this complete journey:

1. An individual user registers and establishes or joins an organisation.
2. The organisation selects either the Service Provider or Service Consumer role.
3. The organisation submits its verification information.
4. An administrator approves the organisation.
5. An authorised Service Provider user creates a food donation listing.
6. An approved Service Consumer discovers the listing.
7. The Service Consumer submits a donation request.
8. The Service Provider approves or rejects the request.
9. Approved quantities are reserved correctly.
10. Both parties agree on collection or delivery arrangements.
11. Where a delivery fee applies, the Service Consumer explicitly accepts it.
12. The food is handed over.
13. Both parties confirm the handover.
14. The platform records the completed donation.
15. The platform reflects the activity in its impact reporting.

The demonstration must use the actual application workflows, not static screens or simulated backend responses presented as real functionality.

---

# 9. Risk Management

| Risk | Impact | Mitigation |
|---|---|---|
| AWS configuration delays | High | Start provisioning and account checks early |
| Cognito integration complexity | High | Validate token flow before building protected features |
| Database/PostGIS configuration | Medium | Test geographical queries during foundation work |
| Quantity over-allocation | Critical | Use transactional reservation logic and concurrency tests |
| Frontend/backend integration delays | High | Agree API contracts before dependent UI work |
| SES sending restrictions | Medium | Validate sending permissions early and maintain a test notification strategy |
| Kiro credit consumption | Medium | Use focused specifications and monitor usage |
| Incomplete testing | High | Reserve Saturday for end-to-end validation |
| Deployment failure | High | Perform an early deployment smoke test |
| Scope expansion | High | Defer all P2 and P3 features until P0 workflows work |
| Incorrect organisation permissions | High | Test organisation membership, role and approval enforcement |
| Unclear cancellation or fee rules | High | Agree business rules during specification review before implementation |

## 9.1 Scope protection

If the schedule becomes constrained, implementation must prioritise:

1. Authentication and organisation approval.
2. Organisation membership and authorisation.
3. Food listing creation.
4. Nearby discovery.
5. Donation requests and provider approval.
6. Quantity reservation.
7. Collection and handover.
8. Essential administration and trust management.
9. Deployment and end-to-end validation.

Optional dashboard enhancements, advanced reporting and visual extras must not delay the core donation workflow.

---

# 10. Cost and Infrastructure Considerations

The AWS architecture must be cost-conscious.

Before provisioning production infrastructure, validate:

- Service availability in the selected AWS region.
- Estimated monthly costs.
- Database instance and storage costs.
- Application hosting costs.
- S3 storage and transfer costs.
- SES sending requirements.
- Public access and HTTPS configuration.
- Free-tier or promotional eligibility, if applicable.

The final hosting service must be selected based on compatibility, deployment simplicity, cost and continued availability during judging.

No assumption should be made that a service is free simply because it offers a free tier.

The frontend and backend hosting decisions must be validated early enough to allow a deployment smoke test before the final release milestone.

---

# 11. Competition Deliverables

The implementation must also support the Kiroween submission requirements.

Expected deliverables include:

- Public GitHub repository.
- Open-source licence.
- Committed `.kiro/` directory.
- Working application URL.
- README with setup and usage instructions.
- Demonstration accounts and credentials where required.
- Actual demonstration video under three minutes.
- Accurate description of Kiro's contribution.
- Appropriate attribution for third-party assets and services.
- Application availability during the judging period.

The demonstration must show the actual functionality implemented.

---

# 12. Completion and Handover

At the end of implementation, the project must have:

- A working frontend.
- A working Spring Boot backend.
- A functioning PostgreSQL database with PostGIS support.
- Cognito authentication.
- Organisation registration and approval.
- Individual user accounts and organisation membership.
- Organisation role and permission enforcement.
- Food listing and discovery.
- Donation request and approval workflows.
- Quantity reservation controls.
- Collection and delivery arrangements.
- Delivery-fee agreement where applicable.
- Handover confirmation.
- Essential administration and trust-management capabilities.
- Basic impact reporting.
- Email notifications.
- Automated tests.
- Production deployment.
- Documentation and competition presentation material.

Any unfinished requirements must be explicitly recorded rather than represented as completed.

---

# 13. Document Control

| Item | Value |
|---|---|
| Document | Technical Implementation Plan |
| Version | 1.1 |
| Status | For Review |
| Supersedes | TIP v1.0 |
| Product | Last Plate |
| Reference PRD | v1.1 |
| Reference SAD | v1.1 |
| Target MVP completion | 28 November 2026 |

This document becomes the active implementation plan once reviewed and accepted. Changes to the implementation scope, priorities or technical baseline must be reviewed against the approved PRD and SAD.