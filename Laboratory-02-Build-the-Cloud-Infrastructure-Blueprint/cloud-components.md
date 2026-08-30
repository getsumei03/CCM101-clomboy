# Cloud Infrastructure Components

## Compute Resources
**Purpose:** Compute resources provide the processing power needed to run applications, execute code, and handle workloads. This includes the CPU, cores, and memory allocated to a system.

**Why important in cloud computing:** Compute is the foundation of any cloud service — without it, no application, website, or workload can run. Cloud providers let users provision and scale compute power on demand instead of buying physical hardware.

**Relation to the KillerCoda environment:** The KillerCoda Ubuntu server has an Intel Xeon E312xx (Sandy Bridge) CPU with 1 core and 1.9 GiB of RAM. This mirrors how a real cloud compute instance (like an AWS EC2 t2.micro) is provisioned with a fixed, limited amount of CPU and memory for a specific task.

## Storage Resources
**Purpose:** Storage resources hold data — operating system files, application data, logs, and user files — persistently on disk.

**Why important in cloud computing:** Applications need reliable, scalable storage that persists independently of compute instances, and cloud storage allows data to be resized, backed up, and accessed without managing physical disks.

**Relation to the KillerCoda environment:** The server has a 19GB root partition (`/dev/vda1`) with 13GB available, plus separate boot partitions (`/dev/vda16`, `/dev/vda15`). This reflects how cloud VMs typically separate the OS/boot volume from data volumes, similar to how AWS separates EBS root and data volumes.

## Networking Resources
**Purpose:** Networking resources allow systems to communicate with each other and with the internet — this includes IP addresses, hostnames, and virtual network interfaces.

**Why important in cloud computing:** Cloud services must be reachable and able to communicate securely between instances, users, and other services; networking is what connects isolated compute and storage resources into a working system.

**Relation to the KillerCoda environment:** The server has a hostname (`ubuntu`) and two IP addresses — `172.30.1.2` (the container's internal network) and `172.17.0.1` (a Docker bridge interface). This is similar to how cloud VMs get both a private IP for internal communication and can be assigned a public IP for external access.

## Operating System
**Purpose:** The operating system manages hardware resources and provides the environment in which applications run — handling processes, memory, file systems, and user permissions.

**Why important in cloud computing:** The OS is the layer that lets cloud providers offer standardized, reproducible environments; it determines compatibility, security patches, and available tools for whatever workload is deployed.

**Relation to the KillerCoda environment:** The server runs Ubuntu 24.04.4 LTS on kernel 6.8.0-138-generic — a common choice for cloud instances because Ubuntu LTS releases are stable, well-supported, and widely used across AWS, Azure, and GCP compute offerings.
