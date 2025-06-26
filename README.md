# Mermaid Diagram Example

This repository constitutes  a single README file to practice Mermaid.js diagram syntax.

### Sequence Diagram
---
A ***simple sequence*** diagram of a Log-in use case.
```mermaid
sequenceDiagram
    actor User
    participant UI as Login Page
    participant API as Controller
    participant DB as Database
    
    User->>UI: enterCredentials()
    activate User
    User->>UI: submitCredentials()
    deactivate User
    activate UI
    UI->>API: processCredentials()
    deactivate UI
    activate API
    API->>DB: checkCredentials()
    deactivate API
    activate DB
    DB-->>API: returnResult()
    deactivate DB
    activate API
    alt isValid
    API-->>UI: logInSuccessful() 
    activate UI
    UI-->>User: redirectToHome()
    deactivate UI
    else isNotValid
    API-->>UI: logInUnsuccessful()
    activate UI
    UI-->User: displayError()
    deactivate UI
    deactivate API
    end
```

### Entity Relational Diagram
---
An ***ERD*** of 3 entities (User, Course, and Enrollment)
``` mermaid
erDiagram
    USER ||--o{ ENROLLMENT: "has"
    USER ||--o{ COURSE: "teaches"
    COURSE || 
```