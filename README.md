# Floci GCP Tutorial

A hands-on, local-first tutorial for learning Google Cloud concepts and workflows using the **Floci GCP emulator**, Docker, and the Google Cloud CLI (`gcloud`).

The goal of this repository is to let students practice core GCP concepts **without needing a Google Cloud free trial, billing account, or paid GCP resources** for the lessons that are supported by Floci.

> **Important:** Floci is an emulator. This tutorial teaches GCP concepts and workflows locally, but it is not a replacement for working in a real Google Cloud project.

## What this tutorial covers

This tutorial focuses on practical GCP skills that can be exercised locally with Floci, including:

- Setting up and running the Floci GCP emulator with Docker.
- Configuring the Google Cloud CLI (`gcloud`) to work with the local emulator.
- Working with a local GCP project/environment such as `floci-local`.
- Using GCP-style CLI commands against local services.
- Cloud Storage (GCS) fundamentals such as buckets and objects.
- Firestore and Datastore concepts and basic operations.
- Pub/Sub concepts, topics, subscriptions, publishing, and consuming messages.
- BigQuery concepts, datasets, tables, and SQL-based analytics where supported by the emulator.
- Event-driven workflows using services such as Cloud Functions, Eventarc, Cloud Tasks, and Cloud Scheduler where supported.
- Running and integrating containers with Cloud Run where supported.
- Working with services such as Secret Manager, IAM/IAM Credentials, KMS, Logging, Monitoring, Cloud SQL, GKE, Firebase Auth, and related Floci-supported services at a conceptual and hands-on level where emulator support is available.
- Building small end-to-end exercises that combine multiple GCP services.
- Understanding how GCP services fit together in real application architectures.

## What this tutorial does **not** cover completely

A local emulator cannot reproduce the full Google Cloud platform. Some topics require a real GCP account and project, and some real-cloud behavior may differ from Floci.

You will need an **actual Google Cloud account/project** for topics such as:

- Creating and managing real Google Cloud projects in the Google Cloud Console.
- Billing accounts, budgets, billing alerts, quotas, and actual cloud costs.
- Real IAM identity management, organization policies, and enterprise access controls.
- Real service accounts, workload identity, OAuth flows, and production authentication/authorization behavior.
- Google Cloud networking, including VPCs, subnets, firewall rules, Cloud NAT, load balancers, VPNs, and private connectivity.
- Deploying workloads to Google's real managed infrastructure and regions/zones.
- Real GKE clusters and production Kubernetes infrastructure on Google Cloud.
- Actual Cloud Run deployments, autoscaling behavior, revisions, traffic splitting, and production networking.
- Real Cloud SQL instances, backups, replication, high availability, and managed database operations.
- Production-grade observability using Google's managed Monitoring and Logging infrastructure.
- Real KMS key management, key protection, rotation, and cloud-resource integration.
- Google Cloud networking/security integrations that depend on real infrastructure.
- Google-managed services or features that are not implemented by the emulator.
- Performance, latency, reliability, quotas, limits, autoscaling, and failure behavior of real GCP infrastructure.
- Google Cloud Console workflows and UI-specific features that are not exposed by Floci.
- Production deployment, operations, disaster recovery, regional/zone architecture, and cost optimization on real GCP.

## Floci vs. Real GCP

Think of Floci as a **practice environment**, not as a complete replica of Google Cloud.

| Topic | Floci local emulator | Real GCP account |
|---|---|---|
| Learn service concepts | ✅ | ✅ |
| Practice many CLI/API workflows | ✅ | ✅ |
| Practice application integration | ✅ | ✅ |
| Avoid cloud billing during local practice | ✅ | ❌ |
| Real Google infrastructure | ❌ | ✅ |
| Real billing/quota behavior | ❌ | ✅ |
| Full production IAM/security behavior | Limited | ✅ |
| Real networking/infrastructure | Limited | ✅ |
| Production-scale behavior | ❌ | ✅ |

## Prerequisites

You should have:

- Windows, macOS, or Linux.
- Docker / Docker Desktop.
- Google Cloud CLI (`gcloud`).
- Basic command-line knowledge.
- A willingness to learn by running commands and observing results.

**A Google Cloud free trial is not required for the Floci-based lessons.**

## Learning approach

The tutorial is designed to be followed as a sequence of practical chapters. Each chapter should explain:

1. The GCP concept.
2. What the equivalent service does in Floci.
3. The commands to run locally.
4. What output to expect.
5. A small hands-on exercise.
6. What changes when the same concept is used on real GCP.

The chapter sequence will be added separately so students can follow the material from fundamentals to multi-service application workflows.

## Disclaimer

Floci's supported services and emulator behavior can change between versions. A feature being listed as available in Floci does not necessarily mean that every capability or production behavior of the corresponding Google Cloud service is implemented locally.

Always consult the Floci documentation for the emulator version you are using when a chapter depends on a specific service capability.
