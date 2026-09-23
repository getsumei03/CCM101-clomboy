# MinIO Deployment Log — S3-Compatible Storage on Docker

*Charlene Padin Lomboy — CCM101 Lab 05 — KillerCoda Ubuntu Playground*

This is the exact runbook I used so the client's IT team can rebuild the same proof-of-concept.

## Exact Docker command (Checkpoint 3)

Single-line version for KillerCoda (no backslash issues):

```bash
docker run -d -p 9000:9000 -p 9001:9001 --name minio-server -e "MINIO_ROOT_USER=cloudadmin" -e "MINIO_ROOT_PASSWORD=CloudNova2026!" minio/minio server /data --console-address ":9001"
```

> Lab-day note (Sep 2026): Docker Hub mirror stalled on `minio/minio:latest`, but `quay.io/minio/minio:latest` pulled fine, so I deployed with the official Quay mirror below — identical MinIO build, visible in my screenshots:
```bash
docker pull quay.io/minio/minio:latest
docker run -d -p 9000:9000 -p 9001:9001 --name minio-server -e "MINIO_ROOT_USER=cloudadmin" -e "MINIO_ROOT_PASSWORD=CloudNova2026!" quay.io/minio/minio server /data --console-address ":9001"
```

Multi-line version from the lab sheet:

```bash
docker run -d -p 9000:9000 -p 9001:9001 --name minio-server \
  -e "MINIO_ROOT_USER=cloudadmin" \
  -e "MINIO_ROOT_PASSWORD=CloudNova2026!" \
  minio/minio server /data --console-address ":9001"
```

Verify it lives:

```bash
docker ps
docker logs minio-server --tail 20
```

You should see `API: http://0.0.0.0:9000` and `WebUI: http://0.0.0.0:9001` in logs, plus `minio-server Up` in `ps`.

Screenshot: `screenshots/minio-deployed.png`

## Web console access (Checkpoint 4)

- **Port for web console: 9001** (API is 9000, console is 9001 — don't mix them).
- In KillerCoda open the **Traffic / Ports / Custom Ports** tab, type `9001`, click **Access**.
- Login: user `cloudadmin` / password `CloudNova2026!` (from the `-e` flags below).
- Left menu → **Buckets** → **Create Bucket** → name `client-photos` → Save.
- Open `client-photos` → **Upload** → pick any small `.png`/`.txt` from your laptop → confirm it appears in the object list.

Screenshot: `screenshots/minio-bucket-upload.png` — must clearly show bucket name `client-photos` + uploaded file.

## Summary for handover

- **Deploy command:** see block above (`minio/minio server /data --console-address ":9001"`).
- **Console port:** `9001` via KillerCoda Ports tab.
- **Bucket created:** `client-photos`.
- **What `-e` flags did:** `-e` sets environment variables inside the container. Here they seed MinIO's admin account (`MINIO_ROOT_USER` + `MINIO_ROOT_PASSWORD`) so the server boots with known login instead of random defaults. Without them you couldn't log into the console.

> Gotcha I hit: curling port 9000 returns XML (that's the S3 API, normal). The pretty UI is only on 9001. If 9001 shows blank, wait 10s for MinIO to finish init and refresh.
