# Laboratory 2: Build the Cloud Infrastructure Blueprint

## Mission Overview
This laboratory activity simulates the planning phase of a cloud deployment for a fictional company, CloudNova Technologies. The goal was to investigate the components of cloud infrastructure — compute, storage, networking, and identity — using a live Linux environment (KillerCoda), and to document the findings as a Cloud Infrastructure Assessment Report before any servers are deployed.

## Objectives
- Explain the major components of cloud infrastructure.
- Investigate the hardware and software resources available in a Linux environment.
- Differentiate compute, storage, networking, and identity resources.
- Interpret the relationship between cloud infrastructure components.
- Create professional technical documentation using Markdown.
- Continue building a structured GitHub Cloud Computing Portfolio.

## Cloud Infrastructure Components
- **Compute:** The CPU, cores, and RAM available on the server (Intel Xeon E312xx, 1 core, 1.9 GiB RAM) — the processing power that runs applications.
- **Storage:** The disk partitions on the server (19GB root volume, plus boot partitions) — where OS files and data persist.
- **Networking:** The hostname and IP addresses assigned to the server — how the machine communicates internally and externally.
- **Operating System:** Ubuntu 24.04.4 LTS running kernel 6.8.0-138-generic — the software layer managing all hardware resources.

Full details are documented in `infrastructure-report.md` and `cloud-components.md`.

## Tools Used
- KillerCoda Playground (Linux terminal environment)
- Linux CLI tools (`uname`, `lscpu`, `free`, `df`, `mount`, `hostname`)
- Draw.io / diagramming tool for the architecture diagram
- GitHub for version control and portfolio documentation
- Markdown for technical documentation

## Linux Commands Executed
- `cat /etc/os-release` — check OS details
- `uname -r` — check kernel version
- `lscpu` — check CPU model and specs
- `nproc` — check number of CPU cores
- `free -h` — check RAM and swap usage
- `df -h` — check disk capacity
- `mount` — check mounted filesystems
- `hostname` — check server hostname
- `hostname -I` — check IP address

## Skills Learned
- How to inspect a Linux server's hardware and software resources from the command line.
- How to map physical/virtual server resources (CPU, RAM, disk, network) to cloud infrastructure concepts (compute, storage, networking).
- How to research and compare equivalent services across AWS, Azure, and GCP.
- How to create clear, professional technical documentation using Markdown.
- How to design a basic cloud architecture diagram showing user, network, compute, and storage relationships.

## Challenges Encountered
- Some Linux commands (like `nproc`, `lscpu`) required looking up flags to get the exact information needed.
- Understanding the distinction between private and public IP addresses on the KillerCoda environment.
- Translating raw command-line output into clear, professional documentation that a non-technical stakeholder could still follow.
