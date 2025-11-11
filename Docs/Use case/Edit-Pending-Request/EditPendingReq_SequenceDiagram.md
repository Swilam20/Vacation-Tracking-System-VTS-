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
