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
