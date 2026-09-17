# 3. Understanding GCP Service Categories

GCP contains a large number of services. Trying to memorize them one by one is not a useful way to learn cloud architecture.

A better approach is to group services by the problem they solve.

## Compute

Compute services provide places where application workloads can run.

Examples:

- Cloud Run
- Google Kubernetes Engine (GKE)
- Cloud Functions

The important question is:

> Where should my application code execute?

We will study containers, Cloud Run, and GKE in later chapters.

## Storage

Storage services hold files and other persistent data.

Example:

- Cloud Storage

A storage bucket can contain objects such as images, videos, documents, backups, and application-generated files.

We will use Cloud Storage early in the hands-on portion of the tutorial.

## Databases

Database services store structured or application data.

Examples:

- Firestore
- Datastore
- Cloud SQL
- BigQuery

These services solve different data problems. A document database, relational database, and analytics warehouse should not be treated as interchangeable products.

## Messaging and Eventing

Distributed applications often need services to communicate without being tightly coupled.

Examples:

- Pub/Sub
- Cloud Tasks
- Cloud Scheduler
- Eventarc

For example:

```text
Order Service
     |
     | publish event
     v
   Pub/Sub
     |
     +------> Notification Service
     |
     +------> Analytics Service
```

This allows multiple consumers to react to an event without the original service directly calling every consumer.

## Security and Identity

Applications need to control who or what can access resources.

Examples:

- IAM
- Service Accounts
- Secret Manager
- Cloud KMS
- IAM Credentials
- Security Token Service (STS)

These services become especially important when applications communicate with other GCP services.

## Observability

After an application is running, you need to understand what it is doing.

Examples:

- Cloud Logging
- Cloud Monitoring

Logging helps you understand events and application output. Monitoring helps you observe metrics and system behavior.

## Data and Analytics

Some workloads require large-scale data processing and analytical queries.

A major example is **BigQuery**, which is designed for analytics rather than serving as a general-purpose transactional database.

## Application Platforms

Some GCP services abstract away much of the underlying infrastructure.

For example, with Cloud Run, you provide a containerized application and Google manages the underlying execution infrastructure.

This is different from managing virtual machines or Kubernetes clusters yourself.

## Why Categories Matter

When designing an application, start with the problem rather than the product name.

For example:

```text
I need to store user-uploaded images.
        |
        v
Object storage problem
        |
        v
Cloud Storage
```

Or:

```text
I need several services to react to an order-created event.
        |
        v
Messaging/eventing problem
        |
        v
Pub/Sub
```

This problem-first approach makes it easier to learn new cloud services because you can map an unfamiliar service to the problem it solves.

## What You Should Remember

A useful first-level classification is:

| Category | Example Services | Typical Problem |
|---|---|---|
| Compute | Cloud Run, GKE, Cloud Functions | Run application workloads |
| Storage | Cloud Storage | Store files/objects |
| Databases | Firestore, Datastore, Cloud SQL | Store application data |
| Analytics | BigQuery | Analyze large datasets |
| Messaging | Pub/Sub, Cloud Tasks | Decouple workloads |
| Scheduling/Eventing | Scheduler, Eventarc | Trigger work and route events |
| Identity/Security | IAM, Secret Manager, KMS | Control and protect access |
| Observability | Logging, Monitoring | Understand system behavior |

Do not worry about remembering every service yet. The later chapters will introduce these services when there is a concrete problem for them to solve.

## Checkpoint

Take these three requirements and identify the category involved:

1. Store a restaurant's menu images.
2. Send an `order.created` event to multiple services.
3. Run a containerized API.

Expected categories:

1. Storage
2. Messaging/Eventing
3. Compute
