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
