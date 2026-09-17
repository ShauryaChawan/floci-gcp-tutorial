# 3. Working with `gcloud storage` 🛠️

## 🎯 Learning Objective

By the end of this topic, you should be able to use the Google Cloud CLI to create buckets and perform basic Cloud Storage operations such as listing, uploading, downloading, and deleting objects.

The goal is not to memorize commands. The goal is to understand what resource each command operates on and what changes as a result.

## ☁️ The `gcloud storage` Command Group

Google Cloud CLI provides the `gcloud storage` command group for interacting with Cloud Storage.

The general pattern is:

```text
gcloud storage <operation> <resource>
```

Cloud Storage resources are commonly represented with:

```text
gs://bucket-name
```

or:

```text
gs://bucket-name/object-name
```

## 📋 List Buckets

To list buckets visible to the current Google Cloud configuration:

```bash
gcloud storage buckets list
```

Conceptually:

```text
Google Cloud project
        │
        ├── Bucket A
        ├── Bucket B
        └── Bucket C
```

This operates at the **bucket level**.

## 🪣 Create a Bucket

Create a bucket with:

```bash
gcloud storage buckets create gs://YOUR-BUCKET-NAME
```

Example:

```bash
gcloud storage buckets create gs://floci-demo-storage
```

Bucket names need to satisfy Cloud Storage naming requirements and must be unique as required by the service.

The command creates the bucket; it does not upload a file.

## 📦 List Objects

To list objects in a bucket:

```bash
gcloud storage ls gs://YOUR-BUCKET-NAME/
```

For example:

```bash
gcloud storage ls gs://floci-demo-storage/
```

If the bucket contains:

```text
hello.txt
images/logo.png
menu.pdf
```

the command shows those objects or prefixes in the bucket.

## ⬆️ Upload an Object

Upload a local file with:

```bash
gcloud storage cp ./hello.txt gs://YOUR-BUCKET-NAME/
```

Example:

```bash
gcloud storage cp ./menu.pdf gs://floci-demo-storage/
```

The direction is:

```text
Local machine
     │
     │ upload
     ▼
Cloud Storage
     │
     ▼
Object
```

The `cp` command copies data; the source is local and the destination is the Cloud Storage URI.

## ⬇️ Download an Object

Download an object with:

```bash
gcloud storage cp gs://YOUR-BUCKET-NAME/hello.txt ./hello.txt
```

The direction is reversed:

```text
Cloud Storage
     │
     │ download
     ▼
Local machine
```

This is an important detail to understand when reading CLI commands.

## 🗑️ Delete an Object

Delete an object with:

```bash
gcloud storage rm gs://YOUR-BUCKET-NAME/hello.txt
```

This removes the specified object from the bucket, subject to the bucket's configuration and any relevant retention/versioning behavior.

Be especially careful with commands that can operate recursively or affect many objects.

## 🔍 Understanding the Resource in Each Command

Compare these commands:

```bash
gcloud storage buckets list
```

```bash
gcloud storage ls gs://floci-demo-storage/
```

```bash
gcloud storage cp ./menu.pdf gs://floci-demo-storage/
```

```bash
gcloud storage rm gs://floci-demo-storage/menu.pdf
```

They operate on different levels:

```text
buckets list
    │
    └── Buckets

storage ls
    │
    └── Objects/prefixes in a bucket

storage cp
    │
    └── Copies object data between locations

storage rm
    │
    └── Removes a specified object
```

## 🧪 Mini Workflow

Create a local file:

```bash
echo "Hello Cloud Storage" > hello.txt
```

Create a bucket:

```bash
gcloud storage buckets create gs://YOUR-BUCKET-NAME
```

Upload:

```bash
gcloud storage cp hello.txt gs://YOUR-BUCKET-NAME/
```

List:

```bash
gcloud storage ls gs://YOUR-BUCKET-NAME/
```

Download:

```bash
gcloud storage cp gs://YOUR-BUCKET-NAME/hello.txt downloaded.txt
```

Verify:

```bash
cat downloaded.txt
```

Delete:

```bash
gcloud storage rm gs://YOUR-BUCKET-NAME/hello.txt
```

## 🧠 Read Commands Like an Engineer

Instead of memorizing:

```bash
gcloud storage cp ./menu.pdf gs://bucket/menu.pdf
```

read it as:

```text
Source:
./menu.pdf

        │
        │ copy
        ▼

Destination:
gs://bucket/menu.pdf
```

Once this mental model is clear, other `cp` operations become easier to reason about.

## ⚠️ Common Mistakes

### Mistake 1 — Confusing bucket and object

This:

```text
gs://my-bucket
```

identifies the bucket.

This:

```text
gs://my-bucket/menu.pdf
```

identifies an object in that bucket.

### Mistake 2 — Reversing upload and download

Upload:

```text
local → Cloud Storage
```

Download:

```text
Cloud Storage → local
```

### Mistake 3 — Treating object names as filesystem paths

```text
gs://my-bucket/images/logo.png
```

contains an object name:

```text
images/logo.png
```

The `/` provides a folder-like naming convention.

## 🧩 Floci vs Real GCP

If you are using Floci as a local emulator, the commands may look similar to real Google Cloud CLI workflows because the tutorial is intentionally teaching the same resource concepts.

However, emulator behavior and real Google Cloud behavior are not necessarily identical.

Always distinguish:

```text
Learning the GCP API/resource model
            ≠
Testing every production GCP behavior
```

Real GCP can introduce production concerns such as IAM, billing, regional placement, organization policies, networking, retention requirements, and other controls.

## ✅ What You Should Remember

1. `gcloud storage` is the Cloud Storage command group in the Google Cloud CLI.
2. `gcloud storage buckets list` lists buckets.
3. `gcloud storage ls` lists objects/prefixes.
4. `gcloud storage cp` copies data between local and Cloud Storage locations.
5. `gcloud storage rm` removes objects.
6. `gs://bucket` refers to a bucket.
7. `gs://bucket/object` refers to an object.
8. Always identify the source and destination before running a copy command.
9. Understand the resource operation instead of memorizing CLI syntax.

## 🧪 Checkpoint

Without looking at the notes, explain what each command does:

```bash
gcloud storage buckets list
```

```bash
gcloud storage ls gs://my-bucket/
```

```bash
gcloud storage cp ./invoice.pdf gs://my-bucket/invoices/invoice.pdf
```

```bash
gcloud storage cp gs://my-bucket/invoices/invoice.pdf ./invoice.pdf
```

```bash
gcloud storage rm gs://my-bucket/invoices/invoice.pdf
```
