---
title: Deployment
nav_order: 12
has_children: true
---

# Deployment

Running a program on your laptop is not the same as running a service. A service runs 24/7, survives reboots, handles multiple users at once, and recovers from failures automatically.

This section deploys the library app on a Raspberry Pi as a real service.

## The Architecture

```
Browser
  ↓
DNS (Raspberry Pi BIND)
  ↓
Nginx (reverse proxy)
  ↓
Flask (app server)
  ↓
SQLite (database)
```

## Topics

- Nginx as a reverse proxy
- Running Flask as a system service
- Cron jobs for backups and reports
- Monitoring

## Exercises

- [10.1 Run Flask on the Pi](exercise-01-first-backup.md)
- [10.2 Nginx as Reverse Proxy](exercise-02-nginx.md)
- [10.3 Flask as a Service](exercise-03-systemd.md)
- [10.4 Automated Backups](exercise-04-cron-backup.md)
- [10.5 Weekly Report](exercise-05-weekly-report.md)