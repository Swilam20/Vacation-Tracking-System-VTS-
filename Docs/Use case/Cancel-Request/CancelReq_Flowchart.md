```mermaid
flowchart TB
    EStart([Start: Employee selects approved request to cancel])
    CancelCheck{Is request in future or recent past?}
    CancelInvalid([Display error: cannot cancel])
    CancelConfirm([Confirm cancel / provide reason])
    RestoreTime([Return time allowance to employee])
    SendEmail([Send notification to Manager])
    CancelDone([State set to canceled])
    AbortCancel([Abort cancellation - no changes made])
    ReturnHome([Return to VTS Home Page])

    %% Flow
    EStart --> CancelCheck
    CancelCheck -- No --> CancelInvalid --> ReturnHome
    CancelCheck -- Yes --> CancelConfirm
    CancelConfirm -- Confirmed --> RestoreTime --> SendEmail --> CancelDone --> ReturnHome
    CancelConfirm -- Abort --> AbortCancel --> ReturnHome
