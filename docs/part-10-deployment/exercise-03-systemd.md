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

### Step 1 — Create a systemd unit file

Create `/etc/systemd/system/library.service`:

This file describes how to run Flask:
- Which user to run as
- Which directory to start from
- The command to run (`flask run` or `gunicorn`)
- Environment variables (the Flask app name, secret key)
- What to do if it crashes (restart automatically)
- When to start it (after the network is up, on every boot)

### Step 2 — Enable and start the service

```
sudo systemctl daemon-reload
sudo systemctl enable library
sudo systemctl start library
```

`enable` means "start this on every boot." `start` means "start it right now."

### Step 3 — Verify it is running

```
sudo systemctl status library
```

You should see: active (running). The last few lines of output should show Flask starting up.

### Step 4 — Reboot and verify

```
sudo reboot
```

Wait for the Pi to come back up. Without doing anything else, navigate to `http://library.elasticnode.com` in the browser. The library should be running — Flask started automatically on boot.

### Step 5 — Test automatic restart

Find the process ID of Flask: `sudo systemctl status library`. Then kill it: `sudo kill -9 <PID>`. Within a few seconds, check `systemctl status library` again. systemd should have restarted it automatically.

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
