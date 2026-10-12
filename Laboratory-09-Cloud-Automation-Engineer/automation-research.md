# Automation Research — Language of Automation
**Engineer:** Charlene Padin Lomboy

**Bash Script:**
A Bash script is a plain text file containing a sequence of Linux commands that run top-to-bottom as if I typed them myself. The first line `#!/bin/bash`, called the shebang, tells the system which interpreter should execute the file, so `./backup.sh` knows to use Bash and not sh or Python.

**Variables:**
Programmers use variables like `$BACKUP_DIR` instead of hard-coding `/root/backups` everywhere so the script is reusable and easy to fix. If CloudNova moves the folder tomorrow, I change one line at the top instead of hunting down ten paths, which also prevents typos that break backups.

**Cron Job:**
A cron job is a scheduled task managed by the Linux cron daemon that runs a command automatically at a fixed time pattern. It is essential for cloud operations because servers must patch, back up, and scale at 2 AM without waking up an engineer — automation removes forgetfulness and makes 1,000 servers behave like one.
