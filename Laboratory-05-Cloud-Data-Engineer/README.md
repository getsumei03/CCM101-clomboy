# Lab 05 — Cloud Data Engineer

*Charlene Padin Lomboy — BSIT — CCM101 Cloud Computing*
*Mission 5 for CloudNova Technologies — MinIO Object Storage PoC*

## Mission Overview

Our photo-sharing client needs room for millions of uploads but can't keep files inside web containers because containers are ephemeral — `docker rm` wipes them. As the Data Engineering trainee, I proved an S3-compatible alternative: deploy MinIO with Docker on KillerCoda, expose its console, create a `client-photos` bucket, and upload a test object. This folder holds the theory, the exact commands, screenshots, and lessons so IT can repeat it for production S3 later.

## Objectives

- Contrast Block vs File vs Object storage with real cloud examples
- Deploy MinIO (`minio/minio`) with Docker env vars and dual port mapping
- Reach a containerized web UI through KillerCoda port forwarding (9001)
- Create bucket `client-photos` and upload a file via browser
- Document storage ops in Markdown with evidence
- Keep the CCM101 portfolio structured and committable

## Tools Used

- KillerCoda `Playground-ubuntu` (Ubuntu 24.04 + Docker)
- Docker image `minio/minio` (S3-compatible storage)
- MinIO Web Console on port `9001` (API on `9000`)
- Bucket: `client-photos`
- Credentials: `cloudadmin` / `CloudNova2026!` (lab PoC only, rotate in prod!)
- Markdown + GitHub for docs and screenshots

Key commands:
```bash
docker run -d -p 9000:9000 -p 9001:9001 --name minio-server -e "MINIO_ROOT_USER=cloudadmin" -e "MINIO_ROOT_PASSWORD=CloudNova2026!" minio/minio server /data --console-address ":9001"
docker ps
docker logs minio-server --tail 20
```

Evidence:
- `screenshots/minio-deployed.png` — terminal + running container
- `screenshots/minio-bucket-upload.png` — console with bucket + file
- Details: `storage-types-research.md`, `minio-deployment.md`

## Skills Learned

- Reading storage trade-offs: why EBS for DBs, EFS for shares, S3/MinIO for billions of images
- Running stateful services in Docker: `-d`, double `-p`, `--name`, `-e` for secrets, trailing `server /data` args
- Separating API (9000, XML/S3) from Console (9001, clickable UI)
- KillerCoda port-forward flow: Ports tab → 9001 → Access → login
- Bucket hygiene: flat namespace, unique keys, upload-verify via UI listing
- Treating object stores as permanent vs containers as disposable — the core data-engineer mindset
- Writing handover-grade Markdown: exact commands, ports, bucket names, gotchas

## Challenges Encountered (bonus notes)

- **Backslash paste:** multi-line `\` command broke when pasted; fixed by using the single-line version above.
- **Wrong port:** opened 9000 first and saw raw XML — learned UI lives only on 9001.
- **Slow pull:** `minio/minio` took a minute on first pull; waited instead of Ctrl-C, then `docker ps` confirmed Up.
- **Upload source:** playground has no photos, so uploaded from my laptop via the browser Upload button as instructed.

## Layout

```
Laboratory-05-Cloud-Data-Engineer/
├── README.md
├── storage-types-research.md
├── minio-deployment.md
├── reflection.md
└── screenshots/
    ├── minio-deployed.png
    └── minio-bucket-upload.png
```
