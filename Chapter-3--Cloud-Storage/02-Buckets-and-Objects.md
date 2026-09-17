# 2. Buckets and Objects 🪣

## 🎯 Learning Objective

By the end of this topic, you should be able to explain buckets, objects, object names, bucket locations, and the difference between bucket-level and object-level concepts.

## 🪣 What is a Bucket?

A **bucket** is a container used to organize and store objects in Cloud Storage.

Example:

```text
Bucket: floci-restaurant-files
```

The bucket can contain many objects:

```text
floci-restaurant-files
│
├── logo.png
├── menu.pdf
├── images/burger.jpg
└── invoices/2026/001.pdf
```

A bucket is not the file itself. It is the storage container in which objects are stored.

## 📦 What is an Object?

An **object** is the data stored in Cloud Storage.

For example:

```text
gs://floci-restaurant-files/menu.pdf
```

Here:

```text
Bucket = floci-restaurant-files
Object = menu.pdf
```

An object has data and associated metadata. Its name is used to identify it within the bucket.

## 🏷️ Object Names

Objects can have names such as:

```text
logo.png
menu.pdf
images/burger.jpg
images/pizza.jpg
invoices/2026/001.pdf
```

The full object name is significant.

For example:

```text
images/burger.jpg
```

is different from:

```text
burger.jpg
```

They are different object names even if their contents are identical.

## 📁 Are Folders Real?

Cloud Storage uses an object namespace. A `/` in an object name can make objects appear organized into folders:

```text
restaurants/123/menu.pdf
restaurants/123/logo.png
```

Conceptually, these are object names:

```text
restaurants/123/menu.pdf
restaurants/123/logo.png
```

rather than files inside a traditional POSIX directory tree.

This is an important distinction when working with object-storage APIs and prefixes.

## 🔗 Bucket + Object

A Cloud Storage URI combines the bucket and object name:

```text
gs://bucket-name/object-name
```

Example:

```text
gs://floci-restaurant-files/restaurants/123/menu.pdf
```

Breakdown:

```text
gs://
    │
    └── Cloud Storage scheme

floci-restaurant-files
    │
    └── Bucket

restaurants/123/menu.pdf
    │
    └── Object name
```

## 🌍 Bucket Location

A bucket has a location. Depending on the Cloud Storage configuration, the location can be a region, dual-region, or multi-region.

Location matters because it can affect factors such as:

- Data placement
- Latency
- Availability characteristics
- Data residency requirements
- Cost

For example, an application with users primarily in one geography may consider a suitable regional location, while an application with broader requirements may consider a dual-region or multi-region configuration.

The important idea for now is:

> **Location is a bucket-level concept.**

## ⚙️ Bucket-Level vs Object-Level

Not every Cloud Storage property belongs to an object.

### Bucket-level concepts

Examples include:

- Bucket name
- Bucket location
- Storage configuration
- Lifecycle configuration
- Versioning configuration
- Access configuration

### Object-level concepts

Examples include:

- Object name
- Object data
- Object metadata
- Object generation/version information

Think about it like this:

```text
                    Bucket
                      │
          ┌───────────┴───────────┐
          │                       │
     Bucket config            Objects
                                  │
                         ┌────────┼────────┐
                         ▼        ▼        ▼
                       Obj 1    Obj 2    Obj 3
```

## 🧩 Example: Restaurant Application

Suppose Floci stores restaurant files in:

```text
Bucket:
floci-restaurant-files
```

Objects could be:

```text
restaurants/101/logo.png
restaurants/101/menu.pdf
restaurants/102/logo.png
restaurants/102/menu.pdf
```

The application can use the object name as a logical naming convention.

For example:

```text
restaurants/{restaurant_id}/{file_type}
```

This is an application-level convention. Cloud Storage does not need to understand the restaurant concept itself.

## ⚠️ Important Naming Concept

Bucket names and object names have different roles.

The bucket identifies the storage container, while the object name identifies the stored object within that bucket.

For example:

```text
gs://floci-restaurant-files/restaurants/101/menu.pdf
    └──────────── bucket ────────────┘ └── object ──┘
```

## 🧠 Interview Mental Model

If an interviewer asks:

> **What is the difference between a bucket and an object?**

A concise answer is:

> A bucket is a container in Cloud Storage, while an object is the actual data stored in that bucket. Each object has a name that identifies it within the bucket.

If they ask:

> **Are folders real in Cloud Storage?**

Explain that Cloud Storage is an object store and that `/` commonly appears in object names to provide a folder-like organization.

## ✅ What You Should Remember

1. A bucket is a container for objects.
2. An object is the stored data plus associated metadata.
3. Object names uniquely identify objects within a bucket.
4. `/` in an object name provides folder-like organization but should not be confused with a traditional filesystem.
5. `gs://bucket/object` identifies a Cloud Storage object.
6. Bucket location is a bucket-level concept.
7. Object data and metadata are object-level concepts.
8. Applications can establish their own object-naming conventions.

## 🧪 Checkpoint

Explain this resource without looking at the notes:

```text
gs://floci-restaurant-files/restaurants/123/menu.pdf
```

You should be able to identify:

- The Cloud Storage scheme
- The bucket
- The object name
- Why `restaurants/123/` should not automatically be interpreted as traditional directories
