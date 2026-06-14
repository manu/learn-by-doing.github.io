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

### Part A — Install and start BIND

SSH into the Raspberry Pi from your laptop. Install BIND — the most widely-used DNS server software in the world — using the Pi's package manager.

After installation, check whether BIND started automatically. You should see a running service.

BIND listens on port 53, which is the standard DNS port. No device on the network knows about your Pi's DNS yet — they are all still asking the router.

### Part B — Read the configuration files

BIND's configuration lives in `/etc/bind/`. Read each of the main configuration files:
- The master configuration that includes the others
- The options file where global settings (like forwarding) are configured
- The local configuration file where custom zones will go (empty for now)

Do not try to understand everything. Focus on the structure. Write down three things you do not understand, so you know what to look up.

### Part C — Configure forwarding

The Pi should be able to answer queries for local names — but for everything else (google.com, github.com, etc.), it should pass the question on to a public DNS server.

This is called *forwarding*. Edit the options configuration to forward unknown queries to a public resolver. After making the change, restart BIND and check for errors.

### Part D — Verify the server works

From another device on the same network, ask the Pi's DNS server to resolve a public name like `google.com`. You are not asking your router or your internet provider — you are specifically asking the Pi.

If the Pi is running correctly and forwarding is configured, you should get back Google's IP address. If you get an error, read the Pi's service logs — the error is always described there.

Write down what you had to do to ask a specific DNS server instead of the default one.

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
