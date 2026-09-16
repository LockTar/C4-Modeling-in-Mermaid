# C4 Container Diagram - Mermaid Flowchart Cheatsheet

> Container diagrams show the high-level technology choices within a software system. Containers represent deployable units (web apps, APIs, databases, microservices, etc.).

---

## Color Palette (C4 Blue Theme)

| Element                | Color       | Hex       | Internal | External |
| ---------------------- | ----------- | --------- | -------- | -------- |
| **Container**          | Medium Blue | `#1168bd` | ✓        | -        |
| **Container**          | Dark Gray   | `#999999` | -        | ✓        |
| **ContainerDb**        | Medium Blue | `#1168bd` | ✓        | -        |
| **ContainerDb**        | Dark Gray   | `#999999` | -        | ✓        |
| **ContainerQueue**     | Medium Blue | `#1168bd` | ✓        | -        |
| **ContainerQueue**     | Dark Gray   | `#999999` | -        | ✓        |
| **Container_Boundary** | Dashed Gray | `#999`    | -        | -        |
| **Text/Stroke**        | Dark Gray   | `#073b6f` | -        | -        |

---

## C4 PlantUML Elements → Mermaid Flowchart Mapping

| C4 PlantUML Element       | Mermaid Class       | Element Type              | Example   |
| ------------------------- | ------------------- | ------------------------- | --------- |
| `Container(...)`          | `Container`         | Container (Internal)      | Element 1 |
| `Container_Ext(...)`      | `ContainerExt`      | Container (External)      | Element 2 |
| `ContainerDb(...)`        | `ContainerDb`       | ContainerDb (Internal)    | Element 3 |
| `ContainerDb_Ext(...)`    | `ContainerDbExt`    | ContainerDb (External)    | Element 4 |
| `ContainerQueue(...)`     | `ContainerQueue`    | ContainerQueue (Internal) | Element 5 |
| `ContainerQueue_Ext(...)` | `ContainerQueueExt` | ContainerQueue (External) | Element 6 |
| `Container_Boundary(...)` | `ContainerBoundary` | Container Boundary        | Element 7 |

---

## Element Index & Legend

All Container-level elements shown together, plus the C4-PlantUML macro each one maps to. Grab the matching `classDef` line(s) and node/subgraph syntax from the legend below — every snippet is self-contained and renders standalone.

```mermaid
flowchart TB
    classDef Person fill:#08427b,stroke:#073b6f,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef PersonExt fill:#999999,stroke:#8a8a8a,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef Container fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ContainerExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef ContainerDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ContainerDbExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef ContainerQueue fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ContainerQueueExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef ContainerBoundary fill:#fff,stroke:#999,stroke-width:2px,stroke-dasharray: 5 5,color:#444;

    subgraph internal["Internal containers"]
        direction LR
        c1["📋<br/><b>Container</b><br/>[1]"]
        cdb1[("💾<br/><b>ContainerDb</b><br/>[3]")]
        cq1@{ shape: das, label: "📨<br/><b>ContainerQueue</b><br/>[5]" }
    end
    class c1 Container
    class cdb1 ContainerDb
    class cq1 ContainerQueue

    subgraph external["External containers"]
        direction LR
        c2["🔗<br/><b>Container_Ext</b><br/>[2]"]
        cdb2[("💾<br/><b>ContainerDb_Ext</b><br/>[4]")]
        cq2@{ shape: das, label: "📨<br/><b>ContainerQueue_Ext</b><br/>[6]" }
    end
    class c2 ContainerExt
    class cdb2 ContainerDbExt
    class cq2 ContainerQueueExt

    subgraph boundary1["Container_Boundary [7]"]
        direction TB
        b1["📋<br/><b>Web App</b>"]
        b2["⚙️<br/><b>API</b>"]
    end
    class b1,b2 Container
    class boundary1 ContainerBoundary
```

| #   | C4 PlantUML                                     | Mermaid class                  | Shape      | Usage                                                 |
| --- | ----------------------------------------------- | ------------------------------ | ---------- | ----------------------------------------------------- |
| 1   | `Container(alias, label, tech, descr)`          | `Container`                    | rect       | Internal deployable unit                              |
| 2   | `Container_Ext(alias, label, tech, descr)`      | `ContainerExt`                 | rect       | External deployable unit                              |
| 3   | `ContainerDb(alias, label, tech, descr)`        | `ContainerDb`                  | cylinder   | Internal database/data store                          |
| 4   | `ContainerDb_Ext(alias, label, tech, descr)`    | `ContainerDbExt`               | cylinder   | External database/data store                          |
| 5   | `ContainerQueue(alias, label, tech, descr)`     | `ContainerQueue`               | rect       | Internal message broker/queue                         |
| 6   | `ContainerQueue_Ext(alias, label, tech, descr)` | `ContainerQueueExt`            | rect       | External message broker/queue                         |
| 7   | `Container_Boundary(alias, label) { ... }`      | `ContainerBoundary` (subgraph) | dashed box | Groups containers within a system/deployment boundary |

---

## Complete Container Diagram Example 1: E-Commerce Microservices

```mermaid
flowchart TB
    classDef Person fill:#08427b,stroke:#073b6f,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef Container fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ContainerDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ContainerExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef ContainerBoundary fill:#fff,stroke:#999,stroke-width:2px,stroke-dasharray: 5 5,color:#444;

    user["👤<br/><b>Customer</b>"]

    subgraph sys["E-Commerce System [Software System]"]
        direction TB

        spa["🌐<br/><b>SPA</b><br/>[Container]<br/>React"]

        subgraph services["Microservices [Container Boundary]"]
            direction TB
            productapi["⚙️<br/><b>Product API</b><br/>[Container]<br/>Node.js"]
            orderapi["⚙️<br/><b>Order API</b><br/>[Container]<br/>Python"]
            paymentapi["💳<br/><b>Payment API</b><br/>[Container]<br/>Java"]
        end
        class services ContainerBoundary

        maindb[("💾<br/><b>Main DB</b><br/>[Container]<br/>PostgreSQL")]
        cache[("⚡<br/><b>Cache</b><br/>[Container]<br/>Redis")]
        queue@{ shape: das, label: "📨<br/><b>Queue</b><br/>[Container]<br/>RabbitMQ" }

        class spa,productapi,orderapi,paymentapi,queue Container
        class maindb,cache ContainerDb

        spa -->|REST| productapi
        spa -->|REST| orderapi
        spa -->|REST| paymentapi

        productapi -->|SQL| maindb
        orderapi -->|SQL| maindb
        paymentapi -->|Cache| cache

        orderapi -->|Publish| queue
    end
    class sys ContainerBoundary;

    paymentgateway["💳<br/><b>Payment Gateway</b><br/>[Container]<br/>Stripe API"]
    email["📧<br/><b>Email Service</b><br/>[Container]<br/>SendGrid"]

    class user Person
    class paymentgateway,email ContainerExt

    user -->|HTTPS| spa
    paymentapi -->|REST| paymentgateway
    queue -->|HTTP Webhook| email
```

---

## Complete Container Diagram Example 2: Enterprise Web Application

```mermaid
flowchart TB
    classDef Person fill:#08427b,stroke:#073b6f,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef Container fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ContainerDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ContainerExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef ContainerBoundary fill:#fff,stroke:#999,stroke-width:2px,stroke-dasharray: 5 5,color:#444;

    browser["👨‍💼<br/><b>User</b>"]
    admin["👨‍💼<br/><b>Admin</b>"]

    subgraph sys["Enterprise System [Software System]"]
        direction TB

        web["🌐<br/><b>Web App</b><br/>[Container]<br/>ASP.NET Core"]
        api["⚙️<br/><b>API Gateway</b><br/>[Container]<br/>.NET 6"]
        worker["🔄<br/><b>Background<br/>Worker</b><br/>[Container]<br/>.NET 6"]

        primary[("💾<br/><b>Primary DB</b><br/>[Container]<br/>SQL Server")]
        backup[("💾<br/><b>Backup DB</b><br/>[Container]<br/>SQL Server")]

        class web,api,worker Container
        class primary,backup ContainerDb

        web -->|REST| api
        api -->|SQL| primary
        worker -->|SQL| primary
        primary -->|Replication| backup
    end
    class sys ContainerBoundary;

    ldap["🔐<br/><b>LDAP Server</b><br/>[Container]<br/>Active Directory"]
    fileserver["📁<br/><b>File Server</b><br/>[Container]<br/>SMB"]

    class browser,admin Person
    class ldap,fileserver ContainerExt

    browser -->|HTTPS| web
    admin -->|HTTPS| web
    api -->|LDAP| ldap
    worker -->|SMB| fileserver
```

---

## Complete Container Diagram Example 3: Cloud-Native SaaS

```mermaid
flowchart TB
    classDef Person fill:#08427b,stroke:#073b6f,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef Container fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ContainerDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ContainerQueue fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ContainerExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef ContainerBoundary fill:#fff,stroke:#999,stroke-width:2px,stroke-dasharray: 5 5,color:#444;

    user["👤<br/><b>User</b>"]
    admin["👤<br/><b>Admin</b>"]

    subgraph sys["SaaS Platform [Software System]"]
        direction TB

        cdn["🌍<br/><b>CDN</b><br/>[Container]<br/>CloudFlare"]
        spa["🌐<br/><b>Web UI</b><br/>[Container]<br/>React + TypeScript"]

        subgraph backend["Backend Services [Container Boundary]"]
            direction TB
            apigw["🚪<br/><b>API Gateway</b><br/>[Container]<br/>Kong"]
            authsvc["🔐<br/><b>Auth Service</b><br/>[Container]<br/>Node.js"]
            usersvc["👤<br/><b>User Service</b><br/>[Container]<br/>Python"]
            bussvc["💼<br/><b>Business Logic</b><br/>[Container]<br/>Go"]
        end
        class backend ContainerBoundary;

        db[("💾<br/><b>Primary DB</b><br/>[Container]<br/>PostgreSQL")]
        cache[("⚡<br/><b>Cache</b><br/>[Container]<br/>Redis")]
        s3@{ shape: lin-cyl, label: "☁️<br/><b>Object Storage</b><br/>[Container]<br/>S3" }

        queue@{ shape: das, label: "📨<br/><b>Event Bus</b><br/>[Container]<br/>Kafka" }
        workers["🔄<br/><b>Workers</b><br/>[Container]<br/>Python"]

        class cdn,spa,apigw,authsvc,usersvc,bussvc,s3,workers Container
        class db,cache ContainerDb
        class queue ContainerQueue

        spa -->|Cached| cdn
        spa -->|REST| apigw

        apigw -->|Route| authsvc
        apigw -->|Route| usersvc
        apigw -->|Route| bussvc

        authsvc -->|Query| db
        usersvc -->|Query| db
        bussvc -->|Query| db

        bussvc -->|Cache| cache
        bussvc -->|Upload| s3
        bussvc -->|Publish| queue

        workers -->|Consume| queue
    end
    class sys ContainerBoundary;

    oauth["🔐<br/><b>OAuth Provider</b><br/>[Container]<br/>Auth0"]
    analytics["📋<br/><b>Analytics</b><br/>[Container]<br/>Segment"]

    class user,admin Person
    class oauth,analytics ContainerExt

    user -->|HTTPS| spa
    admin -->|HTTPS| spa
    authsvc -->|HTTPS| oauth
    workers -->|REST| analytics
```

---

## Styling Combinations

### Container with Technology Labels

```mermaid
flowchart TB
    classDef Container fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ContainerDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;

    c1["🌐<br/><b>Web App</b><br/>[Container]<br/>React"]
    c2["⚙️<br/><b>API</b><br/>[Container]<br/>Node.js"]
    c3["📱<br/><b>Mobile</b><br/>[Container]<br/>Flutter"]
    c4["🔄<br/><b>Worker</b><br/>[Container]<br/>Python"]

    class c1,c2,c3,c4 Container
    c5[("💾<br/><b>Database</b><br/>[Container]<br/>PostgreSQL")]

    class c5 ContainerDb

    c6@{ shape: lin-cyl, label: "☁️<br/><b>Object Storage</b><br/>[Container]<br/>S3" }

    class c6 Container
```

---

## Best Practices for Container Diagrams

### ✅ DO's

- **Show deployable units** — Each container is independently deployable
- **Include technology stack** — Node.js, Python, PostgreSQL, etc.
- **Group by deployment boundary** — Use Container_Boundary for related containers
- **Use consistent technology abbreviations** — React, FastAPI, MySQL
- **Indicate data flow** — Show which containers talk to each other
- **Include database containers** — Databases are first-class deployment units

### ❌ DON'Ts

- **Don't show class diagrams** — That's the Component level
- **Don't mix Container and Component details** — Stay at the Container level of abstraction
- **Don't show internal API endpoints** — Keep labels simple
- **Don't create overly dense diagrams** — Aim for 5-15 containers per diagram
- **Don't forget technology labels** — They're essential context

---

## Copy-Paste Template: Complete Container Diagram

```mermaid
flowchart TB
    %% ===== STYLES =====
    classDef Person fill:#08427b,stroke:#073b6f,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef PersonExt fill:#999999,stroke:#8a8a8a,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef Container fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ContainerDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ContainerQueue fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef ContainerExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef ContainerBoundary fill:#fff,stroke:#999,stroke-width:2px,stroke-dasharray: 5 5,color:#444;

    subgraph main["Title of the diagram"]
        direction TB
        %% ===== ACTORS =====
        user["👤<br/><b>User</b>"]

        class user Person

        %% ===== MAIN SYSTEM BOUNDARY =====
        subgraph sys["System Name [Software System]"]
            direction TB

            %% Internal Containers
            web["🌐<br/><b>Web App</b><br/>[Container]<br/>Tech Stack"]
            api["⚙️<br/><b>API</b><br/>[Container]<br/>Tech Stack"]

            %% Database Containers
            db[("💾<br/><b>Database</b><br/>[Container]<br/>Tech Stack")]

            %% Message Queue
            queue@{ shape: das, label: "📨<br/><b>Queue</b><br/>[Container]<br/>Tech Stack" }

            class web,api Container
            class db ContainerDb
            class queue ContainerQueue

            %% Relationships
            web -->|REST| api
            api -->|SQL| db
            api -->|Publish| queue
        end
        class sys ContainerBoundary;

        %% ===== EXTERNAL CONTAINERS =====
        extservice["🔗<br/><b>External Service</b><br/>[Container]<br/>Tech Stack"]

        class extservice ContainerExt

        %% ===== RELATIONSHIPS =====
        user -->|HTTPS| web
        queue -->|REST| extservice
    end

    %% ===== LEGEND =====
    subgraph legend["🔷 Legend"]
        direction LR
        leg1["👤<br/><b>Person</b><br/>(Internal)"]
        leg2["👤<br/><b>Person</b><br/>(External)"]
        leg3["📋<br/><b>System</b><br/>(Internal)"]
        leg4["🔗<br/><b>System</b><br/>(External)"]
        leg5[("💾<br/><b>Database</b><br/>(Internal)")]

        leg1 ~~~ leg2 ~~~ leg3 ~~~ leg4 ~~~ leg5

        class leg1 Person
        class leg2 PersonExt
        class leg3 System
        class leg4 SystemExt
        class leg5 SystemDb
    end
    class legend SystemBoundary

    main ~~~ legend
```

---

## Container Diagram Layers (C4 Model)

```text
Level 1: System Context     → Systems & People
Level 2: Container          ← YOU ARE HERE (Deployable units)
Level 3: Component          → Internal components
Level 4: Code               → Classes, functions
```

---

## Common Container Technology Stacks

| Container Type | Technologies                                | Examples         |
| -------------- | ------------------------------------------- | ---------------- |
| **Web App**    | React, Vue, Angular, Svelte                 | SPA Frontend     |
| **API**        | Node.js, Python, Java, Go, C#               | REST, GraphQL    |
| **Worker**     | Python, Node.js, Go, C#                     | Background jobs  |
| **Database**   | PostgreSQL, MySQL, MongoDB, SQL Server      | Data persistence |
| **Cache**      | Redis, Memcached, Elasticsearch             | Performance      |
| **Queue**      | RabbitMQ, Kafka, AWS SQS, Azure Service Bus | Async messaging  |
| **Mobile**     | React Native, Flutter, Swift, Kotlin        | Mobile app       |
| **Desktop**    | Electron, WinForms, WPF                     | Desktop app      |
