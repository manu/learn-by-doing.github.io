---
title: "9.2 Set Up BIND on Raspberry Pi"
parent: Networking
nav_order: 2
---

# Exercise 9.2 — Set Up BIND on Raspberry Pi

## The Story

In Exercise 9.1, you discovered why `library.elasticnode.com` only works on one laptop: that name exists only on the Raspberry Pi's private DNS server. Laptop A was configured to ask that server. Laptop B was not.

Now you will build that DNS server.

BIND (Berkeley Internet Name Domain) is the most widely used DNS server software in the world. It runs on the Raspberry Pi. Every device on the local network that asks the Pi for a hostname will get an answer that the public internet has never heard of.

## What to Do

### Step 1 — Install BIND on the Raspberry Pi

SSH into the Raspberry Pi:
```
ssh pi@192.168.x.x
```

Install BIND:
```
sudo apt update
sudo apt install bind9 bind9utils bind9-doc
```

Check that it started:
```
sudo systemctl status bind9
```

### Step 2 — Understand the configuration files

BIND's configuration lives in `/etc/bind/`. The main files are:
- `named.conf` — the master configuration (usually includes others)
- `named.conf.options` — global options (where to forward unknown queries)
- `named.conf.local` — your custom zones

Read each file. You will not understand everything yet — focus on the structure. Write down what you do not understand.

### Step 3 — Configure forwarding

Edit `/etc/bind/named.conf.options` to forward unknown queries to a public DNS server (like Google's `8.8.8.8`). This means: if the Pi does not know a hostname, it asks Google instead of failing.

This is what makes private DNS coexist with the public internet — local names resolve locally, everything else still works normally.

### Step 4 — Test the server is running

From another device on the same network, run:
```
nslookup google.com 192.168.x.x
```

Replace `192.168.x.x` with the Pi's IP address. If BIND is running correctly and forwarding is configured, you should see Google's IP address in the response.

## Topics You Will Learn

- What a DNS server does (resolves names to IP addresses)
- Installing and starting a service with `apt` and `systemctl`
- BIND configuration file structure
- DNS forwarding — passing unknown queries to an upstream resolver
- `nslookup` — the tool for querying DNS servers

## Before You Start — Think About This

1. A DNS server receives a query like "what is the IP address of google.com?" and returns an answer. Where does the Pi get the answer if it does not know? What happens if the upstream server is also unavailable?
2. The Pi is now a DNS server, but other devices still use their default DNS (probably the router). How does a device know which DNS server to ask?
3. BIND is a network service — it listens for connections on port 53 (the standard DNS port). What is the risk of running a service that accepts connections from any device on the network?

## When You're Stuck

- If `systemctl status bind9` shows errors, check `/var/log/syslog` for detailed error messages: `sudo tail -f /var/log/syslog`
- BIND configuration syntax errors will prevent it from starting. Run `sudo named-checkconf` to validate the configuration before restarting.
- Make sure the Pi's firewall (if enabled) allows connections on UDP port 53.

## Once It Works — Go Further

1. Change the DNS settings on one laptop to use the Raspberry Pi's IP as the DNS server. Then run `nslookup google.com` from that laptop — the query is now going through the Pi. Verify this by watching the Pi's logs: `sudo journalctl -u bind9 -f`
2. Look up what a *recursive resolver* is versus an *authoritative nameserver*. Which one is your Pi? Which one is `8.8.8.8`?
