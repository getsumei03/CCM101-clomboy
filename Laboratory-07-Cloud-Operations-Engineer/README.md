# Laboratory 07 – Cloud Operations Engineer

*Charlene Lomboy (getsumei03) – CCM-101 Cloud Computing*
*Mission 7: The Cloud Operations Engineer – CloudNova Technologies*

## Mission Overview

Deploying is only step one — keeping it running is the real job. As a Cloud Operations Engineer (Site Reliability Engineering), I performed a baseline health check for a client's website ahead of a massive marketing surge. I checked the Linux host's RAM, disk, and CPU load, deployed an Nginx container named `client-website` on port 8080, generated test traffic with `curl` (including an intentional 404), then proved health with `docker logs` and `docker stats`.

> A developer hopes the application works; a Site Reliability Engineer uses metrics and logs to prove it.

## Objectives

- Utilize native Linux command-line tools to monitor host CPU, Memory, and Disk capacity
- Deploy a web container and track its real-time performance using Docker metrics
- Generate web traffic and extract application access logs for analysis
- Translate raw performance data into a readable technical report using Markdown
- Continue expanding a professional GitHub Cloud Computing Portfolio

## Monitoring Commands Executed

```bash
# Checkpoint 2 - Host baseline
free -h
df -h
top
# wait 5 sec, press q to exit

# Checkpoint 3 - Deploy + generate traffic
docker run -d -p 8080:80 --name client-website nginx
curl http://localhost:8080
curl http://localhost:8080
curl http://localhost:8080
curl http://localhost:8080/hidden-admin-page

# Checkpoint 4 - Application logs
docker logs client-website

# Checkpoint 5 - Real-time metrics
docker stats
# or one-shot: docker stats --no-stream
# q / Ctrl+C to exit live view
```

## Skills Learned

- Reading `free -h` for total/used/free RAM and `df -h` for root `/` capacity
- Using `top` to spot CPU-hungry processes before a traffic surge
- Running Nginx detached with `-d -p 8080:80 --name client-website`
- Simulating users with `curl` and intentionally triggering a 404 for log evidence
- Grepping `docker logs` for `200` vs `404` to troubleshoot user reports
- Distinguishing logs (what happened) from metrics (how much resource now)
- Understanding why enterprises scale this with Prometheus + Grafana instead of manual `docker stats`
- Writing baseline + observability reports another engineer can reproduce

## Repository Structure

```text
Laboratory-07-Cloud-Operations-Engineer/
├── README.md
├── system-baseline-report.md
├── container-observability.md
├── reflection.md
└── screenshots/
    ├── memory-check.png
    ├── disk-check.png
    ├── install-nginx.png
    ├── simulation1.png
    ├── simulation2.png
    ├── docker-logs.png
    └── container-metrics.png
```

## Screenshot Evidence

- `memory-check.png` – `free -h` output
- `disk-check.png` – `df -h` output
- `install-nginx.png` – `docker run -d -p 8080:80 --name client-website nginx` + `docker ps`
- `simulation1.png` – three `curl http://localhost:8080` returning Nginx welcome HTML
- `simulation2.png` – `curl http://localhost:8080/hidden-admin-page` returning 404
- `docker-logs.png` – `docker logs client-website` showing three 200s + one 404
- `container-metrics.png` – `docker stats` showing CPU %, MEM USAGE, NET I/O for `client-website`

> Replace placeholder values in the two report files with YOUR KillerCoda numbers before final push.

## Quick Reproduce

```bash
free -h; df -h; top
docker run -d -p 8080:80 --name client-website nginx
curl http://localhost:8080; curl http://localhost:8080; curl http://localhost:8080
curl http://localhost:8080/hidden-admin-page
docker logs client-website
docker stats --no-stream
docker stop client-website; docker rm client-website
```

## Author

Charlene Lomboy – GitHub: [@getsumei03](https://github.com/getsumei03/CCM101-clomboy)
