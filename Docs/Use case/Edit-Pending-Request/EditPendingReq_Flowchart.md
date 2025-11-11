```mermaid
flowchart TB
    EStart([Start: Employee selects pending request to edit])
    EditReq([Edit pending request<br/>change title/comments/dates])
    EditValidation{Validation OK?}
    EditError([Redisplay edit page<br/>highlight & explain problems])
    EditSaved([Changes accepted and saved])
    ReturnHome([Return to VTS Home Page - summaries updated])

    %% Flow
    EStart --> EditReq --> EditValidation
    EditValidation -- No --> EditError --> EditReq
    EditValidation -- Yes --> EditSaved --> ReturnHome
