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

### Part A — Write the backup script

Write a shell script called `backup_library.sh`. It should:
- Create a `backups/` folder if one does not already exist
- Copy `library.db` to the backups folder with today's date in the filename (so each backup is uniquely named and you can see when it was made)
- Delete backup files older than 30 days so the disk does not fill up over time
- Write one line to a log file: the date, time, and whether the backup succeeded or failed

Test the script by running it manually. Verify the backup file exists and the log file has an entry. Run it a second time and verify it does not delete the first backup (it is not yet 30 days old).

### Part B — Learn cron syntax

Cron schedules are written as five fields: minute, hour, day-of-month, month, day-of-week. A `*` means "every." Look up the format and write out in plain English what each of these means before using them:

- What does `0 2 * * *` mean?
- What does `30 8 * * 1` mean?
- What does `*/15 * * * *` mean?

### Part C — Schedule the backup

Open the cron editor and add an entry to run the backup script every night at 2am. Then test it without waiting until 2am: change the schedule to run one minute from now, wait for it to trigger, check the backup folder and the log file, then restore the 2am schedule.

### Part D — Verify the backup is actually usable

Copy the backup file to your laptop. Open it in DB Browser. Verify the tables and data are intact.

A backup that cannot be restored is not a backup — it is a false sense of security. Write down the exact steps needed to restore the library from the most recent backup, so the librarian could follow them in an emergency.

This restore procedure is as important as the backup itself.

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
