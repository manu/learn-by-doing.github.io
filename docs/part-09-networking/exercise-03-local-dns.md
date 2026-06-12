---
title: "9.3 Local DNS Records"
parent: Networking
nav_order: 3
---

# Exercise 9.3 — Local DNS Records

## The Story

The BIND server is running. Devices that use it can resolve public names like `google.com`. But it still does not know anything about `library.elasticnode.com` — the local name that only exists on your network.

To add local names, you create a *zone* — a set of DNS records for a domain that your server is authoritative for. When any device on the network asks for anything under `elasticnode.com`, your Pi answers from its own records instead of forwarding to the internet.

## What to Do

### Step 1 — Create the zone file

Create a file at `/etc/bind/db.elasticnode.com`:

This file defines:
- The Start of Authority (SOA) record — identifies this server as authoritative for the zone
- Name Server (NS) record — names this server as the nameserver
- A records — maps hostnames to IP addresses

You will add three A records:
- `library.elasticnode.com` → Pi's IP address
- `school.elasticnode.com` → Pi's IP address (or another device's IP)
- `git.elasticnode.com` → Pi's IP address

### Step 2 — Register the zone with BIND

Edit `/etc/bind/named.conf.local` to add:

```
zone "elasticnode.com" {
    type master;
    file "/etc/bind/db.elasticnode.com";
};
```

Restart BIND:
```
sudo systemctl restart bind9
```

Check for errors:
```
sudo named-checkzone elasticnode.com /etc/bind/db.elasticnode.com
```

### Step 3 — Test from another device

Change a laptop's DNS server to the Pi's IP address. Then open a terminal and run:

```
nslookup library.elasticnode.com
```

It should return the Pi's IP address.

Then open a browser and type `http://library.elasticnode.com`. If the Flask app is running on the Pi, the library page should load.

### Step 4 — Test what still works

While using the Pi as your DNS server, verify:
- `google.com` still resolves (forwarding works)
- `library.elasticnode.com` resolves to the Pi
- A hostname that does not exist (e.g., `fake.elasticnode.com`) returns NXDOMAIN (no such domain)

## Topics You Will Learn

- DNS zone files and record types (SOA, NS, A)
- What it means to be "authoritative" for a domain
- How private DNS coexists with public DNS
- BIND zone configuration in `named.conf.local`
- `nslookup` and `dig` for testing DNS

## Before You Start — Think About This

1. An A record maps a name to an IP. The Pi's IP address is `192.168.1.x` — a private address that only exists inside your network. What would happen if someone outside your network tried to resolve `library.elasticnode.com` using a public DNS server?
2. You are making your Pi the authoritative server for `elasticnode.com`. Does this mean you own that domain? What would happen if someone actually owned `elasticnode.com` and set up their own public DNS?
3. Every time you change a DNS record, what has to happen before devices will see the change? (Look up DNS TTL — Time To Live.)

## When You're Stuck

- `named-checkzone` validates the zone file before BIND loads it. Fix any errors it reports before restarting.
- The most common mistake is a missing trailing dot (`.`) in the zone file. `library.elasticnode.com.` with a dot at the end is a fully-qualified domain name; without the dot, BIND appends the zone name, giving `library.elasticnode.com.elasticnode.com`.
- If DNS changes seem to not take effect, flush the DNS cache on the testing device: on Windows, `ipconfig /flushdns`; on macOS, `sudo killall -HUP mDNSResponder`.

## Once It Works — Go Further

1. Add a CNAME record — an alias. Add `www.library.elasticnode.com` as a CNAME pointing to `library.elasticnode.com`. Test that both hostnames resolve to the same IP.
2. Set up a second service on the Pi (for example, a simple Python HTTP server on port 8080). Add a new A record for it (`api.elasticnode.com`). Navigate to it from the browser using the name. You have now built a local DNS-based microservices infrastructure.
