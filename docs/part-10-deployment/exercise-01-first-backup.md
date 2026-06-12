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

### Step 1 — Copy the project to the Pi

From your laptop, copy the project files to the Pi:
```
scp -r ~/library-project pi@192.168.x.x:~/library-project
```

Or clone from GitHub if you have pushed your code there.

### Step 2 — Install dependencies on the Pi

SSH into the Pi and install Flask and bcrypt:
```
ssh pi@192.168.x.x
cd library-project
pip3 install flask bcrypt
```

### Step 3 — Run Flask on the Pi

By default, Flask binds to `127.0.0.1` (localhost only). To accept connections from other devices on the network, bind to `0.0.0.0`:

```
flask run --host=0.0.0.0 --port=5000
```

### Step 4 — Access from another device

On another device on the same network, open a browser and navigate to:
```
http://192.168.x.x:5000
```

Replace `192.168.x.x` with the Pi's IP address. The library should load.

### Step 5 — What breaks when you close the SSH connection

Close the SSH session (or press Ctrl+C). What happens to the web app?

Try to access it from the browser. It is gone.

Write down: why is this a problem for a production service? What would need to change?

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
