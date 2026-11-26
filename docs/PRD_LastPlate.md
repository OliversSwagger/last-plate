# Last Plate – Product Requirements Document (PRD)

**Version:** 1.1  
**Status:** Accepted  
**Initiative:** Y2iH (Year To Improve Humanity)  
**Competition:** Kiroween 2026 – Costume Contest

---

## 1. Product Overview

### 1.1 Product Name

Last Plate

### 1.2 Product Vision

Last Plate is a food rescue platform that connects organisations with surplus edible food to soup kitchens and community feeding organisations that need it.

The platform enables Service Providers to publish available surplus food, while Service Consumers can discover nearby donations, request suitable quantities and arrange collection or delivery.

Last Plate aims to reduce edible food waste while making surplus food more accessible to organisations feeding people in need.

### 1.3 Problem Statement

Organisations such as supermarkets, restaurants, bakeries and food distributors can have surplus edible food that is still suitable for consumption but may go unused or be discarded.

At the same time, soup kitchens and community feeding organisations need access to food donations but may struggle to discover available donations, coordinate collection and arrange delivery.

Last Plate aims to connect these two groups through a simple, transparent and accessible digital platform.

### 1.4 Product Objectives

1. Make surplus food donations easier to discover.
2. Connect Service Providers with nearby Service Consumers.
3. Simplify donation requests and approval.
4. Support flexible collection and delivery arrangements.
5. Record completed food donations and quantities recovered.
6. Improve visibility into the platform's social and environmental impact.

---

## 2. Target Users

### 2.1 Service Providers

Organisations with suitable surplus edible food that they wish to make available to other organisations.

Examples include:
- Restaurants.
- Supermarkets and grocery stores.
- Bakeries.
- Hotels and caterers.
- Farms and agricultural businesses.
- Food manufacturers and distributors.

Primary capabilities:
- Register and manage a Service Provider organisation profile.
- Publish surplus food donations.
- Specify quantities, deadlines and collection arrangements.
- Review incoming donation requests.
- Approve or reject requests.
- Confirm completed handovers.
- Manage users associated with their organisation.

### 2.2 Service Consumers

Organisations that receive food donations to support soup kitchens and community feeding activities.

Examples include:
- Soup kitchens.
- Community kitchens.
- Non-profit organisations.
- Community feeding programmes.
- Other eligible organisations supporting people in need.

Both registered and unregistered organisations may apply.

Primary capabilities:
- Register and manage a Service Consumer organisation profile.
- Discover available nearby food donations.
- Filter donations according to requirements.
- Request available food quantities.
- Track request and collection status.
- Confirm received donations.
- Report problems or discrepancies.
- Manage users associated with their organisation.

### 2.3 Organisation Users

Individuals access Last Plate through their own user accounts and act on behalf of an associated organisation.

Examples include:
- Employees of a supermarket managing food donations.
- Restaurant staff responsible for surplus food listings.
- Community kitchen coordinators managing donation requests.
- Representatives responsible for collecting donated food.

Primary capabilities:
- Register and authenticate individually.
- Associate their account with an organisation.
- Access functionality according to their assigned permissions.
- Perform activities on behalf of their organisation.

An individual user account does not automatically constitute an independent Service Provider or Service Consumer organisation.

### 2.4 Platform Administrators

Responsible for the operation, safety and administration of Last Plate.

Primary capabilities:
- Review and approve organisation registrations.
- Manage user and organisation accounts.
- Monitor food listings and donations.
- Investigate reports and disputes.
- Suspend or reactivate accounts.
- Access operational and impact reports.
- Review administrative audit history.

---

## 3. Product Scope

### 3.1 MVP Scope

The first release must provide a complete working donation lifecycle:

1. User registration and authentication.
2. Organisation registration and verification.
3. Food donation listing and management.
4. Nearby food discovery.
5. Donation requests and provider approval.
6. Quantity reservation and availability management.
7. Collection and delivery coordination.
8. Handover confirmation.
9. Trust and safety administration.
10. Dashboards and impact reporting.
11. Email notifications.

### 3.2 Out of Scope

The following features are excluded from the initial release:

- Integrated payment processing.
- Driver or volunteer delivery marketplace.
- Automatic driver allocation.
- Route optimisation.
- AI-powered food matching.
- Native Android or iOS applications.
- Advanced warehouse or inventory management.
- Multi-location organisation accounts.
- Automated identity verification integrations.
- External organisation registry integrations.
- In-platform chat or messaging.
- Multi-country support.
- Independent individual food-provider accounts.

These features may be considered for future releases.

---

## 4. Functional Requirements

### FR-01: User Registration and Authentication

The system must:

1. Allow users to register using an email address and password through AWS Cognito.
2. Support email verification.
3. Allow users to sign in and sign out securely.
4. Support password recovery.
5. Distinguish between Service Provider, Service Consumer and administrator roles.
6. Associate users with their respective organisation.
7. Enforce role-based permissions.
8. Prevent users belonging to pending or rejected organisations from accessing restricted donation operations.

**Acceptance criteria:**
- A user can register and authenticate successfully.
- An unverified email cannot be treated as verified.
- Users can only access functionality permitted by their role.
- Authentication alone does not grant organisation approval.

### FR-02: Organisation Management and Verification

The system must:

1. Allow organisations to register as either a Service Provider or a Service Consumer.
2. Support one organisation/location per account.
3. Capture organisation name, type, platform role, contact details and operating location.
4. Allow applicable registration information and supporting documents to be submitted.
5. Support registered and unregistered community kitchens.
6. Allow administrators to review applications.
7. Support approval, rejection and requests for additional information.
8. Record verification status and administrative decisions.
9. Notify applicants of relevant status changes by email.
10. Allow individual users to be associated with their respective organisations.
11. Prevent an organisation from registering as both a Service Provider and a Service Consumer under the same organisation profile.

Organisation verification statuses:

- Pending
- Approved
- Rejected
- Suspended
- Additional information required

NPO registration must not be mandatory for every community kitchen.

**Acceptance criteria:**
- An organisation can submit a registration application with its selected platform role.
- An administrator can review and make a decision.
- Pending organisations cannot publish or request donations.
- Approved organisations can access their permitted functionality according to their platform role.
- Rejected and suspended organisations cannot perform restricted operations.
- Administrative decisions are recorded.
- Individual users can be associated with an approved organisation.
- An organisation cannot operate as both a Service Provider and Service Consumer through the same organisation profile.

### FR-03: Food Donation Listings

The system must allow approved Service Providers to create and manage donation listings.

Each listing must support:

- Food title.
- Description.
- Food category.
- Quantity available.
- Unit of measurement.
- Food preparation or packaging date, where applicable.
- Use-by or best-before date, where applicable.
- Storage requirements.
- Relevant allergen information, where known.
- Food photographs.
- Collection deadline.
- Collection location.
- Delivery arrangement.
- Optional delivery fee.

Food categories must accommodate suitable surplus food, including prepared meals and fresh produce.

Service Providers must be able to:
- Create listings.
- Edit listings.
- View listing availability.
- Withdraw listings where permitted.
- View incoming requests.

**Acceptance criteria:**
- An approved Service Provider can publish a donation.
- Required food information is validated.
- Available quantities cannot be negative.
- Listings can no longer be requested after their collection deadline or withdrawal.
- Listings with approved requests cannot be withdrawn in a way that silently invalidates existing commitments.

### FR-04: Food Discovery

The system must allow approved Service Consumers to discover available donations.

Discovery must:
1. Prioritise nearby food listings.
2. Display relevant food information.
3. Support filtering by food category.
4. Support distance filtering.
5. Support collection deadline filtering.
6. Display available quantities.
7. Display collection and delivery arrangements.
8. Indicate listing availability and request status.

The initial experience will use a list-based interface rather than requiring an interactive map.

Exact collection addresses must only be disclosed to authorised recipients after the relevant request has been approved.

**Acceptance criteria:**
- Service Consumers can discover available nearby donations.
- Filters return relevant results.
- Expired, withdrawn and fully reserved donations cannot be requested.
- Private location information is not exposed prematurely.

### FR-05: Donation Requests and Approval

The system must allow an approved Service Consumer to request food donations.

A request must capture:
- Donation listing reference.
- Requested quantity.
- Intended collection or delivery arrangement.
- Relevant delivery fee agreement, where applicable.
- Additional notes, if required.

Service Providers must be able to approve or reject each request.

The system must:
1. Notify Service Providers of incoming requests.
2. Notify Service Consumers of decisions.
3. Prevent approved requests from exceeding available quantities.
4. Reserve approved quantities.
5. Release reserved quantities when an approved request is cancelled or otherwise legitimately closed without handover.
6. Maintain request history.

**Acceptance criteria:**
- A Service Consumer can submit a request for an available donation.
- The Service Provider can approve or reject it.
- Approval reserves the requested quantity.
- Concurrent requests cannot cause over-allocation.
- Rejected requests do not reserve food.
- Both parties can see the current request status.

### FR-06: Collection and Delivery Coordination

The system must support three arrangements:

1. **Recipient collection:** The Service Consumer collects the donation.
2. **Free provider delivery:** The Service Provider voluntarily delivers the donation at no charge.
3. **Paid provider delivery:** The Service Provider offers delivery for an agreed fee.

For paid delivery:
- The Service Provider specifies the proposed fee.
- The Service Consumer sees the fee before accepting the arrangement.
- The Service Consumer explicitly agrees to the fee.
- Changes to the fee require renewed agreement.
- Payment occurs outside Last Plate.
- The platform records the agreed fee and arrangement.

Last Plate must not represent an external payment as verified simply because a user records it.

**Acceptance criteria:**
- The parties can identify the agreed collection or delivery arrangement.
- A paid delivery fee cannot be accepted without explicit agreement.
- Fee changes require renewed consent.
- The platform records the agreed arrangement.
- No integrated payment functionality is required.

### FR-07: Donation Handover

The system must record the actual transfer of donated food.

Each donation handover must include:
- Unique donation reference.
- Service Provider.
- Service Consumer.
- Requested quantity.
- Approved quantity.
- Actual quantity handed over.
- Collection or delivery arrangement.
- Handover date and time.
- Service Provider confirmation.
- Service Consumer confirmation.

Both parties must confirm completion.

Where quantities differ or either party reports a problem, the handover must be flagged for review.

**Acceptance criteria:**
- Every approved donation has a traceable reference.
- Both parties can confirm handover.
- Actual quantities are recorded.
- Discrepancies can be reported.
- Completed donations are included in impact reporting.
- Handover history cannot be silently overwritten.

### FR-08: Trust and Safety

The system must provide basic administrative controls to protect participants.

It must support:
- Organisation approval.
- Account suspension and reactivation.
- Reporting of suspicious listings or behaviour.
- Donation disputes.
- Food information declarations.
- Administrative investigation.
- Audit history.

Service Providers must declare that listed food is suitable for donation and that relevant handling and storage requirements have been followed.

Last Plate must not claim to certify food safety or guarantee that donated food is safe to consume.

Verification must distinguish between organisation registration checks and any separate food-safety requirements.

**Acceptance criteria:**
- Users can report concerns.
- Administrators can investigate reports.
- Administrators can suspend accounts.
- Administrative actions are recorded.
- Food-safety information is visible to relevant participants.

### FR-09: Dashboards

The system must provide role-specific dashboards.

**Service Provider dashboard**
- Active food listings.
- Pending donation requests.
- Approved donations.
- Completed handovers.
- Food quantities successfully donated.

**Service Consumer dashboard**
- Nearby available donations.
- Pending requests.
- Approved requests.
- Upcoming collections or deliveries.
- Completed donations.

**Administrator dashboard**
- Pending organisation applications.
- Approved and rejected organisations.
- Active users.
- Active food listings.
- Donation activity.
- Reports and disputes.
- Platform impact indicators.

### FR-10: Impact Reporting

The system must capture and report:

- Total food listed.
- Total food successfully handed over.
- Number of completed donations.
- Number of participating Service Providers.
- Number of participating Service Consumers.
- Donation activity by food category.
- Donation activity over selected time periods.

Reports must distinguish between food listed, requested, approved and actually handed over.

Meal-equivalent estimates must only be introduced when supported by a documented conversion methodology. The system must not invent meal counts from donated food quantities.

---

## 5. Donation Lifecycle and Business Rules

### 5.1 Donation Lifecycle

A donation follows this general lifecycle:

Available → Request Pending → Approved / Reserved → Handover In Progress → Completed

Alternative outcomes include:

- Rejected
- Cancelled
- Expired
- Disputed
- Withdrawn

The system must maintain a traceable history of status transitions.

### 5.2 Core Business Rules

**BR-01:** Only approved Service Provider organisations may publish food donations, and only approved Service Consumer organisations may request donations.

**BR-02:** A Service Provider must approve every donation request.

**BR-03:** An approved request must reserve the requested quantity.

**BR-04:** Total reserved quantities must never exceed the available quantity.

**BR-05:** A donation cannot be requested after its deadline or withdrawal.

**BR-06:** Paid delivery requires explicit agreement from the Service Consumer.

**BR-07:** Delivery payments take place outside the platform.

**BR-08:** Both parties must confirm handover completion.

**BR-09:** Quantity discrepancies must be reportable.

**BR-10:** Administrative decisions and important donation status changes must be auditable.

**BR-11:** Exact collection details must only be disclosed to authorised participants.

**BR-12:** Organisation registration and food-safety compliance must not be treated as the same verification process.

**BR-13:** An organisation must register under one platform role: Service Provider or Service Consumer.

**BR-14:** Individual users must be associated with an organisation to perform organisation-specific donation operations. An individual user account does not independently qualify as a Service Provider or Service Consumer organisation.

---

## 6. Email Notifications

The system must send email notifications for important events, including:

- Registration and email verification.
- Organisation application submission.
- Organisation approval or rejection.
- Requests for additional organisation information.
- New donation requests.
- Request approval or rejection.
- Collection or delivery coordination updates.
- Handover confirmation.
- Dispute or report updates where appropriate.

Email is the only communication channel within the initial release. No in-platform messaging system will be implemented.

---

## 7. Non-Functional Requirements

### 7.1 Security
- Secure authentication through AWS Cognito.
- Backend authorisation independent of frontend visibility.
- Role-based access control.
- Secure storage of sensitive information.
- Protection of uploaded documents.
- Input validation and appropriate error handling.
- Audit logging for important actions.

### 7.2 Performance
- Nearby food discovery should return results efficiently.
- Pagination should be supported for listings and administrative views.
- Database queries must avoid unnecessary loading of large datasets.

### 7.3 Usability
- Responsive desktop, tablet and mobile layouts.
- Clear navigation for each user role.
- Simple donation creation and request workflows.
- Accessible forms and meaningful validation messages.
- Consistent visual language.

### 7.4 Reliability
- Donation quantities must remain consistent during concurrent requests.
- Important state changes must be persisted.
- Failed email delivery must not silently invalidate a successful donation transaction.
- Errors must be logged and traceable.

### 7.5 Maintainability
- Modular application structure.
- Clear separation of business logic and infrastructure.
- Consistent coding conventions.
- Automated tests for important business rules.
- Documented API contracts.

### 7.6 Privacy
- Only collect information required for platform operations.
- Restrict access to organisation documents and contact information.
- Avoid exposing exact collection addresses before approval.
- Apply appropriate retention and access controls to personal information.

---

## 8. User Roles and Permissions

| Capability | Service Provider | Service Consumer | Administrator |
|---|:---:|:---:|:---:|
| Manage own profile | Yes | Yes | Yes |
| Publish food listings | Yes | No | Oversight |
| Discover food | No | Yes | Oversight |
| Request donations | No | Yes | Oversight |
| Approve donation requests | Yes | No | Oversight |
| Confirm handover | Yes | Yes | Oversight |
| Manage organisation users | Own organisation | Own organisation | All |
| Manage organisations | Own organisation | Own organisation | All |
| Approve organisations | No | No | Yes |
| Investigate reports | No | No | Yes |
| Suspend accounts | No | No | Yes |
| View platform reports | Own activity | Own activity | All |

All permissions must be enforced by the backend.

Individual users access these capabilities through their association with an organisation and their assigned permissions.

---

## 9. MVP Acceptance Criteria

The initial release will be considered functionally complete when:

1. Users can register and authenticate.
2. Organisations can submit registration applications as either Service Providers or Service Consumers.
3. Administrators can approve, reject or suspend organisations.
4. Approved Service Providers can create and manage food listings.
5. Approved Service Consumers can discover nearby donations.
6. Service Consumers can request specific food quantities.
7. Service Providers can approve or reject requests.
8. The system prevents over-allocation of food.
9. Collection and delivery arrangements can be agreed and recorded.
10. Both parties can confirm completed handovers.
11. Disputes and reports can be submitted and investigated.
12. Role-specific dashboards display relevant information.
13. Impact reports reflect actual completed donations.
14. Email notifications are delivered for important workflow events.
15. The application is accessible through a publicly deployed URL.
16. The complete core donation workflow can be demonstrated successfully.

---

## 10. Future Considerations

Features that may be considered after the competition include:

- Delivery partner and volunteer networks.
- Integrated payment and sponsorship contributions.
- Advanced geographic matching.
- External organisation verification services.
- Automated food donation recommendations.
- Multi-location organisation support.
- Native mobile applications.
- More advanced impact analytics.
- Independent individual food-provider accounts, if the platform model is expanded.

These are not commitments for the initial release.

---

## 11. Product Success Measures

The initial release should measure:

- Number of approved Service Providers.
- Number of approved Service Consumers.
- Number of food listings created.
- Number of donation requests.
- Number of completed handovers.
- Total quantity of food successfully recovered.
- Percentage of approved requests successfully completed.
- Time between listing publication and successful handover.

The primary impact measure is **the quantity of food successfully handed over**, not simply the quantity advertised on the platform.

---

## 12. Document Approval

This PRD defines the agreed functional scope and product behaviour for Last Plate's initial release.