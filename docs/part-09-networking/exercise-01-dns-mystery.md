---
title: "9.1 DNS Mystery"
parent: Networking
nav_order: 1
---

# Exercise 9.1 — DNS Mystery

## Scenario

The library app is running on a Raspberry Pi on your local network.

On Laptop A: `http://library.elasticnode.com` loads perfectly.

On Laptop B: the browser says "Server not found."

Both laptops are on the same Wi-Fi network.

## What to Investigate

1. What DNS server is Laptop A using?
2. What DNS server is Laptop B using?
3. What is different between them?

## What to Observe

The name `library.elasticnode.com` does not exist on the public internet. It only exists in the Raspberry Pi's local DNS. If your computer does not know to ask the Raspberry Pi for names, it will never find the answer.

## The Question

What problem was DNS invented to solve? Why do we use names instead of IP addresses?

## Concept

Name resolution — how a hostname becomes an IP address, and why the answer depends on which DNS server you ask.
