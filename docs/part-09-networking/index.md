---
title: Networking
nav_order: 11
has_children: true
---

# Networking

The library app is running on a Raspberry Pi. You type `library.elasticnode.com` in the browser on one laptop and it works. You try it on another laptop — it fails.

Why?

That question introduces DNS.

## Topics

- IP addresses
- DNS — how names become addresses
- Subnet masks
- Routers and gateways
- Private DNS vs public DNS

## The Experiment

Set one laptop's DNS server to the Raspberry Pi. See what changes. Then understand why.

## Exercises

- [9.1 DNS Mystery](exercise-01-dns-mystery.md)
- [9.2 Set Up BIND on Raspberry Pi](exercise-02-bind-setup.md)
- [9.3 Local DNS Records](exercise-03-local-dns.md)