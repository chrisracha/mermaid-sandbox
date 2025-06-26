# Mermaid Diagram Example
This repository constitutes a single README file to practice Mermaid.js diagram syntax.

### Sequence Diagram
---
A ***simple sequence diagram*** of a Log-in use case.
```mermaid
%% Sequence Diagram: Log-in Use Case
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
```mermaid
%% ERD: User, Course, Enrollment
erDiagram
    USER ||--o{ ENROLLMENT: "has"
    USER ||--o{ COURSE: "teaches"
    COURSE ||--o{ ENROLLMENT: "contains"

    USER {
        int user_id PK
        string first_name
        string last_name
        string email UK
        string password_hash
        string role "student/instructor"
        datetime created_at
    }
    
    COURSE {
        int course_id PK
        int instructor_id FK
        string title
        text description
        datetime created_at
        datetime updated_at
    }
    
    ENROLLMENT {
        int enrollment_id PK
        int student_id FK
        int course_id FK
        datetime enrolled_at
        string status "active/completed/dropped"
    }
```

> A complex system would require more entities such as payment, quiz, category, module, progress, etc.

### Back-end Directory Structure of a Simplified Udemy-based Web Application (Vertical Slice Architecture)

```text
# Directory Structure: Udemy-based Web Application (Blazor, .NET Core, Mediatr)

src/
├── Features/                      
│   ├── UserManagement/
│   │   ├── Account/              
│   │   │   └── Account.cs
│   │   ├── Login/
│   │   │   └── Login.cs
│   │   ├── SwitchRole/
│   │   │   └── SwitchRole.cs
│   ├── CourseManagement/
│   │   └── Course.cs
│   ├── Enrollment/
│   │   └── Enroll.cs
│   ├── CompleteCourse/
│   │   └── CompleteCourse.cs
│   ├── Payments/
│   │   ├── Checkout/
│   │   │   └── Checkout.cs
│   │   └── Webhooks/
│   │       └── StripeWebhook.cs
├── Infrastructure/                
│   ├── Persistence/
│   │   ├── ApplicationDbContext.cs
│   │   └── Migrations/
│   ├── Email/
│   └── FileStorage/
├── Domain/                        
│   ├── Users/
│   │   ├── User.cs
│   │   └── Role.cs
│   ├── Courses/
│   │   ├── Course.cs
│   │   └── Module.cs
│   └── Shared/
│       └── ValueObjects/
├── appsettings.json
├── Program.cs
└── ../../udemy-app                 
```