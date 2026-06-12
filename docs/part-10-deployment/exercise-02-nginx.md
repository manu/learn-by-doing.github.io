---
title: "10.2 Nginx as Reverse Proxy"
parent: Deployment
nav_order: 2
---

# Exercise 10.2 — Nginx as Reverse Proxy

## The Story

Flask is running on the Pi on port 5000. To access it, users type `http://192.168.1.x:5000`. That is not a real URL — it is an internal address with a port number.

Real web services use standard ports: port 80 for HTTP, port 443 for HTTPS. When you type `http://library.elasticnode.com`, the browser connects on port 80 — no port number needed.

Nginx is a web server that sits in front of Flask. It listens on port 80, receives requests, and forwards them to Flask on port 5000. This is called a *reverse proxy*.

The browser talks to Nginx. Nginx talks to Flask. Flask never talks to the browser directly.

## What to Do

### Step 1 — Install Nginx on the Pi

```
sudo apt install nginx
sudo systemctl start nginx
sudo systemctl enable nginx
```

Verify it is running by navigating to `http://192.168.x.x` (no port number) in the browser. You should see the Nginx default page.

### Step 2 — Create a configuration file for the library

Create `/etc/nginx/sites-available/library`:

This file tells Nginx:
- Listen on port 80 for requests to `library.elasticnode.com`
- Forward those requests to `localhost:5000` (Flask)
- Pass the real client IP address in a header so Flask can log it

### Step 3 — Enable the site

```
sudo ln -s /etc/nginx/sites-available/library /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

`nginx -t` tests the configuration for errors before reloading.

### Step 4 — Access via the domain name

Make sure:
- DNS is resolving `library.elasticnode.com` to the Pi's IP (from Exercise 9.3)
- Flask is running on the Pi on port 5000
- Nginx is running on port 80

Then navigate to `http://library.elasticnode.com`. The library should load — through Nginx, which forwarded the request to Flask.

### Step 5 — Understand what Nginx is doing

Use the Network tab in Developer Tools. Look at the response headers. Can you tell that Nginx is in the middle? What headers does it add?

## Topics You Will Learn

- Nginx installation and configuration
- What a reverse proxy is and why it exists
- Nginx `server` block and `location` block
- `proxy_pass` directive
- The value of standard ports (80/443) for end users
- Separation of concerns: Nginx handles HTTP details, Flask handles application logic

## Before You Start — Think About This

1. Flask can serve HTTP on its own. Why add Nginx in front of it? What does Nginx provide that Flask's development server does not? (Think about: SSL termination, static file serving, connection handling, logging.)
2. A reverse proxy hides the internal structure of your application. From the browser's perspective, it is talking to one server. In reality, there could be five Flask processes behind Nginx. Why would you want this?
3. If Flask crashes, what does Nginx do? What would users see?

## When You're Stuck

- The Nginx configuration file uses specific syntax — spacing and semicolons matter. Run `sudo nginx -t` after every edit to check for syntax errors.
- `sudo tail -f /var/log/nginx/error.log` shows real-time Nginx errors.
- If you get a "502 Bad Gateway" error, it means Nginx is running but cannot reach Flask. Is Flask running? Is it on the right port?

## Once It Works — Go Further

1. Configure Nginx to serve the contents of a `static/` folder directly (CSS, images, JS) without forwarding those requests to Flask. This is more efficient and is how most production applications work.
2. Look up how to configure Nginx to serve HTTPS using a self-signed certificate. While self-signed certificates generate browser warnings, the process is identical to setting up real HTTPS — it teaches you what SSL termination means.
