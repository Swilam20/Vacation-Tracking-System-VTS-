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

    VACATIONREQUEST {
        int Request_ID PK
        string Title
        string Description
        int Category_ID FK
        date From_Date
        date To_Date
        float Hours
        string Status
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
