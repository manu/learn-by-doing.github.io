---
title: Architecture Reviews
nav_order: 15
---

# Architecture Reviews

After each major milestone, we step back and review the whole system. Not the code — the architecture.

## Questions for Every Review

1. What does the system do now that it could not do before?
2. What is the weakest part of the current design?
3. What would break first if usage doubled?
4. What decision are we locked into that we might want to change later?

## Review Points

| Milestone | Version | What Changed |
|-----------|---------|--------------|
| Mini Library | v1 | CLI + CSV |
| After Git | v2 | History and branching |
| After Refactoring | v3 | Clean module structure |
| After Real Data | v4 | Performance problems visible |
| After SQL | v5 | SQLite replaces CSV |
| After Web | v6 | Flask web interface |
| After Security | v7 | Authentication + bcrypt |
| After Networking | v8 | DNS + local hostnames |
| After Deployment | v9 | Nginx + systemd + cron |
| After AI | v10 | AI-assisted development workflow |
