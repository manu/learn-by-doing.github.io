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

### Part A — Install Nginx and observe the default page

Install Nginx on the Pi using the package manager. After installation, start it and configure it to start automatically on every boot.

Open a browser and navigate to the Pi's IP address — no port number, just the address. You should see Nginx's default welcome page. Write down what you observe: Nginx is already serving a page, and Flask has nothing to do with it.

### Part B — Create the library's configuration

Nginx's configuration tells it how to handle different hostnames and paths. For the library, you need to configure Nginx to:
- Listen for requests to `library.elasticnode.com` on port 80
- Forward those requests to Flask on port 5000
- Pass the real browser's IP address to Flask (so logs show the actual visitor)

Look up "Nginx reverse proxy configuration" and "Nginx server block". Nginx keeps available configurations in one folder and enabled configurations in another — learn how these two folders relate and why.

Write the configuration file. Run Nginx's built-in configuration checker after every edit — it tells you exactly what is wrong.

### Part C — Enable and reload

Enable your configuration and reload Nginx so it picks up the new settings without restarting completely (a restart briefly drops all connections).

If the reload fails, read the error carefully — Nginx tells you exactly which line has a problem.

### Part D — Access the library through Nginx

Verify all three layers are running: DNS resolves the name, Nginx is on port 80, and Flask is on port 5000.

Navigate to `http://library.elasticnode.com` in the browser. The library should load.

Open Developer Tools and look at the response headers. Can you tell that Nginx is in the middle? What headers does Nginx add that Flask did not?

Draw the complete request path on paper: browser → DNS → Nginx → Flask → database → Flask → Nginx → browser. This is the architecture you have built.

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
