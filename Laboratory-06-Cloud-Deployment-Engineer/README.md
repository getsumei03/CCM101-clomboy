# Lab 06 — Cloud Deployment Engineer

*Charlene Padin Lomboy — BSIT — CCM101 Cloud Computing*
*Mission 6 for CloudNova Technologies — Nextcloud + MariaDB with Docker Compose*

## Mission Overview

Our new client is a university that is tired of paying for Google Drive and wants its own private cloud. They picked Nextcloud, but Nextcloud alone is not enough — it needs a database to remember users and file info. So instead of running one container at a time like in Mission 4 and 5, I deployed two linked containers at once: Nextcloud for the website and MariaDB for the data.

I did it the senior-engineer way, with Infrastructure as Code. I wrote one `docker-compose.yml` file in `nano`, ran a single command, and both containers came up together. This folder has my architecture notes, the Compose file breakdown, screenshots, and what I learned about YAML (mostly that spaces matter way too much).

## Objectives

- Explain two-tier architecture in a way our university client would actually understand
- Read and write a `docker-compose.yml` file without breaking the indentation
- Use `nano` in the KillerCoda terminal to create config files from scratch
- Deploy Nextcloud + MariaDB together with `docker-compose up -d`
- Open the Nextcloud setup page through KillerCoda port forwarding (8080)
- Shut everything down cleanly with `docker-compose down`
- Document IaC steps in Markdown with screenshot proof
- Keep adding to my CCM101 portfolio in order

## Commands Executed

All in KillerCoda Ubuntu Playground, inside `~/nextcloud-deployment`:

```bash
mkdir nextcloud-deployment
cd nextcloud-deployment
nano docker-compose.yml
# pasted the YAML, Ctrl+O, Enter, Ctrl+X to save and exit

docker-compose up -d
docker-compose ps
docker ps
```

Opened Nextcloud in browser:
```
KillerCoda Ports tab -> type 8080 -> Access
# Nextcloud setup screen shows up, asks for admin account
# I stopped there as instructed, no need to finish setup
```

Teardown:
```bash
docker-compose down
docker ps -a
```

Full YAML I used is saved here as `docker-compose.yml` and explained in `docker-compose-guide.md`.

Evidence:
- `screenshots/compose-deployment.png` — terminal after `up -d` + `ps` showing both containers
- `screenshots/nextcloud-web.png` — browser on port 8080 with Nextcloud setup page
- `screenshots/compose-teardown.png` — terminal after `down`, containers stopped/removed

## Skills Learned

- Setting up a real two-tier stack: app tier (Nextcloud, port 8080->80) talking to DB tier (MariaDB 10.6)
- Writing YAML that actually works: 2-space indents, no tabs, `services:`, `image:`, `ports:`, `environment:`
- Using `nano` without panicking — save is Ctrl+O, exit is Ctrl+X, I finally remembered
- How Compose creates its own network so `MYSQL_HOST=database` just works as a hostname
- Passing DB credentials with environment variables instead of hardcoding them inside images
- Difference between `docker run` (one container, long command) vs `docker-compose up -d` (whole stack from file)
- Verifying with `docker-compose ps` and cleaning up with `docker-compose down` so KillerCoda doesn't stay messy
- Documenting IaC so a classmate can copy my file and get the same result

## Layout

```
Laboratory-06-Cloud-Deployment-Engineer/
├── README.md
├── multi-tier-architecture.md
├── docker-compose-guide.md
├── docker-compose.yml
├── reflection.md
└── screenshots/
    ├── compose-deployment.png
    ├── nextcloud-web.png
    └── compose-teardown.png
```
