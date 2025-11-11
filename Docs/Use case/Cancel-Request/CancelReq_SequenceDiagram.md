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
