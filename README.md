## Project Overview
Vacation Tracking System (VTS) will provide individual employees with the capability to manage their own vacation time, sick leave, and personal time off

## Introduction

- In modern organizations, employee independence has increased significantly. It is now common for workers to divide their time across multiple projects and report to several managers. As a result, managers have fewer informal interactions with their team members and find it increasingly difficult to monitor and manage vacation schedules effectively.

- This lack of centralized visibility often leads to overlapping absences, manual tracking errors, and administrative delays. The Vacation Tracking System (VTS) is intended to address these challenges by providing a unified digital platform for managing employee leave efficiently and transparently.

## Vision Statement

- The Vacation Tracking System (VTS) will empower employees to manage their own vacation time, sick leave, and personal time off without needing detailed knowledge of company or facility policies. It will streamline HR operations, reduce non-core administrative tasks for managers, and foster a greater sense of autonomy and transparency across the organization.

## Business Goals

- Automate the vacation request process to replace the existing manual approach.
- Accelerate approval workflows to reduce processing time from several days to near real-time.
- Simplify the process for employees to submit vacation requests, including urgent cases.
- Ensure reliability by preventing loss or mismanagement of submitted requests.
- Provide visibility for employees into their time-off history and upcoming leave plans.
- Enable managers to easily view team availability and plan resource allocation.
- Reduce operational costs and increase HR department efficiency through automation and digital record-keeping.

## Scope

- The Vacation Tracking System (VTS) will focus on automating and streamlining the vacation and leave management process within the organization. The system aims to provide web-based access for employees and managers to handle vacation requests, approvals, and tracking efficiently.

### In Scope

- Develop a web-based application accessible through standard browsers.
- Integrate with existing legacy and HR systems to retrieve employee information and update leave balances.
- Provide functionality for employees to request vacation, sick leave, and personal time off.
- Enable managers to review, approve, or reject vacation requests.
- Maintain leave history and provide visibility of team availability.


## Major Features

The Vacation Tracking System (VTS) will include the following key features:

### Rules-Based Validation

- Implements a flexible, rules-driven system to validate and verify employee leave requests according to company policy.

### Manager Approval Workflow

- Supports optional manager approval before finalizing vacation requests, ensuring proper oversight.

### Historical and Future Requests

- Provides access to vacation records from the previous calendar year and allows employees to submit requests up to 18 months in advance.

### Email Notifications

- Sends automated emails to notify managers of pending approvals and employees of status updates.

### Integration with Existing Infrastructure

- Uses the organization’s existing hardware, middleware, and intranet portal for deployment and authentication (via single sign-on).

### Comprehensive Logging

- Maintains detailed activity logs for all transactions and approvals to support auditing and traceability.

### Administrative Overrides

- Allows HR and system administrators to override restrictions when necessary, with all overrides logged.

### Manager-Granted Leave

- Enables managers to directly award personal leave time to employees within predefined system limits.

### Web Service Interface

- Exposes a service endpoint for internal systems to query an employee’s vacation summary programmatically.

### HR System Integration

- Interfaces with legacy HR systems to synchronize employee details, leave balances, and updates in real time.

## Assumption

The following assumptions are considered true for the successful development and deployment of the Vacation Tracking System (VTS):

- All employees and managers have access to the company intranet and valid login credentials.
- An existing HR system and employee database are available for integration.
- Email infrastructure is already configured and supports automated notifications.
- Company leave policies are already defined and can be represented as system rules.
- Each employee has a unique identifier (e.g., Employee ID) in the HR database.
- Users will access the system using modern browsers (Chrome, Edge, Firefox).
- The organization has sufficient server resources to host the web application.

## Constraints

- The following constraints define the limitations and conditions under which the Vacation Tracking System (VTS) will be designed, developed, and deployed:
- The system must be developed using the existing organizational infrastructure and middleware — no new hardware or major software acquisitions are permitted.
- The solution must integrate seamlessly with the existing HR system and other legacy systems already in use.
- The system must send automated email notifications to employees and managers regarding request status changes.
- The initial release will be web-based only; mobile platforms are excluded from the first phase.
- User authentication must utilize the organization’s existing Single Sign-On (SSO) mechanism.
- All data must comply with organizational privacy, security, and data retention policies.
- The project must be delivered within the approved timeline and allocated budget.

# Actors

##	The following are the primary actors that directly interact with the Vacation Tracking System (VTS):

### Employee
 - A regular system user who requests, views, and manages their own vacation, and sick leave.
 - Responsibilities / Interactions:
	- Submit new leave requests.
	- View available leave balances.
	- Track the status of pending and approved requests.
	- Cancel or modify requests before approval.

### Manager
 - A supervisor or team leader responsible for reviewing and approving employee leave requests.
 - Responsibilities / Interactions:
	- Review pending leave requests submitted by employees.
	- Approve, reject, or comment on requests.
	- View team leave schedules and availability.
	- Award additional personal leave days (within system limits).

### HR Clerk (HR Staff)
 - A member of the Human Resources department who ensures compliance with company leave policies and maintains employee leave data.
 - Responsibilities / Interactions:
	- Review and adjust employee leave balances.
	- ensure employees information in all HR systems is up to date and correct
	- Override system restrictions when necessary.
	- Maintain policy configurations within the system.

### System Administrator
 - A technical user responsible for maintaining system configurations.
 - Responsibilities / Interactions:
	- Monitor system performance and logs.
	- Handle system backup and recovery.


## Functional Requirements

### The Vacation Tracking System (VTS) shall provide the following core functionalities:

#### Integration with HR Systems

- The system shall integrate with existing HR and legacy systems to retrieve employee data and update leave balances in real time.

#### Rules-Based Validation

- The system shall implement a configurable rules engine to validate and verify all vacation and leave requests in accordance with company leave policies.

#### Manager Approval Workflow

- The system shall allow managers to review, approve, reject, or comment on leave requests submitted by employees.
- Manager approval shall be optional based on company policy.

#### Historical and Future Requests

- The system shall allow employees to view leave requests from the previous calendar year and submit new requests up to 18 months in advance.

#### Email Notifications

- The system shall automatically send email notifications to:
  - Managers when new leave requests require their approval.
  - Employees when the status of their request changes (approved, rejected, or modified).


#### Administrative Overrides

- The system shall allow authorized HR and administrative personnel to override leave restrictions or system rules.

#### Manager-Granted Leave

- The system shall allow managers to award additional personal leave days to employees within predefined system limits.

#### Leave Summary Interface

- The system shall provide a user interface for employees to view their leave balances, request history, and current request status.

#### Single-sign-on mechanisms

- The system shall be implemented as an extension to the existing company intranet portal and shall utilize the organization’s Single Sign-On (SSO) mechanism for all authentication.

#### Web Service Interface

- The system shall expose a web service API that enables other internal systems to query employee vacation summaries and leave information.

#### Activity Logging

- The system shall record all key transactions, including requests, approvals, rejections, and overrides, in an activity log for traceability and auditing purposes.

## Non-Functional Requirements

### The following requirements describe how the system will perform and interact with other systems.

#### Use of Existing Infrastructure

- The system shall be deployed using the organization’s existing hardware, middleware, and database infrastructure to minimize cost and ensure compatibility.


#### Usability and User Experience

- The system shall provide an intuitive, user-friendly interface that minimizes the learning curve for all user roles.

## ERD Diagram
```mermaid
erDiagram
    EMPLOYEE {
        int Employee_ID PK
        string Name
        int Managed_By FK "references EMPLOYEE.Employee_ID"
        string Department
    }

    VACATIONCATEGORY {
        int Category_ID PK
        string Name
        string Description
    }

    TIMEBALANCE {
        int Balance_ID PK
        int Employee_ID FK
        int Category_ID FK
        float Hours_Remaining
    }

    REQUESTSTATUS {
        int Status_ID PK
        string Code "e.g., PENDING, APPROVED, REJECTED, COMPLETED"
        string Description
    }

    VACATIONREQUEST {
        int Request_ID PK
        string Title
        string Description
        int Category_ID FK
        date From_Date
        date To_Date
        float Hours
        int Status_ID FK "references REQUESTSTATUS.Status_ID"
        string Explanation
        datetime Request_Timestamp
        datetime Last_Modified
        int Employee_ID FK
        int Manager_ID FK
    }

    NOTIFICATION {
        int Notification_ID PK
        string Type
        datetime Timestamp
        string Status
        int Request_ID FK
        int Employee_ID FK
    }

    AUDITLOG {
        int Audit_ID PK
        string Action
        int Request_ID FK
        int Employee_ID FK
        int Manager_ID FK
        datetime Request_Timestamp
        datetime Processing_Timestamp
        string Status
    }

    %% Relationships
    EMPLOYEE ||--o{ VACATIONREQUEST : "submits"
    EMPLOYEE ||--o{ VACATIONREQUEST : "approves"
    EMPLOYEE ||--o{ TIMEBALANCE : "has"
    EMPLOYEE ||--o{ NOTIFICATION : "receives"
    EMPLOYEE ||--o{ AUDITLOG : "performs"
    EMPLOYEE ||--o{ EMPLOYEE : "manages (self-ref)"

    VACATIONCATEGORY ||--o{ VACATIONREQUEST : "categorizes"
    VACATIONCATEGORY ||--o{ TIMEBALANCE : "linked to"

    TIMEBALANCE }o--|| EMPLOYEE : "belongs to"
    TIMEBALANCE }o--|| VACATIONCATEGORY : "for category"

    VACATIONREQUEST ||--o{ NOTIFICATION : "triggers"
    VACATIONREQUEST ||--o{ AUDITLOG : "logged in"

    REQUESTSTATUS ||--o{ VACATIONREQUEST : "defines status"
```
## Use Case

### Create-Request

#### Flowchart
```mermaid
flowchart TB
    EStart([Start: Employee logs into VTS])
    ViewHome[[View VTS Home Page<br/>shows balances & requests]]
    CreateReq([Create new vacation request])
    FillDates([Select dates & hours<br/>Enter title & description])
    Submit([Submit request])
    Validation{Validation OK?}
    ShowErrors([Show errors - highlight & correct fields])
    ReturnHome([Return to VTS Home Page])
    SendEmail([If approval required, send notification to Manager])

    %% Flow
    EStart --> ViewHome --> CreateReq --> FillDates --> Submit --> Validation
    Validation -- No --> ShowErrors --> FillDates
    Validation -- Yes --> ReturnHome
    Submit --> SendEmail
```
#### Sequence Diagram
```mermaid
sequenceDiagram
    participant Employee
    participant VTS_System as VTS System
    participant DB as Database
    participant Email as Email Service
    participant Manager

    Employee->>VTS_System: Log in via intranet portal
    VTS_System-->>Employee: Display balances & existing requests

    Employee->>VTS_System: Create new vacation request
    VTS_System-->>Employee: Display vacation categories and calendar
    Employee->>VTS_System: Select category, dates, hours, title, and description
    VTS_System->>VTS_System: Validate request data

    alt Validation fails
        VTS_System-->>Employee: Show form errors and request corrections
    else Validation passes
        VTS_System->>DB: Save new request (state: Pending approval)
        VTS_System-->>Employee: Return to VTS Home Page (request pending)
        note right of VTS_System: Async background task triggered
        VTS_System-->>Email: Send notification to Manager
        Email-->>Manager: Notify about pending approval
    end
```

### Edit-Pending-Request

#### Flowchart
```mermaid
flowchart TB
    EStart([Start: Employee selects pending request to edit])
    EditReq([Edit pending request<br/>change title/comments/dates])
    EditValidation{Validation OK?}
    EditError([Redisplay edit page<br/>highlight & explain problems])
    EditSaved([Changes accepted and saved])
    ReturnHome([Return to VTS Home Page - summaries updated])

    %% Flow
    EStart --> EditReq --> EditValidation
    EditValidation -- No --> EditError --> EditReq
    EditValidation -- Yes --> EditSaved --> ReturnHome
```
#### Sequence Diagram
```mermaid
sequenceDiagram
    participant Employee
    participant VTS_System as VTS System
    participant DB as Database
    participant Email as Email Service
    participant Manager

    %% Step 1–2: Employee logs in and views requests
    Employee->>VTS_System: Log in via intranet portal
    VTS_System-->>Employee: Display VTS Home Page<br/>with summaries & pending requests

    %% Step 3: Select request to edit
    Employee->>VTS_System: Select pending vacation request to edit
    VTS_System->>DB: Retrieve request details
    DB-->>VTS_System: Return request data

    %% Step 4: Display editable request form
    VTS_System-->>Employee: Display editable request<br/>(title, comments, dates, withdraw option)

    %% Step 5: Employee edits or withdraws
    Employee->>VTS_System: Submit changes or choose to withdraw

    alt Employee chooses to withdraw
        %% Withdraw confirmation flow
        VTS_System-->>Employee: Prompt confirmation to withdraw
        Employee->>VTS_System: Confirm withdraw
        VTS_System->>DB: Update request state → Withdrawn
        VTS_System-->>Employee: Return to VTS Home Page (updated)
        note right of VTS_System: Async background task
        VTS_System-->>Email: Send notification email to Manager
        Email-->>Manager: Notify about withdrawn request

    else Employee submits changes
        %% Validation logic
        VTS_System->>VTS_System: Validate modified data
        alt Validation fails
            VTS_System-->>Employee: Redisplay edit page<br/>Highlight and explain errors
        else Validation succeeds
            VTS_System->>DB: Update request details
            DB-->>VTS_System: Acknowledge update
            VTS_System-->>Employee: Return to VTS Home Page (changes saved)
        end
    end
```

### Cancel-Request

#### Flowchart
```mermaid
flowchart TB
    EStart([Start: Employee selects approved request to cancel])
    CancelCheck{Is request in future or recent past?}
    CancelInvalid([Display error: cannot cancel])
    CancelConfirm([Confirm cancel / provide reason])
    RestoreTime([Return time allowance to employee])
    SendEmail([Send notification to Manager])
    CancelDone([State set to canceled])
    AbortCancel([Abort cancellation - no changes made])
    ReturnHome([Return to VTS Home Page])

    %% Flow
    EStart --> CancelCheck
    CancelCheck -- No --> CancelInvalid --> ReturnHome
    CancelCheck -- Yes --> CancelConfirm
    CancelConfirm -- Confirmed --> RestoreTime --> SendEmail --> CancelDone --> ReturnHome
    CancelConfirm -- Abort --> AbortCancel --> ReturnHome
```
#### Sequence Diagram
```mermaid
sequenceDiagram
    participant Employee
    participant VTS_System as VTS System
    participant DB as Database
    participant Email as Email Service
    participant Manager

    %% Step 1–2: Employee logs in and views requests
    Employee->>VTS_System: Log in via intranet portal
    VTS_System-->>Employee: Display summary of approved and pending requests

    %% Step 3: Employee selects a request to cancel
    Employee->>VTS_System: Select vacation request to cancel
    VTS_System->>DB: Retrieve request details
    DB-->>VTS_System: Return request data

    %% Validation inside VTS
    VTS_System->>VTS_System: Validate request (approved + future/recent past)

    alt Request invalid
        VTS_System-->>Employee: Display error<br/>"Request cannot be canceled (not recent past or future)"
        VTS_System-->>Employee: Return to VTS Home Page
    else Request valid
        %% Step 4: Confirmation
        VTS_System-->>Employee: Prompt confirmation<br/>(and reason if recent past)
        Employee->>VTS_System: Confirm cancellation (+ explanation if required)

        %% Step 5: System processes cancellation
        VTS_System->>DB: Update request state → Canceled
        VTS_System->>DB: Restore time allowance to employee’s balance
        DB-->>VTS_System: Acknowledge update

        %% Step 6: Employee returned to home page
        VTS_System-->>Employee: Return to VTS Home Page (updated summary)

        %% Step 7: Async email notification
        note right of VTS_System: Async background task
        VTS_System-->>Email: Send cancellation notification to Manager
        Email-->>Manager: Notify about canceled vacation request
    end
```

### Withdraw-Pending-Request

#### Flowchart
```mermaid
flowchart TB
    EStart([Start: Employee selects pending request to withdraw])
    WithdrawConfirm([Confirm withdraw request])
    WithdrawDone([State set to withdrawn])
    RemoveFromManager([Remove request from manager's pending list])
    SendEmail([Send notification to Manager])
    ReturnHome([Return to VTS Home Page])

    %% Flow
    EStart --> WithdrawConfirm
    WithdrawConfirm -- Confirmed --> WithdrawDone --> RemoveFromManager --> SendEmail --> ReturnHome
    WithdrawConfirm -- Cancel --> ReturnHome
```
#### Sequence Diagram
```mermaid
sequenceDiagram
    participant Employee
    participant VTS_System as VTS System
    participant DB as Database
    participant Email as Email Service
    participant Manager

    %% Step 1–2: Employee logs in and views current requests
    Employee->>VTS_System: Log in via intranet portal
    VTS_System-->>Employee: Display summary of vacation requests and balances

    %% Step 3–4: Employee selects request to withdraw
    Employee->>VTS_System: Select pending request to withdraw
    VTS_System-->>Employee: Prompt confirmation to withdraw
    Employee->>VTS_System: Confirm withdrawal

    %% Step 5–6: System processes withdrawal
    VTS_System->>DB: Update request state → Withdrawn
    VTS_System-->>Employee: Return to VTS Home Page (updated summary)

    %% Step 7: Async notification to manager
    note right of VTS_System: Async background task triggered
    VTS_System-->>Email: Send withdrawal notification to Manager
    Email-->>Manager: Notify about withdrawn request
```

### Manager-Approval

#### Flowchart
```mermaid
flowchart TB
    MStart([Start: Manager receives notification or logs into VTS])
    ManagerHome[[View pending vacation requests]]
    ReviewReq([Open request details])
    Approve{Approve or Reject?}
    RejectionReason([Enter rejection reason])
    NotifyEmployee([Send notification to employee])
    ReturnHome([Return to Manager Home Page])

    %% Flow
    MStart --> ManagerHome --> ReviewReq --> Approve
    Approve -- Approve --> NotifyEmployee --> ReturnHome
    Approve -- Reject --> RejectionReason --> NotifyEmployee --> ReturnHome
```
#### Sequence Diagram
```mermaid
sequenceDiagram
    participant Manager
    participant VTS
    participant Employee

    Manager->>VTS: Receive notification or log in
    VTS->>Manager: Display pending vacation requests (ManagerHome)
    Manager->>VTS: Select and open request details (ReviewReq)
    VTS->>Manager: Show request details
    Manager->>VTS: Approve or Reject request (Approve)
    
    alt Approve
        VTS-)Employee: Send approval notification asynchronously (NotifyEmployee)
        VTS->>Manager: Return to Manager Home Page (ReturnHome)
    else Reject
        Manager->>VTS: Enter rejection reason (RejectionReason)
        VTS-)Employee: Send rejection notification asynchronously (NotifyEmployee)
        VTS->>Manager: Return to Manager Home Page (ReturnHome)
    end
```

## State Machine Diagram For Request
```mermaid
stateDiagram-v2
    [*] --> Draft : Employee creates request
    Draft --> Pending_Approval : Employee submits request

    Pending_Approval --> Approved : Manager approves
    Pending_Approval --> Rejected : Manager rejects
    Pending_Approval --> Withdrawn : Employee withdraws
    Pending_Approval --> Pending_Approval : Employee edits request

    Approved --> Canceled : Employee cancels (future/recent)
    Approved --> Completed : Vacation period ends

    Rejected --> [*]
    Withdrawn --> [*]
    Canceled --> [*]
    Completed --> [*]

```

## Initial View for Vacation Requests

### Employee Perspective
- The following interface illustrates how an employee can view their vacation requests within the system.

<img width="872" height="530" alt="image" src="https://github.com/user-attachments/assets/98c915af-3904-4e94-a175-d5b3d7257c4e" />


### Manager Perspective

-This interface shows how a manager can view and manage vacation requests for team members, with the option to act as an employee for his own requests.

<img width="637" height="397" alt="image" src="https://github.com/user-attachments/assets/838eb6fb-91ad-4d3e-a9ee-9be373328719" />


