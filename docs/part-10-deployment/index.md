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

- [First Automated Backup](exercise-01-first-backup.md)