# Backup Script Guide for Client IT Team

## 1. Full backup.sh Code
```bash
#!/bin/bash
# Automated Backup Script for CloudNova Technologies
SOURCE_DIR="app-data"
BACKUP_DIR="backups"
TIMESTAMP=$(date +"%Y%m%d_%H%M%S")
echo "Initiating automated backup..."
mkdir -p $BACKUP_DIR
tar -czf $BACKUP_DIR/backup_$TIMESTAMP.tar.gz $SOURCE_DIR
echo "Backup completed successfully at $TIMESTAMP!"
```
How it works: sets source/destination variables, generates a unique timestamp, creates `backups/` if missing, then tars `app-data/` into `backup_YYYYMMDD_HHMMSS.tar.gz`.

## 2. What chmod +x Did
`chmod +x backup.sh` added the executable bit to the file permissions, changing it from a readable text file to a runnable program. Before this Linux blocked `./backup.sh` with Permission denied; after this the kernel is allowed to launch it via the shebang.

## 3. Cron Schedule Breakdown
```
0 2 * * * /root/backup.sh
```
| Field | Value | Meaning |
|-------|-------|---------|
| Minute | 0 | at minute 0 |
| Hour | 2 | at 2 AM |
| Day of Month | * | every day |
| Month | * | every month |
| Day of Week | * | every weekday |
| Command | /root/backup.sh | absolute path to script |

Result: runs every single night at exactly 02:00 without human clicks. Verified with `crontab -l`.
