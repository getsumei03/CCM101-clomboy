# Mission Reflection – The Cloud Operations Engineer

*Charlene Lomboy (getsumei03) – CCM-101 Mission 7*

Checking host resources matters even when containers look perfect because containers share the host kernel, RAM, disk, and CPU. A `client-website` container can report Up while the host is nearly out of disk for logs or out of memory for new connections, and the next traffic spike will then crash everything at once. Baseline `free -h`, `df -h`, and `top` give me headroom proof before the marketing campaign, not after an outage.

If a user cannot log in, `docker logs` lets me stop guessing and read evidence. I run `docker logs client-website` and filter for their IP, path, and status code to see whether they hit 200, 401, 404, or 500, and at what timestamp. That single timeline tells me if the fault is a wrong URL, failed auth, or server error, so I can reproduce and fix the exact request instead of restarting blindly.

Logs and metrics answer different questions. Logs from Checkpoint 4 are discrete event history showing what happened and when, such as three 200s and one 404 with paths and user-agents. Metrics from Checkpoint 5 are live resource quantities showing how heavy the container is right now, such as CPU %, memory usage, and network I/O. I need logs to debug behavior and metrics to judge capacity and scaling.

Large enterprises cannot watch thousands of containers with manual `docker stats`. They run agents that scrape metrics into Prometheus for time-series storage and alerting, then visualize in Grafana dashboards with per-service CPU, memory, error-rate, and latency panels. Logs are shipped centrally to stacks like ELK or Loki for search, so one query finds all 404s or 500s across the fleet and triggers auto-scale or on-call before users notice.

My Linux troubleshooting improved from memorizing commands to reading systems. I now start with a baseline, deploy, generate traffic with `curl`, verify with logs, and confirm with stats, then document values in Markdown with screenshots. That observe-hypothesize-verify loop makes outages feel diagnosable instead of mysterious. (310 words)
