# 98 — Pub/Sub Commands Cheat Sheet 📋

> ⚠️ **Important:** This is a last-minute revision sheet. Pub/Sub command support can differ between Floci and real Google Cloud. Run `--help` in the local environment and verify the exact command before using it in a lab.

## Environment

| Command | Purpose |
|---|---|
| `gcloud --version` | Check Google Cloud CLI version |
| `gcloud config list` | Inspect active gcloud configuration |
| `gcloud pubsub --help` | Inspect Pub/Sub command groups |
| `gcloud pubsub topics --help` | Inspect topic commands |
| `gcloud pubsub subscriptions --help` | Inspect subscription commands |

## Topics

| Operation | Typical command shape | Purpose |
|---|---|---|
| List topics | `gcloud pubsub topics list` | List available topics |
| Create topic | `gcloud pubsub topics create TOPIC_ID` | Create a topic |
| Describe topic | `gcloud pubsub topics describe TOPIC_ID` | Inspect a topic |
| Delete topic | `gcloud pubsub topics delete TOPIC_ID` | Delete a topic |
| Help | `gcloud pubsub topics --help` | Inspect supported operations |

## Publishing

| Operation | Typical command shape | Purpose |
|---|---|---|
| Publish message | `gcloud pubsub topics publish TOPIC_ID --message="MESSAGE"` | Publish a message |
| Publish JSON text | `gcloud pubsub topics publish TOPIC_ID --message='{"eventType":"OrderCreated"}'` | Publish JSON as message text |

> On Windows PowerShell, quoting/escaping JSON can require care. If a command behaves unexpectedly, first try a simple message and inspect `gcloud pubsub topics publish --help`.

## Subscriptions

| Operation | Typical command shape | Purpose |
|---|---|---|
| List subscriptions | `gcloud pubsub subscriptions list` | List subscriptions |
| Create subscription | `gcloud pubsub subscriptions create SUBSCRIPTION_ID --topic=TOPIC_ID` | Create subscription |
| Describe subscription | `gcloud pubsub subscriptions describe SUBSCRIPTION_ID` | Inspect subscription |
| Delete subscription | `gcloud pubsub subscriptions delete SUBSCRIPTION_ID` | Delete subscription |
| Help | `gcloud pubsub subscriptions --help` | Inspect supported operations |

## Consuming messages

A common pull-style command shape is:

```bash
gcloud pubsub subscriptions pull SUBSCRIPTION_ID --auto-ack
```

For learning acknowledgement behavior, inspect the supported flags before using `--auto-ack`. Automatic acknowledgement changes the experiment because the message is acknowledged as part of the command rather than after separate application processing.

Use:

```bash
gcloud pubsub subscriptions pull --help
```

## Restaurant example

```text
Topic:
orders-topic

Subscriptions:
notification-subscription
billing-subscription
analytics-subscription
```

Typical flow:

```text
Create topic
    ↓
Create subscription
    ↓
Publish OrderCreated
    ↓
Pull/consume message
    ↓
Process
    ↓
ACK
```

## Quick revision table

| Concept | Remember |
|---|---|
| Publisher | Produces message |
| Topic | Receives published messages |
| Message | Data being transported |
| Subscription | Consumer delivery path |
| Subscriber | Processes messages |
| ACK | Confirms successful processing |
| Redelivery | Message may be delivered again after failure/unacknowledged processing |
| Fan-out | Multiple independent subscriptions consume a topic |
| Idempotency | Duplicate processing does not create unintended side effects |

## Common command sequence

```bash
# Inspect commands
gcloud pubsub --help

# Create topic
gcloud pubsub topics create orders-topic

# Create subscription
gcloud pubsub subscriptions create orders-subscription --topic=orders-topic

# Publish
gcloud pubsub topics publish orders-topic --message="OrderCreated: ORD-1001"

# Pull
gcloud pubsub subscriptions pull orders-subscription
```

> ⚠️ Treat the sequence above as a **command-shape revision guide**, not a guarantee that every command behaves identically in Floci. Verify the local emulator's supported syntax before running it.
