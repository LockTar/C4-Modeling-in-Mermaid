# C4 Component Diagram - Mermaid Flowchart Cheatsheet

> Component diagrams show the internal structure of a container. Components represent modular, independently replaceable units within a single deployable container (classes, libraries, modules, etc.).

---

## Color Palette (C4 Blue Theme)

| Element            | Color       | Hex       | Internal | External |
| ------------------ | ----------- | --------- | -------- | -------- |
| **Component**      | Medium Blue | `#1168bd` | ✓        | -        |
| **Component**      | Dark Gray   | `#999999` | -        | ✓        |
| **ComponentDb**    | Medium Blue | `#1168bd` | ✓        | -        |
| **ComponentDb**    | Dark Gray   | `#999999` | -        | ✓        |
| **ComponentQueue** | Medium Blue | `#1168bd` | ✓        | -        |
| **ComponentQueue** | Dark Gray   | `#999999` | -        | ✓        |
| **Text/Stroke**    | Dark Gray   | `#073b6f` | -        | -        |

---

## C4 PlantUML Elements → Mermaid Flowchart Mapping

| C4 PlantUML Element       | Mermaid Class       | Element Type              | Example   |
| ------------------------- | ------------------- | ------------------------- | --------- |
| `Component(...)`          | `Component`         | Component (Internal)      | Element 1 |
| `Component_Ext(...)`      | `ComponentExt`      | Component (External)      | Element 2 |
| `ComponentDb(...)`        | `ComponentDb`       | ComponentDb (Internal)    | Element 3 |
| `ComponentDb_Ext(...)`    | `ComponentDbExt`    | ComponentDb (External)    | Element 4 |
| `ComponentQueue(...)`     | `ComponentQueue`    | ComponentQueue (Internal) | Element 5 |
| `ComponentQueue_Ext(...)` | `ComponentQueueExt` | ComponentQueue (External) | Element 6 |

---

## Element Index & Legend

All Component-level elements shown together, plus the C4-PlantUML macro each one maps to. Grab the matching `classDef` line(s) and node syntax from the legend below — every snippet is self-contained and renders standalone.

```mermaid
flowchart TB
    classDef Component fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ComponentExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef ComponentDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ComponentDbExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef ComponentQueue fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ComponentQueueExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;

    subgraph internal["Internal components"]
        direction LR
        c1["⚙️<br/><b>Component</b><br/>[1]"]
        cdb1[("📊<br/><b>ComponentDb</b><br/>[3]")]
        cq1@{ shape: das, label: "📡<br/><b>ComponentQueue</b><br/>[5]" }
    end
    class c1 Component
    class cdb1 ComponentDb
    class cq1 ComponentQueue

    subgraph external["External components"]
        direction LR
        c2["📦<br/><b>Component_Ext</b><br/>[2]"]
        cdb2[("📊<br/><b>ComponentDb_Ext</b><br/>[4]")]
        cq2@{ shape: das, label: "📡<br/><b>ComponentQueue_Ext</b><br/>[6]" }
    end
    class c2 ComponentExt
    class cdb2 ComponentDbExt
    class cq2 ComponentQueueExt
```

| #   | C4 PlantUML                                     | Mermaid class       | Shape        | Usage                            |
| --- | ----------------------------------------------- | ------------------- | ------------ | -------------------------------- |
| 1   | `Component(alias, label, tech, descr)`          | `Component`         | rect         | Internal class/module/service    |
| 2   | `Component_Ext(alias, label, tech, descr)`      | `ComponentExt`      | rect         | External library/package         |
| 3   | `ComponentDb(alias, label, tech, descr)`        | `ComponentDb`       | cylinder     | Internal repository/DAO          |
| 4   | `ComponentDb_Ext(alias, label, tech, descr)`    | `ComponentDbExt`    | cylinder     | External data client/driver      |
| 5   | `ComponentQueue(alias, label, tech, descr)`     | `ComponentQueue`    | dashed shape | Internal event publisher/handler |
| 6   | `ComponentQueue_Ext(alias, label, tech, descr)` | `ComponentQueueExt` | dashed shape | External messaging client        |

---

## Complete Component Diagram Example 1: Web API Backend

```mermaid
flowchart TB
    classDef Component fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ComponentDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ComponentQueue fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ComponentExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;

    client["📱<br/><b>Web Client</b>"]

    subgraph container["API Container [Node.js]"]
        direction TB

        subgraph handlers["HTTP Handlers"]
            direction TB
            userctrl["⚙️<br/><b>User Controller</b><br/>[Component]"]
            orderctrl["⚙️<br/><b>Order Controller</b><br/>[Component]"]
        end

        subgraph services["Business Services"]
            direction TB
            usersvc["💼<br/><b>User Service</b><br/>[Component]"]
            ordersvc["💼<br/><b>Order Service</b><br/>[Component]"]
        end

        subgraph dataaccess["Data Access"]
            direction TB
            userrepo[("📊<br/><b>User Repository</b><br/>[Component]")]
            orderrepo[("📊<br/><b>Order Repository</b><br/>[Component]")]
        end

        subgraph events["Events"]
            direction TB
            eventpub@{ shape: das, label: "📡<br/><b>Event Publisher</b><br/>[Component]" }
        end

        class userctrl,orderctrl,usersvc,ordersvc Component
        class userrepo,orderrepo ComponentDb
        class eventpub ComponentQueue

        userctrl -->|"Call"| usersvc
        orderctrl -->|"Call"| ordersvc

        usersvc -->|"Use"| userrepo
        ordersvc -->|"Use"| orderrepo

        ordersvc -->|"Publish"| eventpub
    end

    db[("💾<br/><b>Database</b>")]
    queue["📨<br/><b>Message Queue</b>"]
    extapi["🔗<br/><b>External API</b>"]

    class extapi ComponentExt

    client -->|"REST"| userctrl
    client -->|"REST"| orderctrl

    userrepo -->|"SQL"| db
    orderrepo -->|"SQL"| db

    eventpub -->|"Publish"| queue
    usersvc -->|"Call"| extapi
```

---

## Complete Component Diagram Example 2: Microservice Architecture

```mermaid
flowchart TB
    classDef Component fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ComponentDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ComponentExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;

    request["🌐<br/><b>HTTP Request</b>"]

    subgraph container["Authentication Service [Python]"]
        direction TB

        subgraph handlers["API Layer"]
            direction TB
            authctrl["🔐<br/><b>Auth Controller</b><br/>[Component]"]
        end

        subgraph logic["Business Logic"]
            direction TB
            authsvc["🔐<br/><b>Auth Service</b><br/>[Component]"]
            jwtsvc["🔑<br/><b>JWT Service</b><br/>[Component]"]
            hashsvc["🔒<br/><b>Hash Service</b><br/>[Component]"]
        end

        subgraph persistence["Persistence"]
            direction TB
            userrepo[("👤<br/><b>User Repository</b><br/>[Component]")]
            sessionrepo[("📋<br/><b>Session Repository</b><br/>[Component]")]
        end

        class authctrl,authsvc,jwtsvc,hashsvc Component
        class userrepo,sessionrepo ComponentDb

        authctrl -->|"Validate"| authsvc
        authsvc -->|"Sign"| jwtsvc
        authsvc -->|"Hash"| hashsvc

        authsvc -->|"Query"| userrepo
        authsvc -->|"Query"| sessionrepo
    end

    db[("💾<br/><b>User DB</b>")]
    cache[("⚡<br/><b>Session Cache</b>")]
    oauthprov["🔐<br/><b>OAuth Provider</b>"]

    class oauthprov ComponentExt

    request -->|"HTTP"| authctrl

    userrepo -->|"Query"| db
    sessionrepo -->|"Cache"| cache

    authsvc -->|"Verify"| oauthprov
```

---

## Complete Component Diagram Example 3: Desktop Application

```mermaid
flowchart TB
    classDef Component fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ComponentDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ComponentExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;

    user["👤<br/><b>User</b>"]

    subgraph container["Desktop App Container [Electron + TypeScript]"]
        direction TB

        subgraph ui["User Interface"]
            direction TB
            mainwin["🖼️<br/><b>Main Window</b><br/>[Component]"]
            menubar["📋<br/><b>Menu Bar</b><br/>[Component]"]
        end

        subgraph viewmodels["ViewModels"]
            direction TB
            mainvm["📊<br/><b>Main ViewModel</b><br/>[Component]"]
            settingsvm["⚙️<br/><b>Settings ViewModel</b><br/>[Component]"]
        end

        subgraph services["Services"]
            direction TB
            datasvc["💼<br/><b>Data Service</b><br/>[Component]"]
            configsvc["📝<br/><b>Config Service</b><br/>[Component]"]
            apiclient["🔗<br/><b>API Client</b><br/>[Component]"]
        end

        subgraph storage["Local Storage"]
            direction TB
            localdb[("💾<br/><b>SQLite DB</b><br/>[Component]")]
            cache[("💾<br/><b>App Cache</b><br/>[Component]")]
        end

        class mainwin,menubar,mainvm,settingsvm,datasvc,configsvc,apiclient Component
        class localdb,cache ComponentDb

        mainwin -->|"Bind"| mainvm
        menubar -->|"Update"| mainvm

        mainvm -->|"Use"| datasvc
        settingsvm -->|"Use"| configsvc

        datasvc -->|"Store"| localdb
        datasvc -->|"Cache"| cache
        datasvc -->|"Call"| apiclient
    end

    api["☁️<br/><b>Backend API</b>"]
    extlib["📦<br/><b>Chart Library</b>"]

    class extlib ComponentExt

    user -->|"Interact"| mainwin
    apiclient -->|"REST"| api
    mainvm -->|"Use"| extlib
```

---

## Component Design Patterns

### Common Component Patterns

| Pattern              | Description                       | Example Components               |
| -------------------- | --------------------------------- | -------------------------------- |
| **MVC**              | Model-View-Controller             | Controller, Service, Repository  |
| **MVVM**             | Model-View-ViewModel              | ViewModel, Model, DataService    |
| **Layered**          | Presentation-Business-Persistence | Controller, Service, Repository  |
| **Microkernel**      | Core + Plugin modules             | Kernel, Plugins, Plugin Registry |
| **Event-Driven**     | Event producers & consumers       | Publisher, Subscriber, EventBus  |
| **Ports & Adapters** | Hexagonal architecture            | Port, Adapter, Core Domain       |

---

## Best Practices for Component Diagrams

### ✅ DO's

- **Show internal organization** — How the container is structured
- **Include technology/framework** — Spring, Django, React, etc.
- **Use meaningful names** — Reflect actual classes/modules
- **Group by layer or feature** — Controllers, Services, Repositories, etc.
- **Show dependencies** — Component A depends on Component B
- **Include data stores** — Where components persist/access data
- **Use consistent styling** — All components follow same color/shape rules

### ❌ DON'Ts

- **Don't show individual methods** — That's code-level detail
- **Don't over-detail** — Component diagrams should be readable at a glance
- **Don't mix Container and Component levels** — Each diagram focuses on one level
- **Don't show every possible relationship** — Only significant dependencies
- **Don't forget technology labels** — Context on which framework/library is used
- **Don't create diagrams for every container** — Focus on complex or critical containers

---

## Copy-Paste Template: Complete Component Diagram

```mermaid
flowchart TB
    %% ===== STYLES =====
    classDef Component fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ComponentDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ComponentQueue fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ComponentExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;

    %% ===== EXTERNAL INPUT =====
    input["📱<br/><b>Client Request</b>"]

    %% ===== CONTAINER BOUNDARY =====
    subgraph container["Container Name [Technology]"]
        direction TB

        %% Layer 1: Interface/Controller
        ctrl["⚙️<br/><b>Controller</b><br/>[Component]<br/>Tech"]

        %% Layer 2: Business Logic
        svc["💼<br/><b>Service</b><br/>[Component]<br/>Tech"]

        %% Layer 3: Data Access
        repo[("📊<br/><b>Repository</b><br/>[Component]<br/>Tech")]

        %% Events
        events@{ shape: das, label: "📡<br/><b>Event Handler</b><br/>[Component]<br/>Tech" }

        class events ComponentQueue
        class ctrl,svc Component
        class repo ComponentDb

        %% Dependencies
        ctrl -->|"Use"| svc
        svc -->|"Use"| repo
        svc -->|"Publish"| events
    end

    %% ===== EXTERNAL SYSTEMS =====
    extdb[("💾<br/><b>Database</b>")]
    extlib["📦<br/><b>External Lib</b>"]

    class extlib ComponentExt

    %% ===== RELATIONSHIPS =====
    input -->|"HTTP"| ctrl
    repo -->|"Query"| extdb
    svc -->|"Use"| extlib
```

---

## C4 Model Progression: Context → Container → Component

```
Context Diagram
  └─ Shows overall system context and external systems

  Container Diagram (for selected system)
    └─ Shows deployment units (apps, databases, services)

      Component Diagram (for selected container)
      └─ Shows internal structure and modules

        Code Diagram (UML Class Diagrams)
        └─ Shows actual classes, methods, attributes
```

---

## Technology Stack Examples by Language

| Language     | Component Types                             | Example Stack                  |
| ------------ | ------------------------------------------- | ------------------------------ |
| **Java**     | Controller, Service, Repository, Manager    | Spring Boot, Hibernate, JPA    |
| **Python**   | Controller, Service, DAO, Manager           | Flask, SQLAlchemy, Django ORM  |
| **C#**       | Controller, Service, Repository, Manager    | ASP.NET Core, Entity Framework |
| **Node.js**  | Controller, Service, Repository, Middleware | Express, Sequelize, Mongoose   |
| **Go**       | Handler, Service, Repository, Manager       | Gin, GORM, sqlc                |
| **Frontend** | View, ViewModel, Service, Store             | React, Vue, Angular, Redux     |
