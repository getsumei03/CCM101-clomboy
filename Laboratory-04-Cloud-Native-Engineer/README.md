# Lab 04 — Cloud-Native Engineer

*Charlene Padin Lomboy — BSIT — CCM101 Cloud Computing*
*Mission 4 for CloudNova Technologies*

## Mission Overview

Our client says VMs boot too slowly and eat too much RAM for simple web hosting. As the Cloud-Native trainee on this ticket, my job was to compare VMs against containers in plain language, then prove the difference live: boot a real Nginx web server with Docker on KillerCoda Ubuntu and hand over commands the IT team can rerun. This folder is that proof — research, terminal log, screenshots, and what I learned.

## Objectives

- Explain VM vs container architecture without jargon
- Get comfortable in a KillerCoda Ubuntu playground with Docker
- Practice core Docker CLI: pull, run, ps, stop, rm, curl check
- Expose a container port correctly (`8080 -> 80`) and verify with curl
- Write clean Markdown docs with evidence
- Keep my CCM101 portfolio tidy and committable per checkpoint

## Docker Commands Executed

Environment: KillerCoda `Playground-ubuntu` (Ubuntu 24.04, Docker 29.x).

**Checkpoint 3 — health check:**
```bash
docker --version
docker info
docker ps
```

**Checkpoint 4 — ship Nginx as `nginx-lab04`:**
```bash
docker pull nginx
docker run -d -p 8080:80 --name nginx-lab04 nginx
docker images | grep nginx
curl -s http://localhost:8080 | head -20
```

**Checkpoint 5 — teardown:**
```bash
docker ps
docker stop nginx-lab04
docker ps
docker ps -a
docker rm nginx-lab04
docker ps -a
```

Evidence mapping:
- `screenshots/docker-version.png` — version + info + empty ps
- `screenshots/nginx-running.png` — run output + curl Welcome page
- `screenshots/container-lifecycle.png` — ps / stop / rm sequence

Full narration in `docker-deployment.md`, theory in `virtualization-vs-containers.md`.

## Skills Learned

- Reading `docker info` output (storage driver overlay2, cgroup driver, CPUs/RAM) instead of just blindly typing
- Difference between image (`pull`) and live process (`run -d`), and why `-d` matters for servers
- Port publishing logic: container's private 80 must be published to host 8080 to be reachable
- Lifecycle discipline: always `ps` before `stop`, `ps -a` before `rm`, final `ps -a` to prove clean
- Naming containers (`--name nginx-lab04`) to avoid random names and ID copy-paste errors
- Markdown handover writing: code fences, tables, screenshot links, troubleshooting tips

## Challenges Encountered

- **Playground timer:** KillerCoda kills idle sessions after a while, so I learned to run pull/run/curl back-to-back and screenshot immediately.
- **Name collision:** First `run` failed once with name in use from an earlier attempt; fixed with `docker rm -f nginx-lab04` and reran.
- **Port confusion:** At first I curled port 80 instead of 8080 and got connection refused; re-reading `-p 8080:80` as host:container fixed my mental model.
- **Screenshot size:** Full `docker info` is long, so I scrolled to include version + server section in one capture for readability.
- **Upload naming:** GitHub web is case-sensitive, so I double-checked exact lowercase names `docker-version.png`, `nginx-running.png`, `container-lifecycle.png`.

## Layout

```
Laboratory-04-Cloud-Native-Engineer/
├── README.md
├── virtualization-vs-containers.md
├── docker-deployment.md
├── reflection.md
└── screenshots/
    ├── docker-version.png
    ├── nginx-running.png
    └── container-lifecycle.png
```
