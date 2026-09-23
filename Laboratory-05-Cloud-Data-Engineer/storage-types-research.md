# Types of Cloud Storage — Research

*Charlene Padin Lomboy — CCM101 Lab 05 — For CloudNova photo-app client*

## Comparison Table

| Storage Type | Description (How does it store data?) | Primary Use Case (Best for?) | Cloud Provider Example |
|---|---|---|---|
| **Block Storage** | Splits data into fixed-size blocks with unique addresses, like a raw hard drive. No file structure — OS formats it. Low-latency, high-performance volumes attached to one VM at a time. | Databases, boot disks, high-IOPS apps (MySQL, VM system drives) where speed and random read/write matter. | AWS EBS, Azure Managed Disks, Google Persistent Disk |
| **File Storage** | Keeps a shared hierarchical tree of folders and files accessed over the network (NFS/SMB). Many clients can mount the same share at once. | Shared team drives, CMS content, dev workspaces, lift-and-shift apps that expect a normal folder path. | AWS EFS, Azure Files, Google Filestore |
| **Object Storage** | Stores each file as an object (data + metadata + unique key) inside flat buckets over HTTP/S3 API. No folders, virtually unlimited scale, built-in replication. | Images, videos, backups, static web assets — millions of unstructured files accessed via URL/API. | AWS S3, Google Cloud Storage, Azure Blob Storage, self-hosted MinIO |

## Why Object Storage for User Photos?

For millions of user-uploaded images, object storage is the clear winner because each photo becomes one cheap, URL-addressable object that scales without reformatting drives or managing folder hierarchies. Unlike block volumes tied to one server, buckets grow infinitely, replicate automatically, and serve directly to the app via S3 API. That is why our proof-of-concept uses MinIO with a `client-photos` bucket.

*Hands-on proof: `minio-deployment.md` + `screenshots/minio-deployed.png`, `minio-bucket-upload.png`.*
