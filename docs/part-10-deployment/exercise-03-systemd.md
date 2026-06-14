---
title: "10.3 Flask as a Service"
parent: Deployment
nav_order: 3
---

# Exercise 10.3 — Flask as a Service (systemd)

## The Story

Flask is running. Nginx is forwarding requests to it. But Flask is still started manually — you SSH in, run the command, and keep the SSH session alive.

If the Pi reboots, the library is down. If you forget to restart Flask after a code change, the library is running old code. If Flask crashes, nobody knows until someone notices the site is broken.

*systemd* is the service manager built into Linux. It starts services when the Pi boots, restarts them if they crash, and logs their output. You will register Flask as a systemd service so the library runs automatically and reliably.

## What to Do

### Part A — Design the service properties

Before creating any files, write down the properties your library service must have:
1. It must start automatically when the Pi boots
2. If Flask crashes, it must restart without anyone having to log in and start it manually
3. Its output (logs) must be captured so you can read them later
4. It must run as a specific user, not as root

Look up `systemd unit files` — a systemd service is described in a text file called a unit file. Find out what the three sections are (`[Unit]`, `[Service]`, `[Install]`) and what goes in each one.

### Part B — Create the unit file

Create a unit file for the library service at `/etc/systemd/system/library.service`. The file must specify:
- A description of what this service is
- When to start it (after the network is ready)
- Which user to run as
- Which directory to run from
- The command that starts Flask (consider using Gunicorn instead of Flask's development server — look up why)
- Any environment variables Flask needs (the app name, the secret key)
- What to do if the service crashes

### Part C — Enable, start, and verify

After creating the unit file, tell systemd about it, enable it to start on boot, and start it immediately. Check its status.

### Part D — Test that it actually works

Reboot the Pi completely. Wait for it to come back. Without SSHing in or running any commands, open a browser and navigate to `http://library.elasticnode.com`.

If the library loads, your service is working correctly.

Then test the self-healing: find the process ID of the running Flask process and terminate it forcefully. Wait a few seconds. Check the service status. Has systemd restarted it?

## Topics You Will Learn

- systemd unit files (`[Unit]`, `[Service]`, `[Install]` sections)
- `systemctl enable` (start on boot) vs `systemctl start` (start now)
- `systemctl status`, `journalctl -u library` (viewing logs)
- Environment variables in service files
- Gunicorn — a production WSGI server (better than `flask run` for serving requests)
- The principle: a service should be self-healing, not manually supervised

## Before You Start — Think About This

1. What is the difference between a process and a service? A process is a running program. What additional properties does a service have that a process does not?
2. Why should Flask not run as the `root` user (the superuser)? What is the security principle here?
3. `flask run` uses Flask's built-in development server. For production, engineers use Gunicorn or uWSGI — dedicated WSGI servers. What does "WSGI" mean and why is the development server not suitable for production?

## When You're Stuck

- If the service fails to start, check the logs: `sudo journalctl -u library -n 50` (last 50 lines).
- The most common issue is the wrong working directory or wrong path to the Python executable. Verify with `which python3` and `which gunicorn` on the Pi.
- Install Gunicorn: `pip3 install gunicorn`. Then use `gunicorn -w 2 -b 127.0.0.1:5000 app:app` as the service command.

## Once It Works — Go Further

1. Look at the other services running on the Pi: `systemctl list-units --type=service`. Find Nginx and BIND in the list. What is the dependency order? (If BIND fails to start, does Nginx care? Does Flask care?)
2. Set up log rotation for the library service logs so they do not fill the Pi's storage over time. Look up `journald` configuration for log size limits.
