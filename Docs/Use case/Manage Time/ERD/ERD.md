```mermaid
erDiagram
    EMPLOYEE ||--o{ VACATIONREQUEST : submits
    EMPLOYEE ||--o{ TIMEBALANCE : has
    EMPLOYEE ||--o{ NOTIFICATION : receives
    EMPLOYEE ||--o{ AUDITLOG : performs
    EMPLOYEE ||--o{ VACATIONREQUEST : approves

    VACATIONCATEGORY ||--o{ VACATIONREQUEST : "categorized as"
    VACATIONCATEGORY ||--o{ TIMEBALANCE : "tracked by"

    VACATIONREQUEST ||--o{ NOTIFICATION : triggers
    VACATIONREQUEST ||--o{ AUDITLOG : recorded_in

    EMPLOYEE {
        int employee_id PK
        string name
        string email
        string role
        string department
        int manager_id FK
    }

    VACATIONREQUEST {
        int request_id PK
        int employee_id FK
        int manager_id FK
        int category_id FK
        string title
        string description
        date start_date
        date end_date
        string status
        date creation_date
        date last_modified_date
    }

    VACATIONCATEGORY {
        int category_id PK
        string name
        string description
        int max_days_per_year
    }

    TIMEBALANCE {
        int balance_id PK
        int employee_id FK
        int category_id FK
        int total_allowed_days
        int used_days
        int remaining_days
    }

    NOTIFICATION {
        int notification_id PK
        int request_id FK
        int recipient_id FK
        string message
        date sent_date
        string status
    }

    AUDITLOG {
        int log_id PK
        int request_id FK
        int action_by FK
        string action
        string notes
        date timestamp
    }
