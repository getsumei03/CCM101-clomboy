# Mission 9: The Cloud Automation Engineer — CloudNova Technologies

**Author:** Charlene Padin Lomboy (@getsumei03)
**Course:** CCM101 – Cloud Computing | UEP College of Information Technology
**Environment:** KillerCoda Ubuntu Playground + Bash + Cron
**Date:** October 2026

## Mission Overview
CloudNova's client kept losing customer files because backups depended on humans remembering to do them every Friday. Promoted to the Automation and DevOps Team, I eliminated the human element: built `app-data/` dummy data, wrote `backup.sh` to auto-compress it with timestamped tarballs, made it executable, and scheduled it for 2:00 AM daily via Cron.

> If you have to do a task more than twice in the cloud, you should automate it.

## Objectives
- Understand Bash syntax, variables, and shebang
- Write and save executable scripts with nano
- Use chmod to manage Linux permissions
- Schedule autonomous tasks with crontab
- Document code and schedules in Markdown
- Complete the 9-lab Cloud Computing Portfolio

## Commands Executed
```bash
mkdir app-data
echo "This is critical client data." > app-data/data.txt
nano backup.sh
./backup.sh
chmod +x backup.sh
./backup.sh
ls -l backups/
crontab -l
env EDITOR=nano crontab -e
# added: 0 2 * * * /root/backup.sh
crontab -l
```

## Skills Learned
- Bash scripting with variables and timestamps
- Permission model: why scripts need +x
- Cron five-field timing and unattended operations
- Testing automation and verifying .tar.gz output
- Final portfolio polish from Lab 1 to Lab 9
