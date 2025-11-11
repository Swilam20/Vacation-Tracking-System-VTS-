```mermaid
flowchart TB
    EStart([Start: Employee logs into VTS])
    ViewHome[[View VTS Home Page<br/>shows balances & requests]]
    CreateReq([Create new vacation request])
    FillDates([Select dates & hours<br/>Enter title & description])
    Submit([Submit request])
    Validation{Validation OK?}
    ShowErrors([Show errors - highlight & correct fields])
    ReturnHome([Return to VTS Home Page])
    SendEmail([If approval required, send notification to Manager])

    %% Flow
    EStart --> ViewHome --> CreateReq --> FillDates --> Submit --> Validation
    Validation -- No --> ShowErrors --> FillDates
    Validation -- Yes --> ReturnHome
    Submit --> SendEmail
