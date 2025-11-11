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
