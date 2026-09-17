# 5. Cloud Storage Learning Checklist ✅

Use this checklist before moving to **Chapter 4 — Storage in an Application**.

## 🧠 Concepts

- [ ] I can explain what Cloud Storage is.
- [ ] I can explain why object storage is useful.
- [ ] I can explain the difference between a bucket and an object.
- [ ] I can explain what an object name is.
- [ ] I understand why `/` in an object name does not make Cloud Storage a traditional filesystem.
- [ ] I understand the `gs://bucket/object` notation.
- [ ] I know that bucket location is a bucket-level concept.
- [ ] I can distinguish bucket-level concepts from object-level concepts.
- [ ] I understand the difference between Cloud Storage and Persistent Disk.
- [ ] I understand why an application might store file data in Cloud Storage and metadata in a database.

## 🛠️ CLI

- [ ] I can list buckets.
- [ ] I can create a bucket in my lab.
- [ ] I can list objects in a bucket.
- [ ] I can upload a local file.
- [ ] I can download an object.
- [ ] I can delete an object.
- [ ] I can explain the source and destination of a `gcloud storage cp` command.

## 🧪 Hands-On

- [ ] I completed the local file-storage workflow.
- [ ] I uploaded an object using a folder-like object name.
- [ ] I downloaded the object and verified its contents.
- [ ] I deleted the object and verified that it was gone.
- [ ] I completed the challenge without copying the solution commands.

## 🎯 Interview Readiness

I should be able to answer these in my own words:

1. What is Cloud Storage?
2. Why would you use Cloud Storage instead of local application-server storage?
3. What is a bucket?
4. What is an object?
5. What is an object name?
6. Are folders real in Cloud Storage?
7. What does `gs://bucket/object` mean?
8. What is the difference between Cloud Storage and Persistent Disk?
9. What happens when a local file is uploaded to a Cloud Storage bucket?
10. What is the difference between a bucket-level configuration and object-level metadata?

## 🚦 Ready for Chapter 4?

Do not move forward just because the commands worked.

You are ready when you can explain the following without notes:

> **What problem does Cloud Storage solve, how is data organized inside it, how does an application interact with it, and how is it different from storage attached directly to a compute resource?**
