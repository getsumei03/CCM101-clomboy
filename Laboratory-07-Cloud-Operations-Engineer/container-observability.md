# Container Observability – Logs and Metrics

*Charlene Lomboy (getsumei03) – CCM-101 Mission 7*

Deployment and traffic generation:

```bash
docker run -d -p 8080:80 --name client-website nginx
curl http://localhost:8080
curl http://localhost:8080
curl http://localhost:8080
curl http://localhost:8080/hidden-admin-page
docker logs client-website
docker stats
```

Screenshots: `install-nginx.png`, `simulation1.png`, `simulation2.png`, `docker-logs.png`, `container-metrics.png`

## 1. Application Logs – `docker logs client-website`

> TODO: paste YOUR real 404 line. Example shape (IP/date will differ):

```text
172.17.0.1 - - [12/Oct/2026:09:00:00 +0000] "GET /hidden-admin-page HTTP/1.1" 404 153 "-" "curl/7.81.0" "-"
```

The three prior lines in the same output show `"GET / HTTP/1.1" 200`, proving three successful visits, while this line proves the single failed visit to the missing page.

Why application logs are vital for troubleshooting: logs are the timestamped proof of exactly what users requested and what status the server returned, so a 404 vs 200 tells me whether the fault is a bad link or a down server. Without them I would be guessing, but with them I can filter by IP, path, and code and fix the exact broken route.

## 2. Real-Time Container Metrics – `docker stats`

> TODO: replace with YOUR values from the screenshot:

- **Container:** `client-website`
- **CPU %:** `__REPLACE__ e.g. 0.05%`
- **Memory Usage / Limit:** `__REPLACE__ e.g. 3.52MiB / 3.8GiB`
- **Memory %:** `__REPLACE__ e.g. 0.09%`
- **Net I/O:** `__REPLACE__ e.g. 25.1kB / 18.4kB`
- Screenshot: `screenshots/container-metrics.png`

These numbers prove the Nginx container is idle-healthy: near-zero CPU and only a few MiB of RAM, leaving headroom for the marketing surge. If CPU stayed high or memory climbed on every `curl`, that would signal a leak or undersized host before launch.
