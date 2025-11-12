```mermaid
stateDiagram-v2
    [*] --> Pending_Approval : Employee submits request

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
