# 🧜‍♀️ Mermaid.js Sandbox
![Ariel](https://images.genius.com/b246eacb8eb8a9a01a0ed79ed9273040.690x388x41.gif)

> This repository constitutes a single README file to practice Mermaid.js diagram syntax.


### I. Sequence Diagram
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

### II. Process Flowchart of a Log-in Feature
---
``` mermaid
flowchart TD
  Start([Start])
  subgraph Frontend [Blazor Client]
    A[LoginComponent: User enters username & password]
    B[HttpClient POST /api/auth/login]
  end

  subgraph Backend [ASP.NET Core Web API]
    C[AuthController.Login(LoginDto dto)]
    D[AuthService.ValidateUser(dto)]
    E[UserRepository.GetByUsername(dto.Username)]
    F[EF Core: DbContext.Users.SingleOrDefault(...)]
    G{user == null \nor password invalid?}
    H[Return 401 Unauthorized]
    K[TokenService.CreateToken(user)]
    L[AuthController returns 200 OK + { token }]
  end

  subgraph Database [SQL Server via EF Core]
    M[(Users Table)]
  end

  subgraph FrontendPost [Blazor Client cont.]
    I[On success: Store JWT/token in local storage]
    J[Navigate to protected page]
    X[Display "Invalid credentials" message]
  end

  End([End])

  Start --> A
  A --> B

  B --> C
  C --> D
  D --> E
  E --> F
  F --> G

  G -->|Yes| H
  H --> X
  X --> A

  G -->|No| K
  K --> L
  L --> I
  I --> J
  J --> End
  F --> M
```

### III. Entity Relational Diagram
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

### IV. Back-end Directory Structure of a Simplified Udemy-based Web Application (Vertical Slice Architecture)
---
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



#### i. Bonus Side Project: General flowchart of the Modified Hippopotamus Optimization (MHO) Algorithm.
---
MHO (Han et al., 2025) is a modified metaheuristic algorithm based on the  Hippopotamus Optimization (MHO) Algorithm (Amiri et. al, 2024), to be used for my thesis, where it is to be modified and used to solve land allocation and harvest scheduling, benchmarked against established methodology.

```mermaid
flowchart TD

A([Start]) --> B[Input optimization problem]
    B --> C[Set N, T, t=1, i=1]
    C --> D[Initialize population with sine chaotic map]
    D --> E[Calculate objective function]
    E --> F[Update dominant hippopotamus]
    F --> G{i > N/2?}
    G -->|No| H[Calculate Xi^Mhippo & Xi^FBhippo]
    H --> I[Update Xi]
    I --> K
    G -->|Yes| L[Generate random predator position]
    L --> M[Calculate Xi^HippoR]
    M --> N[Update Xi]
    N --> K
    K[i = i+1] --> P{i <= N?}
    P -->|Yes| G
    P -->|No| Q[Set i=1]
    Q --> R[Calculate new bounds]
    R --> S[Calculate Xi^HippoE]
    S --> T[Update Xi]
    T --> U[i = i+1]
    U --> V{i <= N?}
    V -->|Yes| S
    V -->|No| W[Apply small-hole reverse learning]
    W --> X[Save best solution]
    X --> Y{t < T?}
    Y -->|Yes| Z[t = t+1, i=1]
    Z --> E
    Y -->|No| AA[Output best solution]
    AA --> AB([End])
```
> Lifted from https://www.nature.com/articles/s41598-024-54910-3
