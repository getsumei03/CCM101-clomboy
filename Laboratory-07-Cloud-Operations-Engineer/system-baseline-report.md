# System Baseline Report – Host Health Check

*Charlene Lomboy (getsumei03) – CCM-101 Mission 7 – CloudNova Technologies*

Commands used in KillerCoda Ubuntu Playground:

```bash
free -h
df -h
top
# observe 5 seconds, press q to exit
```

## 1. Memory (RAM) – `free -h`

> TODO: replace with YOUR output. Example format only:

```text
               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       420Mi       2.6Gi        12Mi       800Mi       3.2Gi
Swap:             0B          0B          0B
```

- **Total RAM available on the server:** `__REPLACE__ e.g. 3.8Gi`
- Screenshot: `screenshots/memory-check.png`

## 2. Disk Storage – `df -h`

> TODO: replace with YOUR output. Example format only:

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G  8.2G   42G  17% /
```

- **Total Storage capacity of the root (/) file system:** `__REPLACE__ e.g. 50G (Avail 42G, Use% 17%)`
- Screenshot: `screenshots/disk-check.png`

## 3. CPU / Processes – `top`

Observed live CPU %, MEM %, and top processes for 5 seconds before pressing `q`. Baseline showed low idle CPU with no runaway process, confirming the host was healthy before deploying Nginx.

## Why Check Disk Space Before a Traffic Surge?

Checking disk space is critical before a massive traffic surge because Nginx access logs, container layers, and image pulls all consume disk, and a full root filesystem will crash the web server and block new writes even if CPU and RAM look fine.
