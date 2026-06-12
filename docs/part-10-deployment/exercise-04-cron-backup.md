---
title: "10.4 Automated Backups"
parent: Deployment
nav_order: 4
---

# Exercise 10.4 — Automated Backups

## The Story

`library.db` holds every book record, every member, every loan in the system. It lives on the Pi's SD card. SD cards fail — especially under frequent read/write load. When this one fails, every record is gone.

The answer is backups. But backups only help if they run reliably, every day, without anyone having to remember to do them. A backup that depends on a person remembering is not a backup strategy — it is a hope.

*Cron* is the Linux tool for scheduled, automatic tasks. You will use it to run a backup script every night.

## What to Do

### Step 1 — Write the backup script

Create `/home/pi/scripts/backup_library.sh`:

This script should:
1. Create a `backups/` folder if it does not exist
2. Copy `library.db` to `backups/library-YYYY-MM-DD.db` (today's date in the filename)
3. Delete any backup files older than 30 days (to avoid filling the disk)
4. Log one line to a logfile: the date, time, and whether the backup succeeded or failed

Test it manually:
```
bash /home/pi/scripts/backup_library.sh
```

Verify the backup file was created and the log has an entry.

### Step 2 — Schedule it with cron

Open the cron editor:
```
crontab -e
```

Add a line to run the backup script every night at 2am:
```
0 2 * * * /home/pi/scripts/backup_library.sh
```

The five fields mean: minute, hour, day of month, month, day of week. `0 2 * * *` means: minute 0, hour 2, every day, every month, every day of week.

### Step 3 — Test the schedule (without waiting until 2am)

Change the cron entry temporarily to run one minute from now. Wait for it to trigger. Check the backup folder and the log. Then restore the `0 2 * * *` schedule.

### Step 4 — Verify the backup is usable

Restore the backup to a test location and open it with DB Browser. Verify the tables and data are intact. A backup that cannot be restored is worthless.

## Topics You Will Learn

- Cron syntax and the crontab file
- Shell scripting basics: variables, file operations, date formatting, exit codes
- `find -mtime +30 -delete` — deleting old files automatically
- The difference between a backup and an archive
- The principle: test your restore process, not just your backup process

## Before You Start — Think About This

1. If the backup script fails silently (no output, no error), you might not discover the problem until after a failure when you need the backup. How does writing to a log file help?
2. Backups on the same device as the data are not real backups. If the SD card fails, the backups fail too. What would a better backup strategy look like?
3. The cron schedule `0 2 * * *` runs at 2am local time. What is "local time" on the Pi? How do you check and set the Pi's timezone?

## When You're Stuck

- `date +%Y-%m-%d` in a shell script returns the current date as `2026-06-12`. Use this in the filename.
- `cp library.db backups/library-$(date +%Y-%m-%d).db` copies the file with a date-stamped name.
- If cron does not seem to run, check the cron log: `grep CRON /var/log/syslog`
- Make the script executable: `chmod +x /home/pi/scripts/backup_library.sh`

## Once It Works — Go Further

1. Modify the backup script to also copy the backup to a second location — a USB drive mounted at `/mnt/usb/`. This is a simple version of the "3-2-1 backup rule": 3 copies of data, 2 different media, 1 off-site. Look up the full rule.
2. Add email notification when the backup fails. Look up `msmtp` for sending email from the command line on Raspberry Pi.
