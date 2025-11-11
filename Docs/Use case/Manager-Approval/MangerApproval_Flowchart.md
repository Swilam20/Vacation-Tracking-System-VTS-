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
