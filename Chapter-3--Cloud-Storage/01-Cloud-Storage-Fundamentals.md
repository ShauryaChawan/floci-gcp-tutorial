# 1. Cloud Storage Fundamentals ☁️

## 🎯 Learning Objective

By the end of this topic, you should be able to explain what Google Cloud Storage is, what problem object storage solves, and where Cloud Storage fits in a modern application architecture.

## ☁️ What is Cloud Storage?

Google Cloud Storage is Google's **managed object storage service**.

Instead of storing files on the disk attached to an application server, an application can store data as **objects inside buckets** managed by Google Cloud.

Typical data stored in Cloud Storage includes:

- Images
- Videos
- PDFs and documents
- Backups
- Exports
- Application-generated files
- Large binary data

The two concepts you must remember are:

```text
Bucket = container
Object = stored data
```

## 🤔 Why Object Storage?

Imagine a restaurant SaaS application where restaurants upload:

```text
logo.png
menu.pdf
burger.jpg
pizza.jpg
invoice-2026-09.pdf
```

If these files are stored only on an application server's local disk, the files become coupled to that server.

With multiple application servers, this becomes harder to manage:

```text
                 Load Balancer
                      │
             ┌────────┴────────┐
             ▼                 ▼
        Application 1      Application 2
          /uploads           /uploads
```

The application now has to deal with questions such as:

- Which server has the file?
- What happens when a server is replaced?
- How do multiple servers share uploads?
- How does storage grow independently of compute?

Cloud Storage separates **application compute** from **object storage**.

```text
                 Application
                      │
                      ▼
               Cloud Storage
                      │
                  Bucket
                      │
             ┌────────┼────────┐
             ▼        ▼        ▼
          image     invoice    PDF
          object     object   object
```

## 🧠 Object Storage Mental Model

Cloud Storage is best understood as an object store rather than as a traditional filesystem.

Think about this path:

```text
restaurants/123/menu.pdf
```

It may look like a directory structure:

```text
restaurants/
└── 123/
    └── menu.pdf
```

Conceptually, however, Cloud Storage stores an object whose **name** is:

```text
restaurants/123/menu.pdf
```

The `/` characters are part of the object name. This distinction becomes important when you reason about listing, prefixes, application design, and APIs.

## 🔗 `gs://` URI

Cloud Storage commonly represents a bucket and object using the `gs://` URI scheme.

Example:

```text
gs://floci-restaurant-files/restaurants/123/menu.pdf
```

Break it down:

```text
gs://
  │
  └── Cloud Storage URI scheme

floci-restaurant-files
  │
  └── Bucket name

restaurants/123/menu.pdf
  │
  └── Object name
```

You will use this notation frequently with the `gcloud storage` CLI.

## 🏗️ Cloud Storage in an Application

A common application architecture separates business metadata from file data.

```text
                 Restaurant Application
                         │
             ┌───────────┴───────────┐
             ▼                       ▼
        Application DB          Cloud Storage
             │                       │
             │                  menu.pdf
             │                  logo.png
             ▼                  food.jpg
       File metadata
```

For example, a database record could contain:

```text
restaurant_id: 123
file_type: menu
object_name: restaurants/123/menu.pdf
```

The actual file bytes live in Cloud Storage.

This creates a useful separation:

> **Database → business/application metadata**  
> **Cloud Storage → file/object data**

## 🆚 Cloud Storage vs Persistent Disk

Cloud Storage and Persistent Disk solve different storage problems.

| Cloud Storage | Persistent Disk |
|---|---|
| Object storage | Block storage |
| Bucket/object model | Disk/block-device model |
| Accessed through storage APIs/tools | Attached to compute resources |
| Good for files, media, backups and exports | Commonly used for VM/application filesystem data |
| Independent from a specific VM | Commonly associated with compute resources |

A useful mental model is:

```text
Compute Engine
      │
      └── Persistent Disk
              │
              └── OS / filesystem

Application
      │
      └── Cloud Storage
              │
              ├── images
              ├── documents
              └── backups
```

## ✅ What You Should Remember

1. Cloud Storage is a managed **object storage** service.
2. A **bucket** is a container for objects.
3. An **object** is stored data with associated metadata.
4. An object name can contain `/` without requiring traditional directories.
5. `gs://bucket/object` identifies a Cloud Storage resource.
6. Cloud Storage lets storage exist independently from application compute.
7. Cloud Storage and Persistent Disk solve different storage problems.
8. Applications commonly store file data in Cloud Storage and keep related business metadata in a database.

## 🧪 Checkpoint

Try answering these without looking at the notes:

> **What problem does Cloud Storage solve that storing files on an application's local disk does not solve well?**

> **What is the difference between a bucket, an object, and an object name?**

> **Why does `restaurants/123/menu.pdf` not necessarily mean that Cloud Storage contains traditional directories called `restaurants` and `123`?**

> **What does `gs://my-bucket/menu.pdf` represent?**

A good answer should describe Cloud Storage as object storage and explain the relationship between the bucket and the object name.
