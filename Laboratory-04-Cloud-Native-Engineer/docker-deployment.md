# Docker Hands-On Log — Nginx on KillerCoda

*Charlene Padin Lomboy — CCM101 Lab 04 — Ubuntu Playground (Docker 29.x)*

This log shows exactly what I typed so the client's IT staff can repeat it. I used a fresh container name `nginx-lab04` so it won't clash with other demos.

## 1. Confirm Docker is alive (Checkpoint 3)

```bash
docker --version
# Prints client + server version; proves the Docker binaries are installed.

docker info
# Prints daemon details — storage driver, CPUs, RAM, running containers; proves the daemon is responding.

docker ps
# Lists live containers; empty table on a fresh playground is expected and means ready to deploy.
```

Screenshot: `screenshots/docker-version.png`

## 2. Ship Nginx in seconds (Checkpoint 4)

```bash
docker pull nginx
```
Fetches the official `nginx:latest` image from Docker Hub into local storage without starting anything.

```bash
docker run -d -p 8080:80 --name nginx-lab04 nginx
```
Launches Nginx detached (`-d`), publishes host `8080` to container `80`, and tags it `nginx-lab04` for easy stop/remove.

```bash
docker images | grep nginx
# Optional sanity check that the image is cached locally.

curl -s http://localhost:8080 | head -20
```
Requests the site through the mapped port; seeing `<h1>Welcome to nginx!</h1>` proves port mapping works and the service is up.

Screenshot: `screenshots/nginx-running.png`

## 3. Lifecycle — start to cleanup (Checkpoint 5)

| Order | Command I ran | One-line meaning |
|---|---|---|
| 1 | `docker ps` | Showed `nginx-lab04` as Up with `0.0.0.0:8080->80/tcp`, confirming the web server was still serving. |
| 2 | `docker stop nginx-lab04` | Sent SIGTERM then SIGKILL to freeze the web process but left the container on disk. |
| 3 | `docker ps` | Returned an empty list, proving nothing is running anymore. |
| 4 | `docker ps -a` | Showed `nginx-lab04` as `Exited (0)`, proving it stopped cleanly and is awaiting removal. |
| 5 | `docker rm nginx-lab04` | Erased the stopped container and its writable layer to reclaim space. |
| 6 | `docker ps -a` | Returned empty again, proving full cleanup with no leftovers. |

Copy-paste block for IT handover:
```bash
docker ps
docker stop nginx-lab04
docker ps
docker ps -a
docker rm nginx-lab04
docker ps -a
```

Screenshot: `screenshots/container-lifecycle.png`

> Tip I hit: if `docker run` says `name is already in use`, run `docker rm -f nginx-lab04` first or pick another `--name`.
