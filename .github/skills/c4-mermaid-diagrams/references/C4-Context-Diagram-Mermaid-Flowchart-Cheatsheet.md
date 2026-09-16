# C4 Context Diagram - Mermaid Flowchart Cheatsheet

<!-- Synced from C4-cheatsheets/C4-Context-Diagram-Mermaid-Flowchart-Cheatsheet.md on 2026-09-16. Keep in sync when the source changes. -->

> Using mermaid `flowchart` with C4 styling to replace mermaid's native C4Context that has limitations.

## Color Palette (C4 Blue Theme)

| Element                        | Color       | Hex       | Internal | External |
| ------------------------------ | ----------- | --------- | -------- | -------- |
| **Person**                     | Dark Blue   | `#08427b` | ✓        | -        |
| **Person**                     | Gray        | `#999999` | -        | ✓        |
| **System**                     | Medium Blue | `#1168bd` | ✓        | -        |
| **System**                     | Dark Gray   | `#999999` | -        | ✓        |
| **SystemDb**                   | Medium Blue | `#1168bd` | ✓        | -        |
| **SystemDb**                   | Dark Gray   | `#999999` | -        | ✓        |
| **SystemQueue**                | Medium Blue | `#1168bd` | ✓        | -        |
| **SystemQueue**                | Dark Gray   | `#999999` | -        | ✓        |
| **Boundary / System_Boundary** | Dashed Gray | `#999`    | -        | -        |
| **Enterprise_Boundary**        | Dashed Gray | `#999`    | -        | -        |
| **Text/Stroke**                | Dark Gray   | `#073b6f` | -        | -        |

---

## C4 PlantUML Elements → Mermaid Flowchart Mapping

| C4 PlantUML Element        | Mermaid Class        | Element Type           | Example    |
| -------------------------- | -------------------- | ---------------------- | ---------- |
| `Person(...)`              | `Person`             | Person (Internal)      | Element 1  |
| `Person_Ext(...)`          | `PersonExt`          | Person (External)      | Element 2  |
| `System(...)`              | `System`             | System (Internal)      | Element 3  |
| `System_Ext(...)`          | `SystemExt`          | System (External)      | Element 4  |
| `SystemDb(...)`            | `SystemDb`           | SystemDb (Internal)    | Element 7  |
| `SystemDb_Ext(...)`        | `SystemDbExt`        | SystemDb (External)    | Element 8  |
| `SystemQueue(...)`         | `SystemQueue`        | SystemQueue (Internal) | Element 6  |
| `SystemQueue_Ext(...)`     | `SystemQueueExt`     | SystemQueue (External) | Element 9  |
| `System_Boundary(...)`     | `SystemBoundary`     | System Boundary        | Element 10 |
| `Enterprise_Boundary(...)` | `EnterpriseBoundary` | Enterprise Boundary    | Element 11 |
| `Boundary(...)`            | `Boundary`           | Generic Boundary       | Element 12 |

---

## Element Index & Legend

All Context-level elements shown together, plus the C4-PlantUML macro each one maps to. Grab the matching `classDef` line(s) and node/subgraph syntax from the legend below — every snippet is self-contained and renders standalone.

```mermaid
flowchart TB
    classDef Person fill:#08427b,stroke:#073b6f,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef PersonExt fill:#999999,stroke:#8a8a8a,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef System fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef SystemExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef SystemDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef SystemDbExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef SystemQueue fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef SystemQueueExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef SystemBoundary fill:#fff,stroke:#999,stroke-width:2px,stroke-dasharray: 5 5,color:#444;
    classDef EnterpriseBoundary fill:#fff,stroke:#444,stroke-width:3px,stroke-dasharray: 5 5,color:#444;
    classDef Boundary fill:#fff,stroke:#999,stroke-width:2px,stroke-dasharray: 5 5,color:#444;

    subgraph internal["Internal elements"]
        direction LR
        p1["👤<br/><b>Person</b><br/>[1]"]
        s1["📋<br/><b>System</b><br/>[3]"]
        db1[("💾<br/><b>SystemDb</b><br/>[7]")]
        q1@{ shape: das, label: "📨<br/><b>SystemQueue</b><br/>[6]" }
    end
    class p1 Person
    class s1 System
    class db1 SystemDb
    class q1 SystemQueue

    subgraph external["External elements"]
        direction LR
        p2["👤<br/><b>Person_Ext</b><br/>[2]"]
        s2["🔗<br/><b>System_Ext</b><br/>[4]"]
        db2[("💾<br/><b>SystemDb_Ext</b><br/>[8]")]
        q2@{ shape: das, label: "📨<br/><b>SystemQueue_Ext</b><br/>[9]" }
    end
    class p2 PersonExt
    class s2 SystemExt
    class db2 SystemDbExt
    class q2 SystemQueueExt

    subgraph enterprise["Enterprise_Boundary [11]"]
        direction TB
        subgraph sysb["System_Boundary [10]"]
            direction TB
            comp1["📋<br/><b>Component</b>"]
        end
        class comp1 System
        class sysb SystemBoundary
    end
    class enterprise EnterpriseBoundary

    subgraph generic["Boundary generic [12]"]
        direction LR
        item1["Item 1"]
        item2["Item 2"]
    end
    class item1,item2 System
    class generic Boundary
```

| #   | C4 PlantUML                                 | Mermaid class                   | Shape            | Usage                             |
| --- | ------------------------------------------- | ------------------------------- | ---------------- | --------------------------------- |
| 1   | `Person(alias, label)`                      | `Person`                        | rounded rect     | Internal user/actor               |
| 2   | `Person_Ext(alias, label)`                  | `PersonExt`                     | rounded rect     | External user/actor               |
| 3   | `System(alias, label)`                      | `System`                        | rect             | Internal software system          |
| 4   | `System_Ext(alias, label)`                  | `SystemExt`                     | rect             | External software system          |
| 5   | `SystemDb(alias, label)`                    | `SystemDb`                      | cylinder         | Generic internal data store       |
| 6   | `SystemQueue(alias, label)`                 | `SystemQueue`                   | rect             | Internal message broker/event bus |
| 7   | `SystemDb(alias, label)`                    | `SystemDb`                      | cylinder         | Internal database                 |
| 8   | `SystemDb_Ext(alias, label)`                | `SystemDbExt`                   | cylinder         | External database                 |
| 9   | `SystemQueue_Ext(alias, label)`             | `SystemQueueExt`                | rect             | External message broker           |
| 10  | `System_Boundary(alias, label) { ... }`     | `SystemBoundary` (subgraph)     | dashed box       | Groups elements inside one system |
| 11  | `Enterprise_Boundary(alias, label) { ... }` | `EnterpriseBoundary` (subgraph) | thick dashed box | Groups one or more systems        |
| 12  | `Boundary(alias, label, type) { ... }`      | `Boundary` (subgraph)           | dashed box       | Generic/custom grouping           |

---

## Complete Context Diagram Example 1: Basic E-Commerce

```mermaid
flowchart TB
    %% Style definitions
    classDef Person fill:#08427b,stroke:#073b6f,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef PersonExt fill:#999999,stroke:#8a8a8a,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef System fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef SystemExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef SystemDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef SystemBoundary fill:#fff,stroke:#999,stroke-width:2px,stroke-dasharray: 5 5,color:#444;

    %% External Actor
    customer["👤<br/><b>Customer</b><br/>[Person]"]

    %% Main System Boundary
    subgraph ecommerce["E-Commerce Platform [Software System]"]
        direction TB
        web["🌐<br/><b>Web App</b><br/>[Container]"]
        api["⚙️<br/><b>API Backend</b><br/>[Container]"]
        db[("💾<br/><b>Database</b><br/>[Database]")]

        class web,api System
        class db SystemDb

        web -->|REST/JSON| api
        api -->|SQL| db
    end
    class ecommerce SystemBoundary

    %% External Systems
    extpay["💳<br/><b>Payment Gateway</b><br/>[External System]"]
    extmail["📧<br/><b>Email Service</b><br/>[External System]"]

    class customer Person
    class extpay,extmail SystemExt

    %% Relationships
    customer -->|"Browse & Purchase<br/>[HTTP/HTTPS]"| ecommerce
    ecommerce -->|"Process Payment<br/>[REST API]"| extpay
    ecommerce -->|"Send Confirmation<br/>[SMTP]"| extmail
```

---

## Complete Context Diagram Example 2: Banking System

```mermaid
flowchart TB
    %% Style definitions
    classDef Person fill:#08427b,stroke:#073b6f,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef PersonExt fill:#999999,stroke:#8a8a8a,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef System fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef SystemExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef SystemDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef SystemBoundary fill:#fff,stroke:#999,stroke-width:2px,stroke-dasharray: 5 5,color:#444;

    %% Internal Actor
    customer["👤<br/><b>Customer</b><br/>[Person]"]
    banker["👤<br/><b>Banker</b><br/>[Person]"]

    %% Main System Boundary
    subgraph banking["Internet Banking System [Software System]"]
        direction TB
        webportal["🌐<br/><b>Web Portal</b><br/>[Container]"]
        mobileapp["📱<br/><b>Mobile App</b><br/>[Container]"]
        api["⚙️<br/><b>API Server</b><br/>[Container]"]
        db[("💾<br/><b>Banking DB</b><br/>[Database]")]

        class customer,banker Person
        class webportal,mobileapp,api System
        class db SystemDb

        webportal -->|REST| api
        mobileapp -->|REST| api
        api -->|SQL| db
    end
    class banking SystemBoundary

    %% External Systems
    mainframe["🖥️<br/><b>Mainframe<br/>Banking System</b><br/>[External System]"]
    extmail["📧<br/><b>Email Service</b><br/>[External System]"]

    class mainframe,extmail SystemExt

    %% Relationships
    customer -->|"Check Balance<br/>Make Payments<br/>[HTTPS]"| banking
    banker -->|"Manage Accounts<br/>[HTTPS]"| banking
    banking -->|"Read Accounts<br/>Execute Transactions<br/>[API]"| mainframe
    banking -->|"Send Notifications<br/>[SMTP]"| extmail
```

---

## Complete Context Diagram Example 3: Multi-Tenant SaaS

```mermaid
flowchart TB
    %% Style definitions
    classDef Person fill:#08427b,stroke:#073b6f,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef PersonExt fill:#999999,stroke:#8a8a8a,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef System fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef SystemExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef SystemDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef SystemQueue fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef SystemBoundary fill:#fff,stroke:#999,stroke-width:2px,stroke-dasharray: 5 5,color:#444;

    %% Actors
    employee["👤<br/><b>Employee</b><br/>[Person]"]
    admin["👤<br/><b>Administrator</b><br/>[Person]"]
    partner["👤<br/><b>Partner</b><br/>[Person]"]

    %% Main System Boundary
    subgraph saas["SaaS Application [Software System]"]
        direction TB
        ui["📋<br/><b>Web UI</b><br/>[Container]"]
        api["⚙️<br/><b>API Gateway</b><br/>[Container]"]
        workers["🔄<br/><b>Workers</b><br/>[Container]"]
        db[("💾<br/><b>Primary DB</b><br/>[Database]")]

        class employee,admin Person
        class partner PersonExt
        class ui,api,workers System
        class db SystemDb
        cache[("⚡<br/><b>Cache</b><br/>[Data Store]")]
        queue@{ shape: das, label: "📨<br/><b>Message Queue</b><br/>[System]" }

        class cache SystemDb
        class queue SystemQueue

        ui -->|REST| api
        api -->|Query| db
        api -->|Query| cache
        workers -->|Consume| queue
        workers -->|Write| db
    end
    class saas SystemBoundary;

    %% External Systems
    analytics["📋<br/><b>Analytics<br/>Platform</b><br/>[External System]"]
    auth["🔐<br/><b>OAuth Provider</b><br/>[External System]"]
    webhook["🔗<br/><b>Webhook<br/>Service</b><br/>[External System]"]

    class analytics,auth,webhook SystemExt

    %% Relationships
    employee -->|"Use Application<br/>[HTTPS]"| saas
    admin -->|"Manage System<br/>[HTTPS]"| saas
    partner -->|"Integration<br/>[REST API]"| saas
    saas -->|"Send Events<br/>[HTTPS]"| analytics
    saas -->|"Authenticate<br/>[OAuth 2.0]"| auth
    saas -->|"Post Events<br/>[Webhooks]"| webhook
```

---

## Complete Context Diagram Example 4: IoT System

```mermaid
flowchart TB
    %% Style definitions
    classDef Person fill:#08427b,stroke:#073b6f,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef PersonExt fill:#999999,stroke:#8a8a8a,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef System fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef SystemExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef SystemDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef SystemQueue fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef device fill:#0f5daf,stroke:#073b6f,color:#fff,stroke-width:2px;
    classDef SystemBoundary fill:#fff,stroke:#999,stroke-width:2px,stroke-dasharray: 5 5,color:#444;

    %% Actors
    operator["👤<br/><b>IoT Operator</b><br/>[Person]"]
    technician["👤<br/><b>Technician</b><br/>[Person]"]

    class operator,technician Person

    sensor["📡<br/><b>IoT Sensors</b><br/>[Device]"]

    class sensor device

    %% Main System Boundary
    subgraph iot["IoT Platform [Software System]"]
        direction TB
        ingest["📥<br/><b>Data Ingestion</b><br/>[Container]"]
        api["⚙️<br/><b>API Server</b><br/>[Container]"]
        analytics["📋<br/><b>Analytics<br/>Engine</b><br/>[Container]"]
        ui["📋<br/><b>Dashboard</b><br/>[Container]"]

        timeseries[("⏱️<br/><b>Time Series DB</b><br/>[Database]")]
        cache[("⚡<br/><b>Cache</b><br/>[Data Store]")]
        queue@{ shape: das, label: "📨<br/><b>Event Queue</b><br/>[System]" }

        class ingest,api,analytics,ui System
        class timeseries,cache SystemDb
        class queue SystemQueue

        ingest -->|Insert| queue
        queue -->|Consume| analytics
        analytics -->|Write| timeseries
        api -->|Query| timeseries
        api -->|Query| cache
        ui -->|Query| api
    end
    class iot SystemBoundary;

    %% External Systems
    alerts["🔔<br/><b>Alert System</b><br/>[External System]"]
    storage@{ shape: lin-cyl, label: "☁️<br/><b>Cloud Storage</b><br/>[External System]" }

    class alerts,storage SystemExt

    %% Relationships
    sensor -->|"Send Telemetry<br/>[MQTT]"| iot
    operator -->|"Monitor & Control<br/>[HTTPS]"| iot
    technician -->|"Manage Devices<br/>[HTTPS]"| iot
    iot -->|"Archive Data<br/>[REST API]"| storage
    iot -->|"Trigger Alerts<br/>[Webhooks]"| alerts
```

---

## Styling Combinations

### Person with Different Icons

```mermaid
flowchart TB
    classDef Person fill:#08427b,stroke:#073b6f,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef PersonExt fill:#999999,stroke:#8a8a8a,color:#fff,rx:20px,ry:20px,stroke-width:2px;

    u1["👤<br/><b>User</b>"]
    u2["👨‍💼<br/><b>Manager</b>"]
    u3["👩‍💻<br/><b>Developer</b>"]
    u4["🔧<br/><b>Operator</b>"]
    u5["🛪<br/><b>Guest</b>"]

    class u1,u2,u3,u4 Person
    class u5 PersonExt
```

---

### System with Different Icons

```mermaid
flowchart TB
    classDef System fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef SystemExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;

    s1["📋<br/><b>Web App</b>"]
    s2["📱<br/><b>Mobile App</b>"]
    s3["⚙️<br/><b>API</b>"]
    s4["🔄<br/><b>Batch Service</b>"]
    s5["🔗<br/><b>Legacy System</b>"]

    class s1,s2,s3,s4 System
    class s5 SystemExt
```

---

> **Arrow styles and directional relationships:** see [C4-Relationships-Layouts-Cheatsheet.md](./C4-Relationships-Layouts-Cheatsheet.md) for `Rel`, `BiRel`, `Rel_U/D/L/R`, and arrow-style variations.

---

## Best Practices

### ✅ DO's

- Use consistent icon-emoji combinations per element type
- Always label with type in brackets: `[Person]`, `[Software System]`, `[Database]`, `[Container]`, `[External System]`
- Use subgraphs with `SystemBoundary` class to show system boundaries
- Keep descriptions concise (max 3 lines per element)
- Use dashed lines for optional/deprecated relationships
- Include protocol/technology in relationship labels

### ❌ DON'Ts

- Don't mix colors randomly—stick to the C4 palette
- Don't use inconsistent corner radius (rx/ry)—all persons should have `rx:20px,ry:20px`
- Don't forget stroke colors; they make shapes pop
- Don't create super dense diagrams—aim for max 6-8 elements per context
- Don't omit type labels—they're key to C4

---

## Copy-Paste Template

Use this as a starting point for your own context diagram:

```mermaid
flowchart TB
    %% ===== STYLES =====
    classDef Person fill:#08427b,stroke:#073b6f,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef PersonExt fill:#999999,stroke:#8a8a8a,color:#fff,rx:20px,ry:20px,stroke-width:2px;
    classDef System fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef SystemExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef SystemDb fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef SystemDbExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef SystemQueue fill:#1168bd,stroke:#0f5daf,color:#fff,stroke-width:2px;
    classDef SystemQueueExt fill:#999999,stroke:#8a8a8a,color:#fff,stroke-width:2px;
    classDef SystemBoundary fill:#fff,stroke:#999,stroke-width:2px,stroke-dasharray: 5 5,color:#444;
    classDef EnterpriseBoundary fill:#fff,stroke:#444,stroke-width:3px,stroke-dasharray: 5 5,color:#444;

    subgraph main["Title of the diagram"]
        direction TB
        %% ===== ACTORS =====
        user1["👤<br/><b>User</b><br/>[Person]"]

        class user1 Person

        %% ===== MAIN SYSTEM BOUNDARY =====
        subgraph sys["Main System [Software System]"]
            direction TB
            comp1["📋<br/><b>Component 1</b><br/>[Container]"]
            comp2["📋<br/><b>Component 2</b><br/>[Container]"]
            db[("💾<br/><b>Database</b><br/>[Database]")]

            class comp1,comp2 System
            class db SystemDb

            comp1 --> comp2
            comp2 --> db
        end
        class sys SystemBoundary;

        %% ===== EXTERNAL SYSTEMS =====
        ext1["🔗<br/><b>External System</b><br/>[External System]"]

        class ext1 SystemExt

        %% ===== RELATIONSHIPS =====
        user1 -->|"Interaction<br/>[Protocol]"| comp1
        comp1 -->|"Integration<br/>[Protocol]"| ext1

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

### Warning

Don't use relationships from boundary elements directly; always connect through the components inside the boundary. Styling will not be applied correctly if you connect to the boundary itself.

> See the [README](./README.md#mermaid-rendering-tip) for a Mermaid rendering config tip.
