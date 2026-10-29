# IT Risk and Compliance Management System – Requirements v1.0

## 1. Project Overview

**Project name:** IT Risk and Compliance Management System  
**Organisation:** Mvelo Logistics (Pty) Ltd (fictional)  
**Project type:** Portfolio web application  
**Primary framework:** ASP.NET Core MVC  
**Database:** SQL Server  
**Security framework:** NIST Cybersecurity Framework (CSF) 2.0

## 2. Background and Problem Statement

Mvelo Logistics (Pty) Ltd is a fictional, medium-sized South African logistics company with approximately 200 employees, a head office in Johannesburg and two depots in Gauteng.

The organisation currently manages its IT risks using spreadsheets. This makes it difficult to identify the most serious risks, monitor security controls, track corrective actions and determine who made changes to risk records.

The proposed system will provide a central place to record IT risks, assess their severity, document controls, manage corrective actions and monitor outstanding risks. It will also maintain an audit trail of important changes to support accountability and internal reviews.

The application is being developed as a portfolio project to demonstrate skills in information systems, database design, web development, IT risk management, access control and cybersecurity governance.

## 3. Project Objectives

The system aims to:

1. Maintain a central register of IT risks.
2. Calculate inherent and residual risk scores using a consistent scoring method.
3. Display risk severity through a dashboard and a 5×5 risk heat map.
4. Record security controls and map them to relevant NIST CSF 2.0 categories.
5. Track corrective actions, assigned owners, deadlines and progress.
6. Maintain an audit trail showing who changed a record, when it was changed and what changed.
7. Restrict access to information and functions according to user roles.
8. Provide reports that help users understand the organisation's risk position.
9. Demonstrate secure development practices, automated testing and clear technical documentation.

## 4. User Roles and Permissions

The system will have three roles: Admin, Risk Owner and Auditor.

### 4.1 Admin

The Admin manages users and has access to all risk management functions.

An Admin can:

- Create user accounts and assign roles.
- Deactivate user accounts instead of deleting them.
- View, create and edit any risk.
- Assign and reassign risk owners.
- Manage security controls, including creating, editing and retiring controls.
- Create and manage corrective actions.
- View the organisation-wide dashboard, reports and audit trail.
- View and manage records across the system.
- Reopen closed risks by changing their status to Assessed.

User accounts will be created by an Admin. Self-registration will not be available.

### 4.2 Risk Owner

A Risk Owner is responsible for managing risks assigned to them and following up on related corrective actions.

A Risk Owner can:

- View risks assigned to them.
- Create new risks, which will automatically be assigned to them.
- Edit risks assigned to them.
- Link existing security controls to their own risks.
- View existing security controls but cannot create, edit or retire them.
- Create corrective actions for risks they own.
- View and update corrective actions assigned directly to them or linked to risks they own, subject to the permissions and status rules of the application.
- View dashboard information and reports relating only to their own risks and related actions.

A Risk Owner cannot:

- Edit another owner's risk.
- Reassign risks to other users.
- Manage user accounts.
- Create, edit or retire security controls.
- View the organisation-wide audit trail.
- Reopen closed risks.

Access restrictions must be enforced by the server-side application, not only by hiding buttons or pages in the interface.

### 4.3 Auditor

The Auditor has read-only access to risk management records for review and monitoring.

An Auditor can:

- View all risks and their assessments.
- View security controls and their mappings.
- View corrective actions and their statuses.
- View the organisation-wide dashboard and reports.
- View the audit trail.

An Auditor cannot create, edit or delete risk management records, manage users or change system data.

### 4.4 Access Control Summary

| Function | Admin | Risk Owner | Auditor |
|---|---|---|---|
| Create user accounts | Yes | No | No |
| Deactivate user accounts | Yes | No | No |
| View all risks | Yes | No | Yes |
| Create risks | Yes | Yes | No |
| Edit any risk | Yes | No | No |
| Edit own assigned risks | Yes | Yes | No |
| Reassign risk owners | Yes | No | No |
| View security controls | Yes | Yes | Yes |
| Create and edit controls | Yes | No | No |
| Link existing controls to risks | Yes | Yes, own risks only | No |
| Retire controls | Yes | No | No |
| Create corrective actions | Yes | Yes, own risks only | No |
| Manage all corrective actions | Yes | No | No |
| Update permitted corrective actions | Yes | Yes, assigned or linked to own risks | No |
| View organisation-wide dashboard and reports | Yes | No | Yes |
| View own risks and related dashboard information | Yes | Yes | No |
| View audit trail | Yes | No | Yes |
| Edit or delete audit records | No | No | No |

The permissions in this table will be enforced through application authorisation rules. Admins and Auditors can view audit records, but neither role can edit or delete those records through the application.

Risk Owners will only see their own risks and related corrective actions throughout the application. This restriction applies to dashboard totals, charts, reports, heat maps and record lists. They must not receive organisation-wide totals or information about other owners' risks.

## 5. Project Scope

### 5.1 Included in Version 1

The first version will include the following features.

**Risk Register**

- Create, view and edit risk records according to role permissions.
- Record a risk title, description, category, affected asset or system, risk owner and status.
- Record inherent and residual likelihood, impact and scores.
- Store risk treatment notes and assessment justifications.
- Track the dates on which risks are created and updated.
- Allow Admins to reassign risk owners.
- Prevent risks from being hard-deleted through the application. Risks that are no longer active must be closed with a recorded reason.

**Risk Scoring**

- Calculate inherent risk scores.
- Calculate residual risk scores.
- Assign severity levels using defined score bands.
- Validate residual ratings against inherent ratings.
- Require a written justification when residual ratings differ from inherent ratings.
- Set residual likelihood and impact equal to inherent likelihood and impact when a new risk is created. This is a default value and does not mean that the risk has been fully assessed.
- Exclude risks that have not been fully assessed from the main assessed-risk heat map, or clearly distinguish them from assessed risks.

**Risk Heat Map**

- Display assessed risks on a 5×5 likelihood-and-impact heat map.
- Use residual risk ratings for the main view, with inherent ratings available for comparison.
- Display the number of risks in each heat map cell.
- Allow users to select a cell to view the risks within that likelihood-and-impact combination.
- Apply role-based access restrictions when displaying risks in the selected cell.
- Allow users to identify high-priority risks visually.

**Security Controls**

- Record control names, descriptions and implementation details.
- Map controls to relevant NIST CSF 2.0 categories.
- Link controls to risks.
- Allow Risk Owners to link existing controls to their own risks without changing the control details.
- Allow Admins to create, edit and retire controls.
- Use the following control statuses:
  - Planned
  - Implemented
  - Requires Attention
- Prevent controls from being hard-deleted through the application. Controls that are no longer applicable must be retired.

**Corrective Actions**

- Create actions to address risks or control weaknesses.
- Assign an action owner and due date.
- Track action status and progress notes.
- Allow Risk Owners to create corrective actions for risks they own.
- Allow Risk Owners to update actions assigned to them or linked to risks they own, subject to the applicable permissions.
- Allow Admins to manage all corrective actions.
- Use the following corrective action statuses:
  - Open
  - In Progress
  - Completed
  - Cancelled
- Calculate overdue actions using the due date and completion status. Overdue will be displayed as a calculated condition, not stored as a separate status.
- Prevent corrective actions from being hard-deleted through the application. Actions that will no longer be pursued must be cancelled.

**Audit Trail**

- Record important create, update, status-change and reassignment operations.
- Record user account creation, role changes and account deactivation.
- Capture the user, timestamp, operation, affected record and relevant old and new values.
- Include changes to risks, controls and corrective actions.
- Include risk closure, reopening, control retirement and action cancellation.
- Restrict audit trail viewing to Admins and Auditors.
- Prevent audit records from being edited or deleted through the application.

**Dashboard and Reports**

- Show the total number of risks within the user's permitted view.
- Summarise risks by severity and status.
- Highlight high and critical residual risks.
- Show overdue corrective actions.
- Provide a report summarising risks, controls and corrective actions.
- Restrict Risk Owners to information about their own risks and related actions.
- Allow Admins and Auditors to view organisation-wide information.

**Methodology Page**

- Explain the risk scoring method.
- Define the severity bands.
- Explain the difference between inherent and residual risk.
- Explain the purpose and limitations of the NIST CSF 2.0 mappings.

### 5.2 Excluded from Version 1

The following features are outside the initial scope:

- ISO 27001 control mapping.
- Email and SMS notifications.
- PDF report generation.
- Support for multiple organisations.
- Automated risk scoring using machine learning.
- Complex risk acceptance approval workflows.
- Integration with external security monitoring tools.

These features may be considered for future versions after the main system is complete and tested.

## 6. Risk Assessment Methodology

The system will use a likelihood-and-impact approach to assess risk. This is a project-defined scoring method for the demonstration application, not a claim that every organisation or framework uses the same scale.

### 6.1 Likelihood and Impact

Both likelihood and impact will be rated on a scale from 1 to 5.

| Rating | Likelihood | Impact |
|---|---|---|
| 1 | Rare | Insignificant |
| 2 | Unlikely | Minor |
| 3 | Possible | Moderate |
| 4 | Likely | Major |
| 5 | Almost Certain | Severe |

Likelihood represents how likely an event is to occur. Impact represents the expected seriousness of its consequences.

### 6.2 Risk Score

The risk score will be calculated as:

**Risk Score = Likelihood × Impact**

The lowest possible score is 1 and the highest is 25.

The system will calculate the score automatically from the selected ratings.

### 6.3 Severity Bands

The following bands will be used throughout the application.

| Score | Severity |
|---|---|
| 1–5 | Low |
| 6–12 | Medium |
| 13–19 | High |
| 20–25 | Critical |

These severity bands are specific to this project. They will be documented on the methodology page and used consistently in the dashboard, heat map and reports.

### 6.4 Inherent and Residual Risk

**Inherent risk** is the risk level before considering the effect of existing controls.

**Residual risk** is the remaining risk after considering the effectiveness of controls and other treatment measures.

The user assessing the risk will enter the residual likelihood and impact ratings. The application will calculate the residual score from those ratings. It will not automatically reduce the residual score based on the number of controls recorded.

When a new risk is created, its residual likelihood and impact will initially be set equal to its inherent likelihood and impact. This provides default values while the risk is being assessed. It does not mean that the residual assessment has been completed.

Residual ratings must not exceed the corresponding inherent ratings:

- Residual likelihood must be less than or equal to inherent likelihood.
- Residual impact must be less than or equal to inherent impact.

This means the residual score cannot exceed the inherent score. If either residual rating differs from its corresponding inherent rating, the assessor must provide a written justification explaining the difference.

The application will validate these rules on the server side.

Risks that have not been fully assessed will not be presented as confirmed assessments on the main risk heat map. They will either be excluded from the assessed-risk heat map or clearly identified as unassessed.

### 6.5 Worked Example

A fictional internet-facing server has the following inherent risk assessment:

- Inherent likelihood: 4 — Likely
- Inherent impact: 5 — Severe
- Inherent score: 4 × 5 = 20
- Inherent severity: Critical

The organisation implements patch management and firewall restrictions. After reviewing the controls, the assessor determines that the likelihood has decreased.

The residual assessment is:

- Residual likelihood: 2 — Unlikely
- Residual impact: 5 — Severe
- Residual score: 2 × 5 = 10
- Residual severity: Medium

The assessor must document why the likelihood has decreased from 4 to 2 and why the impact remains at 5.

The example illustrates how the application records an assessment. It does not automatically prove that the controls are effective.

## 7. Risk Statuses and Transitions

Each risk will have a status to show its current position in the risk management process.

### 7.1 Risk Status Definitions

| Status | Description |
|---|---|
| Identified | The risk has been recorded but may not have a complete assessment. |
| Assessed | The risk has been assessed and its ratings have been recorded. |
| Treatment in Progress | Actions are being taken to reduce or manage the risk. |
| Accepted | The organisation has formally accepted the remaining risk, with a recorded justification. |
| Closed | The risk is no longer active and has been closed with a recorded reason. |

### 7.2 Allowed Status Transitions

The application will validate risk status changes according to the following rules.

| Current status | Allowed next status |
|---|---|
| Identified | Assessed, Closed |
| Assessed | Treatment in Progress, Accepted, Closed |
| Treatment in Progress | Assessed, Accepted, Closed |
| Accepted | Assessed, Closed |
| Closed | Assessed — Admin only |

A risk cannot move to a status that is not allowed in the table.

Only an Admin can reopen a closed risk. Reopening a risk changes its status to Assessed and creates an audit record.

### 7.3 Required Justifications

- A risk moving to Accepted must have an acceptance justification.
- A risk moving to Closed must have a closure reason.
- Reopening a closed risk must be recorded in the audit trail.
- All status changes must record the previous status, new status, user and timestamp.

For Version 1, accepting a risk will require a justification but will not require a separate approval workflow.

## 8. NIST Cybersecurity Framework Mapping

The system will use the NIST Cybersecurity Framework (CSF) 2.0 as a reference for organising security controls.

Controls can be mapped to relevant CSF 2.0 categories to help users understand which cybersecurity outcomes they support.

The application will provide the mapping as a reference rather than treating it as proof of compliance. Mapping a control to a NIST CSF 2.0 category does not establish that the organisation has implemented the control effectively or complies with the framework.

The project will document the limitations of its mapping and avoid claiming that the application certifies compliance.

## 9. Technology Stack and Application Design

The initial implementation will use the following technologies:

| Technology | Purpose |
|---|---|
| C# | Main programming language |
| ASP.NET Core MVC | Web application framework |
| .NET 10 LTS | Application runtime and framework |
| Entity Framework Core | Database access and object-relational mapping |
| SQL Server | Relational database |
| ASP.NET Core Identity | Authentication, user accounts and role management |
| HTML, CSS and Bootstrap | Page structure and responsive styling |
| JavaScript | Client-side interaction |
| Chart.js | Dashboard charts and visualisations |
| xUnit | Automated unit testing |
| Git and GitHub | Version control and source code hosting |

The application will use a layered structure to separate controllers, business logic, data access and presentation where appropriate.

### 9.1 Concurrent Editing

The Risks database table will include a `RowVersion` concurrency token.

This will allow the application to detect when two users attempt to update the same risk record at the same time. If one user saves changes before the other, the second user's save must be rejected or handled through a concurrency warning rather than silently overwriting the first user's changes.

The application will inform the user that the record has been changed and that they should reload the latest version before making further changes.

### 9.2 Configuration and Secrets

Sensitive configuration, such as database credentials, will not be committed to the repository.

Development configuration will be managed using appropriate local configuration and secret management practices.

## 10. Security Requirements

Security will be considered throughout development.

The application will:

- Require users to log in before accessing protected pages.
- Use role-based authorisation.
- Enforce record-level ownership rules on the server.
- Validate inputs and enforce business rules on the server.
- Use Entity Framework Core parameterised database operations rather than constructing unsafe SQL queries.
- Use ASP.NET Core Identity for password handling and account management.
- Prevent self-registration.
- Deactivate user accounts instead of deleting them.
- Prevent risks, controls and corrective actions from being hard-deleted through the application.
- Protect audit records from modification and deletion through the application.
- Avoid storing passwords in plain text.
- Keep secrets and credentials out of source control.
- Include tests for unauthorised access and invalid operations.

The audit trail will provide application-level accountability. It will not be described as tamper-proof against database administrators or people with direct access to the underlying database.

## 11. Demo Data and Test Accounts

The application will use fictional demonstration data based on Mvelo Logistics (Pty) Ltd.

The seeded data will include examples of risks, controls, corrective actions and different risk severity levels so that the dashboard and heat map can be demonstrated without requiring users to create all records manually.

Demo accounts will be provided for the Admin, Risk Owner and Auditor roles. Their credentials will be clearly labelled as demonstration-only and documented safely for local testing.

The application will not use real employee information, real company risk records or real credentials.

## 12. Testing and Validation

Automated tests and manual checks will be used to verify the system's main business rules and access restrictions.

Testing will include:

**Risk Scoring and Validation**

- Correct risk score calculations.
- Correct severity classification at the boundaries of each score band.
- Correct default residual ratings when a new risk is created.
- Validation that residual likelihood and impact do not exceed their corresponding inherent ratings.
- Rejection of residual rating changes without a justification.
- Exclusion or clear identification of unassessed risks on the assessed-risk heat map.

**Risk Status Management**

- Correct handling of allowed risk status transitions.
- Rejection of invalid status transitions.
- Requirement for an acceptance justification when a risk is accepted.
- Requirement for a closure reason when a risk is closed.
- Prevention of Risk Owners and Auditors reopening closed risks.
- Correct audit records when risks are accepted, closed or reopened.

**Role-Based Access Control**

- Correct role-based access to application features.
- Prevention of Risk Owners editing risks assigned to other users, including through direct server requests.
- Prevention of Risk Owners linking controls to risks they do not own.
- Prevention of unauthorised control creation, editing and retirement.
- Prevention of unauthorised corrective action updates.
- Prevention of unauthorised access to the audit trail.
- Correct filtering of dashboard, report and heat map information according to user permissions.

**Audit Trail**

- Creation of audit entries containing the relevant user, timestamp, operation and old and new values.
- Recording of user creation, role changes and account deactivation.
- Recording of risk, control and corrective action changes.
- Prevention of audit record edits and deletions through the application.

**Other Application Functions**

- Correct display of seeded risks on the dashboard and heat map.
- Correct counting of risks in heat map cells.
- Correct filtering of risks when a heat map cell is selected.
- Correct calculation of overdue corrective actions.
- Detection of conflicting updates through the `RowVersion` concurrency token.
- Prevention of hard deletion of risks, controls and corrective actions through the application.

The tests will include both successful operations and operations that must be rejected.

## 13. Success Criteria

The project will be considered complete for Version 1 when:

1. Users can log in and access only the functions permitted by their roles.
2. Admins can manage user accounts, risks, owners, controls and corrective actions.
3. Risk Owners can manage their own risks and permitted corrective actions without editing other owners' risks.
4. Risk Owners can link existing controls to their own risks without changing control details.
5. Auditors can view relevant records and the audit trail without changing system data.
6. The application calculates risk scores and severity levels correctly.
7. New risks receive default residual ratings equal to their inherent ratings.
8. Residual ratings cannot exceed the corresponding inherent ratings.
9. The application requires justification when residual ratings differ from inherent ratings.
10. Risk status transitions follow the defined rules.
11. Acceptance justifications and closure reasons are required where applicable.
12. The dashboard and 5×5 heat map display the correct risk information according to user permissions.
13. Heat map cells display risk counts and allow users to view the relevant risks.
14. Controls can be mapped to relevant NIST CSF 2.0 categories.
15. Corrective action statuses and overdue calculations work as defined.
16. Important changes create audit records that cannot be edited or deleted through the application.
17. User creation, role changes and account deactivation are recorded in the audit trail.
18. Conflicting risk updates are detected instead of silently overwriting existing changes.
19. Risks, controls and corrective actions cannot be hard-deleted through the application.
20. Automated tests cover the main scoring, validation and access control rules.
21. The GitHub repository includes a README with setup instructions, technology details, test instructions, demo account guidance and screenshots.
22. The application can be run locally using the documented instructions.

## 14. Project Limitations

This application is a portfolio demonstration and is not intended to be used as a production compliance or enterprise risk management system.

It will use fictional data and a simplified risk assessment methodology. The NIST CSF 2.0 mappings will provide guidance but will not prove compliance. The application will also depend on users entering accurate risk assessments, control information and remediation updates.

The audit trail will record application-level changes but will not provide protection against direct database manipulation by privileged users.

A production deployment would require further security review, operational monitoring, backup and recovery procedures, access reviews, deployment hardening and validation against the organisation's actual risk management policies.

## 15. Future Improvements

Possible improvements after Version 1 include:

- ISO 27001 mapping.
- Email notifications for overdue corrective actions.
- PDF report generation.
- More detailed risk treatment plans.
- Risk acceptance approval workflows.
- Additional dashboard filters and report options.
- Deployment to a cloud environment.
- Improved automated integration and security testing.

These improvements will only be considered after the Version 1 requirements have been implemented and tested.

## 16. Project Deliverables

The final portfolio project will include:

- A working ASP.NET Core MVC web application.
- A SQL Server database with migrations and fictional seed data.
- Authentication and role-based access control.
- Risk register, scoring, heat map and dashboard.# IT Risk and Compliance Management System: Project Brief

For the full rules, see [requirements.md](requirements.md).

## Organisation
Mvelo Logistics (Pty) Ltd is a fictional, medium-sized South African logistics
company (about 200 employees, a head office in Johannesburg and two depots in
Gauteng).

## Problem
IT risks are tracked in spreadsheets. It is hard to see which risks matter most,
monitor controls, track corrective actions, or know who changed what.

## Solution
A web application that records IT risks, scores them, links them to controls
mapped to NIST CSF 2.0, tracks corrective actions, and keeps an audit trail.

## Roles
- **Admin:** manages users, risks, controls and actions.
- **Risk Owner:** manages their own risks and related actions only.
- **Auditor:** read-only access, including the audit trail.

## Scoring method
Risk score = Likelihood x Impact, each rated 1 to 5.

| Score | Severity |
|---|---|
| 1-5 | Low |
| 6-12 | Medium |
| 13-19 | High |
| 20-25 | Critical |

Residual ratings are entered by the assessor, cannot exceed the inherent
ratings, and need a written justification when they differ.

Example: inherent 4 x 5 = 20 (Critical). After patching and firewall rules,
residual 2 x 5 = 10 (Medium).

## Technology
C#, ASP.NET Core MVC (.NET 10 LTS), SQL Server, Entity Framework Core,
ASP.NET Core Identity, Bootstrap, Chart.js, xUnit, Git and GitHub.

## Status
Phase 1: database design in progress.

## Note
This is a portfolio demonstration using fictional data. It is not a production
compliance tool.
- Security control and corrective action management.
- Audit trail and reports.
- Automated tests for important business rules.
- A README with installation and usage instructions.
- Screenshots or a demonstration video.
- A clear explanation of the methodology, security considerations and limitations.

The project will demonstrate the practical application of information systems, database development, cybersecurity governance, IT risk management and secure web development.