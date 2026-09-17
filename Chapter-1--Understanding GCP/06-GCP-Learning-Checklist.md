# 6. Chapter 1 Learning Checklist

Chapter 1 is about building the mental model you will use for the rest of the tutorial.

Before moving to Chapter 2, you should be comfortable explaining the following concepts in your own words.

## GCP Fundamentals

- [ ] What GCP is
- [ ] Why organizations use cloud platforms
- [ ] Why GCP is a collection of services rather than one product
- [ ] What a cloud service is responsible for

## Resource Hierarchy

- [ ] Organization
- [ ] Folder
- [ ] Project
- [ ] Resource
- [ ] Region
- [ ] Zone

## Service Categories

- [ ] Compute
- [ ] Storage
- [ ] Databases
- [ ] Analytics
- [ ] Messaging and eventing
- [ ] Identity and security
- [ ] Observability

## Architecture

- [ ] Synchronous communication
- [ ] Asynchronous communication
- [ ] Service-to-service communication
- [ ] Data flow
- [ ] Why applications use multiple services
- [ ] Why choosing a service should start with the problem being solved

## Cloud Infrastructure

- [ ] Difference between traditional infrastructure and cloud infrastructure
- [ ] Infrastructure abstraction
- [ ] Shared responsibility
- [ ] Why managed services reduce some infrastructure responsibilities but do not remove application responsibilities

## Local Learning Environment

You should also understand the role of Floci in this tutorial:

```text
Real GCP concepts
       |
       v
Local Floci environment
       |
       v
Hands-on practice
       |
       v
Real GCP later
```

The purpose of Floci is to give you a local environment for practicing supported GCP-like services. It should not be assumed that every emulator behavior is identical to production GCP.

## Final Chapter 1 Exercise

Without looking at the previous topics, describe this application in your own words:

```text
Customer
   |
   v
Restaurant API
   |
   +----> Database
   |
   +----> Object Storage
   |
   +----> Event System
               |
               +----> Notification Service
               |
               +----> Analytics Service
```

Answer these questions:

1. Why might the application use more than one GCP service?
2. Which interactions are likely to be synchronous?
3. Which interactions could be asynchronous?
4. Why might the application store files separately from application data?
5. Why might the API publish an event instead of directly calling every downstream service?

If you can explain the architecture without memorizing service definitions, you are ready for Chapter 2.
