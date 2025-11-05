```mermaid
flowchart TB
  %% Swimlane-like layout using subgraphs
  subgraph Employee
    direction TB
    EStart([Start: Employee logs into VTS])
    ViewHome[[View VTS Home Page<br/>shows balances & requests]]
    CreateReq([Create new vacation request])
    FillDates([Select dates & hours<br/>Enter title & description])
    Submit([Submit request])
    Validation{Validation OK?}
    ShowErrors([Show errors - highlight fields])
    ReturnHome1([Return to VTS Home Page])
    EditChoice{Edit / Withdraw / Cancel?}

    %% Edit pending request details
    EditWithdraw{withdraw?}
    EditReq([Edit pending request<br/>change title/comments/dates])
    EditValidation{Validation OK?}
    EditError([Redisplay edit page<br/>highlight & explain problems])
    EditSaved(["Changes accepted and saved"])
    ReturnHome2([Return to VTS Home Page - update summaries])

    %% Withdraw flow (separate)
    WithdrawConfirm(["Confirm withdraw request"])
    WithdrawDone(["State set to withdrawn"])
    WithdrawRemoveFromManager(["Remove request from manger list"])
    WithdrawSendEmaiManager(["Send notification email to manager"])
    %% Cancel flow
    CancelSelect(["Select approved/future request to cancel"])
    CancelCheck{Is request<br/>in future or recent past?}
    CancelInvalid(["Display error:<br/>Request cannot be canceled<br/>(not recent past or future)"])
    CancelConfirm(["Confirm cancel (future)<br/>or confirm + reason (recent past)"])
    AbortCancel(["Abort cancellation - no changes made"])
    RestoreTime(["Return time allowance to employee"])
    SendCancelEmail(["Send notification to manager"])
    CancelDone(["State set to canceled"])
  end

  subgraph Manager
    direction TB
    MStart(["Trigger: Notification received or Manager logs into VTS"])
    ManagerHome[[Manager VTS Home Page<br/>shows pending approvals]]
    ReviewReq([Open pending request details])
    Approve{Approve or Reject?}
    RejectionReason([Enter rejection reason])
    NotifyEmployee([Notify employee via e-mail])
    ReturnHomeM([Return to Manager Home Page])
  end

  %% Employee main flow
  EStart --> ViewHome --> CreateReq --> FillDates --> Submit --> Validation
  Validation -- No --> ShowErrors --> FillDates
  Validation -- Yes --> ReturnHome1
  Submit -->|If approval required for new request| SendEmail["Send notification email to manager"]

  %% Manager flow
  SendEmail --> MStart
  MStart --> ManagerHome --> ReviewReq --> Approve
  Approve -- Approve --> NotifyEmployee --> ReturnHomeM
  Approve -- Reject --> RejectionReason --> NotifyEmployee --> ReturnHomeM
  NotifyEmployee --> ReturnHome1

  %% Alternate employee flows
  ViewHome --> EditChoice

  %% Edit branch (cleaned)
  EditChoice -- Edit pending --> EditWithdraw 
  EditWithdraw  -- No--> EditReq --> EditValidation
  EditWithdraw  -- Yes --> WithdrawConfirm
  EditValidation -- No --> EditError --> EditReq
  EditValidation -- Yes --> EditSaved --> ReturnHome2

  %% Withdraw branch
  EditChoice -- Withdraw pending --> WithdrawConfirm -->|Confirmed| WithdrawDone --> WithdrawRemoveFromManager --> WithdrawSendEmaiManager -->ReturnHome2
  WithdrawConfirm -->|Cancel| ReturnHome2
  WithdrawSendEmaiManager -->MStart
  %% Cancel branch with validation and abort
  EditChoice -- Cancel approved --> CancelSelect --> CancelCheck
  CancelCheck -- No --> CancelInvalid --> ReturnHome2
  CancelCheck -- Yes --> CancelConfirm
  CancelConfirm -->|Confirmed| RestoreTime --> SendCancelEmail --> CancelDone --> ReturnHome2
  CancelConfirm -->|Abort| AbortCancel --> ReturnHome2

  %% Notifications
  SendCancelEmail --> MStart

