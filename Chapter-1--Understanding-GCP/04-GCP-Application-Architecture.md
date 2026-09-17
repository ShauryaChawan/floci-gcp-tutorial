# 4. How GCP Services Work Together 🔗

Learning individual services is useful, but real applications rarely use only one cloud service.

The more important skill is understanding **how services communicate and work together**.

## 🏗️ A Simple Application

Imagine a restaurant ordering platform.

A simplified architecture might look like this:

```mermaid
flowchart TD
    C[👤 Client] --> CR[🚀 Cloud Run<br/>API Service]
    CR --> FS[🔥 Firestore<br/>Data]
    CR --> PS[📨 Pub/Sub<br/>Events]
    CR --> CS[🪣 Cloud Storage]
    PS --> N[🔔 Notification Service]
    PS --> A[📊 Analytics Service]
```

The diagram is intentionally simplified. Its purpose is to demonstrate a common cloud architecture pattern: **one service does not need to own every responsibility**.

## 🔄 Request-Response Communication

A client may make a request to an application running on Cloud Run:

```mermaid
sequenceDiagram
    participant C as 👤 Client
    participant A as 🚀 Cloud Run
    participant D as 🔥 Firestore
    C->>A: HTTP request
    A->>D: Read / write data
    D-->>A: Data / result
    A-->>C: HTTP response
```

The client waits for a response.

This is a **synchronous** interaction.

## 📨 Asynchronous Communication

Now consider sending an email after an order is created.

The API does not necessarily need to wait for the email to be delivered.

Instead:

```mermaid
flowchart LR
    API[🚀 API] -->|publish order.created| PS[📨 Pub/Sub]
    PS -->|deliver message| N[🔔 Notification Service]
```

The API can finish the order request while another service handles the notification work.

This is an example of **asynchronous communication**.

## 🧩 Why This Separation Helps

Separating responsibilities can make systems easier to evolve.

For example:

```mermaid
flowchart LR
    O[🛒 Order API] --> D[🗄️ Database]
    O --> E[📨 Event System]
    E --> N[🔔 Notification]
    E --> A[📊 Analytics]
    E --> L[🎁 Loyalty]
```

The order service does not need to contain all notification, analytics, and loyalty logic itself.

## ⚠️ A Service Is Not an Architecture

Knowing that an application uses Cloud Run does not tell us much about the complete architecture.

For example, these are both Cloud Run applications:

```mermaid
flowchart LR
    C1[👤 Client] --> A1[🚀 Cloud Run] --> D1[🔥 Firestore]
```

and:

```mermaid
flowchart LR
    C2[👤 Client] --> A2[🚀 Cloud Run]
    A2 --> P[📨 Pub/Sub]
    P --> W[⚙️ Worker]
    W --> SQL[🗄️ Cloud SQL]
    W --> CS[🪣 Cloud Storage]
```

The important architectural question is not simply:

> ❌ **Which GCP service are you using?**

It is:

> ✅ **Why is this service being used here, and how does it interact with the rest of the system?**

## 🔀 Data Flow Matters

For every application architecture, try to trace the data.

For an order workflow:

```mermaid
flowchart TD
    S[1️⃣ Customer submits order] --> A[2️⃣ API receives request]
    A --> D[3️⃣ Order is stored]
    D --> E[4️⃣ order.created event is published]
    E --> N[🔔 Notification]
    E --> AN[📊 Analytics]
```

This data-flow perspective will become increasingly important when we study event-driven systems.

## 🏠 Where Floci Fits

In this tutorial, Floci provides a local environment in which supported GCP-like services can be exercised without requiring the corresponding real GCP infrastructure.

For example, instead of immediately deploying an application to real Cloud Run, you can first learn the service interaction patterns locally where supported.

> ⚠️ **Important:** An emulator should not be treated as proof that a production architecture will behave identically on GCP. Real GCP introduces additional concerns such as authentication, networking, regional placement, quotas, managed infrastructure, reliability, scaling, billing, and production operations.

## ✅ What You Should Remember

- ✅ Real applications combine multiple services.
- 🔄 Some communication is synchronous and some is asynchronous.
- 🔗 Architecture is about relationships and data flow, not just a list of products.
- 🧩 Each service should have a reason for being part of the design.
- ⚠️ Local emulation helps you learn concepts, but real GCP behavior must eventually be validated in the real platform.

## 🧪 Checkpoint

For this requirement:

> **"When a customer places an order, save the order and notify several independent services that an order was created."**

Think about:

1. 🤔 Which component receives the request?
2. 🤔 Where should the order data be stored?
3. 🤔 How could multiple services receive the event without the API directly calling each one?

Do not worry about choosing the exact services yet. The goal is to identify the architectural problems first.
