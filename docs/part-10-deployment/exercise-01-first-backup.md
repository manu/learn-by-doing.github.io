---
title: "10.1 Run Flask on the Pi"
parent: Deployment
nav_order: 1
---

# Exercise 10.1 — Run Flask on the Raspberry Pi

## The Story

The library web app runs on your laptop. When you close the lid, the library is gone. When you want to use it from another device, you cannot.

A real service runs on a dedicated machine that is always on. For this project, that machine is the Raspberry Pi. This exercise moves the app from your laptop to the Pi and makes it accessible from any device on the local network.

This is your first deployment.

## What to Do

### Part A — Move the project to the Pi

The library project is on your laptop. The Raspberry Pi needs to have the code, the database, and all dependencies.

Think through what needs to transfer:
- The Python source files
- The database file (`library.db`)
- The list of Python packages the app depends on

How will you move these files? There are several approaches — look up `scp` for secure file copy, or use git if you have pushed to GitHub. Choose one and move the project.

### Part B — Install dependencies on the Pi

SSH into the Pi. The Pi does not have Flask or bcrypt installed. Install them.

If you used a `requirements.txt` file to track your project's dependencies, this is the right moment to use it. If you have not created one, create it now — it lists every package the project needs.

### Part C — Start the app and access it from another device

Start Flask on the Pi. There is one important difference from running it on your laptop: Flask's default configuration only accepts connections from the Pi itself. You need to tell Flask to accept connections from any device on the network.

Look up how to configure Flask's host binding. Then start the app.

From another device on the same network, open a browser and navigate to the Pi's IP address on the correct port. The library should load.

### Part D — Discover what breaks

Close the SSH session (without stopping Flask first). Then try to load the library from the browser.

What happened? Why?

Now reboot the Pi. After it comes back up, try to load the library again without doing anything else.

Write down every problem you discovered. These are the requirements for Exercise 10.3.

## Topics You Will Learn

- `scp` — secure file copy between computers
- Flask `--host=0.0.0.0` — binding to all network interfaces
- The difference between `localhost` and a network IP address
- Why a process that runs inside an SSH session dies when the session ends
- The concept of a *daemon* — a process that runs in the background independently

## Before You Start — Think About This

1. The Pi has two IP addresses: `127.0.0.1` (loopback — only accessible from the Pi itself) and `192.168.x.x` (network — accessible from other devices). Why does Flask need to know which one to bind to?
2. When you close the SSH session, the terminal process ends and takes all its child processes with it. What would you need to do to keep a process running after the SSH session ends?
3. If the Pi reboots (power cut, update, etc.), what happens to the Flask process? Would it restart automatically?

## When You're Stuck

- Find the Pi's IP address with: `hostname -I` (run on the Pi)
- If the port is unreachable from another device, check that the Pi's firewall allows port 5000: `sudo ufw allow 5000`
- If Flask cannot find `library.db`, verify the path is correct relative to where you run `flask run` from.

## Once It Works — Go Further

1. Use `nohup flask run --host=0.0.0.0 &` to run Flask in the background so it survives after you close the SSH session. Does this work? What are the risks of this approach compared to a proper service manager?
2. This exercise surfaces the need for systemd (Exercise 10.3). Write down the three things that are wrong with running Flask in an SSH terminal, and what properties a properly managed service would have.
