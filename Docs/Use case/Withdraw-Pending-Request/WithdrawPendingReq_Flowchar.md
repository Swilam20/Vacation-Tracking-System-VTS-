```mermaid
flowchart TB
    EStart([Start: Employee selects pending request to withdraw])
    WithdrawConfirm([Confirm withdraw request])
    WithdrawDone([State set to withdrawn])
    RemoveFromManager([Remove request from manager's pending list])
    SendEmail([Send notification to Manager])
    ReturnHome([Return to VTS Home Page])

    %% Flow
    EStart --> WithdrawConfirm
    WithdrawConfirm -- Confirmed --> WithdrawDone --> RemoveFromManager --> SendEmail --> ReturnHome
    WithdrawConfirm -- Cancel --> ReturnHome
