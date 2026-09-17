# GCP Learning Chapters

This is the learning roadmap for the **Floci GCP Tutorial**.

The chapters are intentionally ordered from fundamentals → individual services → event-driven systems → containers → security/observability → multi-service application architecture.

> **Learning principle:** Do not just memorize `gcloud` commands. For every chapter, understand **what problem the GCP service solves, why you would use it, how it connects to other services, and what changes when you move from Floci to real GCP**.

---

## Phase 0 — Environment & GCP Fundamentals

### Chapter 01 — Understanding GCP
- What Google Cloud is
- Projects and resources
- Regions and zones
- Managed services vs. self-managed infrastructure
- The role of APIs and the `gcloud` CLI
- Floci vs. real GCP

### Chapter 02 — Setting Up Your Local GCP Lab

**Before starting this chapter, read the dedicated setup guide:**

👉 [SETUP.md — Floci GCP Setup Guide](./SETUP.md)

The setup guide contains the platform-specific instructions for:

- Windows 11 / PowerShell
- macOS
- Linux
- Docker / Docker Desktop
- Floci CLI
- Google Cloud CLI (`gcloud`)
- Local emulator endpoint configuration
- Credential-free local development
- Setup verification
- Troubleshooting with AI

This chapter is about understanding **what was configured and why**, rather than repeating the installation instructions.

#### Concepts
- Docker and Floci
- Google Cloud CLI
- Local project configuration
- Emulator endpoints
- Credential-free local development
- Understanding `gcloud` configuration
- Verifying the local environment
- Local GCP project: `floci-local`

**Hands-on:** Verify your local `floci-local` environment and confirm that `gcloud` can communicate with the Floci emulator.

---

# Phase 1 — Cloud Storage

### Chapter 03 — Cloud Storage Fundamentals
- Buckets and objects
- Object paths
- Uploading and downloading files
- Listing and deleting objects
- Bucket-level concepts
- Working with `gcloud storage`

**Hands-on:** Build a small local file-storage workflow.

### Chapter 04 — Storage in an Application
- Application uploads
- Reading objects from an application
- File-processing workflows
- Storage + application integration
- Emulator limitations vs. real GCS

**Hands-on:** Build a simple document/image upload workflow.

---

# Phase 2 — Data Services

### Chapter 05 — Firestore
- Documents and collections
- Reads and writes
- Queries
- Updates and deletes
- Data modeling concepts
- When document databases make sense

**Hands-on:** Build a small restaurant/customer data store.

### Chapter 06 — Datastore
- Entities and keys
- Properties
- Queries
- Datastore vs. Firestore concepts
- Choosing a data model

**Hands-on:** Store and query structured application entities.

### Chapter 07 — BigQuery
- Data warehouse concepts
- Datasets and tables
- Loading data
- SQL analytics
- Aggregations
- Analytical vs. transactional workloads

**Hands-on:** Analyze restaurant/order data with SQL.

---

# Phase 3 — Messaging & Event-Driven Architecture

### Chapter 08 — Pub/Sub Fundamentals
- Topics
- Subscriptions
- Publishers
- Subscribers
- Message delivery
- Asynchronous processing

**Hands-on:** Publish and consume restaurant order events.

### Chapter 09 — Building an Event-Driven Application
- Producers and consumers
- Decoupling services
- Event-driven workflows
- Failure and retry concepts
- Connecting Pub/Sub with application services

**Hands-on:** Build an order-event processing pipeline.

### Chapter 10 — Cloud Functions
- Serverless functions
- Function triggers
- Event-driven execution
- Stateless application design
- Connecting Functions to Pub/Sub and storage

**Hands-on:** Process an event using a function.

### Chapter 11 — Cloud Tasks
- Task queues
- Background processing
- Delayed execution
- Retry concepts
- HTTP-based task processing

**Hands-on:** Build a background-job workflow.

### Chapter 12 — Cloud Scheduler
- Scheduled jobs
- Cron concepts
- HTTP-triggered workflows
- Scheduler + Functions/Cloud Run

**Hands-on:** Create a scheduled data-processing workflow.

### Chapter 13 — Eventarc
- Event routing
- Event-driven architecture
- Connecting events to services
- Eventarc vs. direct service integration

**Hands-on:** Build an event-routing workflow where supported by Floci.

---

# Phase 4 — Containers & Application Deployment

### Chapter 14 — Containers for GCP
- Why containers matter
- Docker images
- Container lifecycle
- Stateless services
- Containerized application design

**Hands-on:** Containerize a small application.

### Chapter 15 — Cloud Run
- Serverless containers
- Deploying HTTP applications
- Revisions
- Request-based execution
- Scaling concepts
- Cloud Run + database/service integration

**Hands-on:** Run the containerized application locally through the Floci-supported Cloud Run workflow.

### Chapter 16 — Cloud Run Application Architecture
- Application + database
- Application + storage
- Application + Pub/Sub
- Secrets and configuration
- Service-to-service architecture

**Hands-on:** Combine several services into one application.

---

# Phase 5 — Security & Identity

### Chapter 17 — IAM Fundamentals
- Authentication vs. authorization
- Users
- Service accounts
- Roles
- Permissions
- Least privilege

**Important:** Floci can help demonstrate concepts, but real Google Cloud IAM behavior and enterprise identity management require a real GCP environment.

### Chapter 18 — Service Accounts & Application Identity
- Why applications need identities
- Service-account concepts
- Application-to-service authentication
- Workload identity concepts
- Local emulator authentication vs. real GCP authentication

### Chapter 19 — Secret Manager
- Secrets vs. configuration
- Creating and retrieving secrets
- Application secret management
- Avoiding secrets in source code

**Hands-on:** Connect an application to a secret.

### Chapter 20 — KMS & Encryption Concepts
- Encryption at rest
- Encryption keys
- Key-management concepts
- Application/resource encryption workflows

**Important:** Production-grade Cloud KMS behavior and real key management require real GCP infrastructure.

---

# Phase 6 — Databases & Infrastructure Services

### Chapter 21 — Cloud SQL
- Managed relational databases
- PostgreSQL/MySQL concepts
- Application-to-database connectivity
- Connection management
- Backups and high availability concepts

**Hands-on:** Connect an application to a SQL database where supported by the emulator.

### Chapter 22 — GKE & Kubernetes Fundamentals
- Containers vs. Kubernetes
- Pods
- Deployments
- Services
- Scaling concepts
- Kubernetes architecture
- GKE vs. self-managed Kubernetes

**Important:** A real production GKE cluster requires Google Cloud infrastructure.

---

# Phase 7 — Observability

### Chapter 23 — Cloud Logging
- Application logs
- Structured logs
- Log levels
- Searching logs
- Debugging distributed applications

**Hands-on:** Generate and inspect application/service logs.

### Chapter 24 — Cloud Monitoring
- Metrics
- Monitoring concepts
- Service health
- Application observability
- Alerts and dashboards concepts

**Important:** Full production monitoring, managed metrics, alerting behavior, and Google Cloud infrastructure telemetry require real GCP.

---

# Phase 8 — Firebase & Additional GCP Services

### Chapter 25 — Firebase Authentication
- Authentication concepts
- Users
- Authentication flows
- Connecting authentication to an application
- Firebase Auth vs. application-managed authentication

### Chapter 26 — Resource Manager & Service Usage
- Project-level concepts
- Service enablement
- Resource hierarchy concepts
- Managing cloud resources

### Chapter 27 — IAM Credentials & STS
- Credential exchange concepts
- Temporary credentials
- Identity federation concepts
- Where these fit into real GCP architectures

### Chapter 28 — Kafka & Event Streaming
- Kafka fundamentals
- Topics and consumers
- Event streaming vs. Pub/Sub
- When Kafka-style architecture is useful

---

# Phase 9 — Putting Everything Together

### Chapter 29 — Build a Restaurant Order Platform

Build one complete application using the concepts learned throughout the tutorial.

Example architecture:

```text
                         Application
                              │
             ┌────────────────┼────────────────┐
             │                │                │
             ▼                ▼                ▼
        Cloud Storage      Pub/Sub         Cloud Run
             │                │                │
             │                ▼                │
             │          Cloud Functions        │
             │                │                │
             └────────┬───────┴────────┬───────┘
                      ▼                ▼
                  Firestore        Cloud SQL
                      │
                      └───────┬────────┘
                              ▼
                          BigQuery
                              │
                              ▼
                           Analytics
```

Students should implement the system incrementally rather than creating everything at once.

### Chapter 30 — Production Architecture: Floci → Real GCP

Compare the local application with a real Google Cloud deployment.

Topics include:

- What can be copied directly
- What needs new configuration
- Authentication changes
- Real IAM
- Networking
- Regions and zones
- Managed infrastructure
- Scaling
- Reliability
- Monitoring
- Security
- Costs and billing
- Production deployment strategy

This chapter explicitly identifies which parts of the previous chapters require a real GCP account.

---

# Chapter Format

Every chapter should follow a consistent structure:

1. **What are we learning?**
2. **Why does this service exist?**
3. **Core GCP concepts**
4. **How the service fits into an architecture**
5. **Floci setup/configuration**
6. **Commands to run**
7. **Hands-on exercise**
8. **Expected result**
9. **Troubleshooting**
10. **Floci limitations**
11. **How this differs on real GCP**
12. **What you should understand before moving on**

---

# Learning Rule

Do not move to the next chapter just because the commands worked.

A student should be able to explain:

> **What problem does this GCP service solve, why would I use it, how does it communicate with other services, and what changes when I deploy it on real GCP?**

That is the skill this tutorial is intended to build.
