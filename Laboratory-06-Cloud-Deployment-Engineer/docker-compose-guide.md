# Docker Compose Guide — What My YAML Actually Does

*Charlene Padin Lomboy — Lab 06 — Nextcloud + MariaDB stack*

This is my handover note so another engineer (or future me during exams) can understand the file I deployed. The full file is also saved in this folder as `docker-compose.yml`.

## The Compose file I used

```yaml
version: '3'
services:
  database:
    image: mariadb:10.6
    environment:
      - MYSQL_ROOT_PASSWORD=cloudnova_root
      - MYSQL_PASSWORD=cloudnova_pass
      - MYSQL_DATABASE=nextcloud_db
      - MYSQL_USER=nextcloud_user
  app:
    image: nextcloud
    ports:
      - 8080:80
    environment:
      - MYSQL_PASSWORD=cloudnova_pass
      - MYSQL_DATABASE=nextcloud_db
      - MYSQL_USER=nextcloud_user
      - MYSQL_HOST=database
```

I wrote this in KillerCoda with `nano docker-compose.yml`. YAML is space-sensitive so I used 2 spaces per level, no tabs. One wrong indent and Compose refuses to run, which happened to me once before I fixed it.

## What does the `services:` block do?

`services:` is where you list every container that belongs to the stack. Here I declared two:

- `database` — built from `mariadb:10.6`, holds all persistent records. No `ports:` because users should never reach it directly.
- `app` — built from `nextcloud`, with `ports: - 8080:80` so KillerCoda port 8080 forwards to port 80 inside the container where Nextcloud listens.

When I ran `docker-compose up -d`, Compose read this block, pulled both images if missing, created a private network for them, and started both in detached mode. `docker-compose ps` then showed both as Up. Without `services:`, Compose would not know what to create — it is basically the table of contents for my infrastructure.

## How did Nextcloud find the database?

Through `MYSQL_HOST=database`.

Compose gives each service a built-in hostname equal to its service name. So even though I never typed an IP address, the `app` container can resolve `database` to the MariaDB container on their shared network. The other three variables have to match on both sides (`MYSQL_USER`, `MYSQL_PASSWORD`, `MYSQL_DATABASE`) so Nextcloud logs in with the same user and password that MariaDB created.

That is why spelling matters. If I typed `MYSQL_HOST=databse` or used a different password in `app`, Nextcloud would just keep spinning on the setup page and fail to connect. Matching credentials + service-name hostname is the whole trick.

## `docker run` vs `docker-compose up -d`

In Mission 4 I used `docker run -d -p 8080:80 --name my-nginx nginx` — one container, one long command I had to remember and retype perfectly every time.

`docker-compose up -d` is different: it reads the YAML file and builds the *entire system* at once. I do not retype ports and passwords; they live in the file. I can redeploy on another machine by copying one file and running one command. And `docker-compose down` stops and removes everything from that file together, while with `docker run` I had to `stop` and `rm` each container manually.

That is the IaC idea our instructor keeps repeating: junior engineers type commands, senior engineers write files. My YAML is now the deployment — reviewable, repeatable, and easy to share with the university IT team.
