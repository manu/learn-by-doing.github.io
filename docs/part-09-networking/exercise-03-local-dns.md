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

### Part A — Design the zone

Before touching any configuration files, design the three records you need:

| Name | Points to |
|------|-----------|
| `library.elasticnode.com` | Pi's IP address |
| `school.elasticnode.com` | Pi's IP address (or another device's) |
| `git.elasticnode.com` | Pi's IP address |

These are called A records — they map a hostname to an IPv4 address.

But a zone file needs more than just A records. It also needs to identify who is authoritative for the zone and name the DNS server. Look up what SOA and NS records are before creating the file.

### Part B — Create the zone file

Create a zone file on the Pi for the `elasticnode.com` domain. DNS zone files have a specific syntax — look up the format. The file needs:
- An SOA record declaring this server as authoritative
- An NS record naming the DNS server
- Three A records for your three services

Use the BIND validation tool to check the file for errors before telling BIND to load it. Fix any errors it reports.

### Part C — Register the zone with BIND

Tell BIND to use your zone file. Edit BIND's local configuration to add a zone declaration for `elasticnode.com`, pointing to the file you created.

After restarting BIND, query for `library.elasticnode.com` from another device — asking the Pi specifically. You should get back the Pi's IP address.

### Part D — Full end-to-end test

Change a laptop's DNS setting to use the Pi's IP address. Now run all four checks:
- `google.com` still resolves (forwarding still works)
- `library.elasticnode.com` resolves to the Pi
- `school.elasticnode.com` and `git.elasticnode.com` also resolve
- A name that does not exist returns an error (not a wrong answer)

Open a browser and type `http://library.elasticnode.com`. If the library Flask app is running on the Pi, the page should load.

Write down each result.

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
