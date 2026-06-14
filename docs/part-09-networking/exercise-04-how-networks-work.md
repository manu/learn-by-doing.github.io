---
title: "9.4 How Networks Work"
parent: Networking
nav_order: 4
---

# Exercise 9.4 — How Networks Work

## The Story

The library is accessible to everyone on the school's Wi-Fi. A teacher from a different building — connected to a different network segment — tries to visit `library.elasticnode.com`. His DNS is configured correctly. The name resolves. But the page does not load.

He can reach Google. He can reach other websites. But he cannot reach the library on the Raspberry Pi.

You check the Pi. It is running. You can reach it from your own laptop.

Why can a device on one part of the school network reach the Pi, but a device on another part cannot?

This is a networking problem, not a DNS problem. DNS tells you the IP address. Getting to the IP address is a separate problem entirely.

## What to Do

### Part A — Map your network

Find out the following for each device involved in the library system:
- What is its IP address?
- What is its subnet mask?
- What is its default gateway?

Look up these terms before you start:
- **IP address**: a unique address for a device on a network
- **Subnet mask**: defines which part of the IP address identifies the network, and which part identifies the specific device
- **Default gateway**: the address of the router that handles traffic going outside the local network

Write the values down in a table.

### Part B — Understand which devices can talk to each other directly

Two devices can communicate directly (without going through a router) only if they are on the same network — meaning the network portion of their IP addresses matches.

For each pair of devices in your setup, determine: are they on the same network or different networks? Show your working — use the subnet mask to identify the network portion of each IP address.

This is why the teacher in the other building cannot reach the Pi: they are on different network segments. Traffic from his laptop needs to pass through a router to reach the Pi's network.

### Part C — Trace the path a packet takes

When the library Flask app sends a response back to a student's browser, write down the complete path the data packet takes:
- From which process on the Pi (Flask, port 5000)
- Through which network interface on the Pi
- Through which device (router, switch) to reach the student's laptop
- Through which interface to reach the student's browser

This path is what a packet takes every time someone loads a page in the library.

On Windows, the `tracert` command (or `traceroute` on macOS/Linux) shows every device a packet passes through to reach a destination. Run it from a laptop to the Pi's IP address and write down the hops.

### Part D — Understand why this matters for deployment

The library currently runs on the Pi with Flask's development server on port 5000. This means:
- It only works on the local network
- Anyone on the network can access it (no firewall)
- The development server is not designed for multiple simultaneous users

Write a short paragraph describing what would need to change to make the library accessible to devices on different network segments, or from outside the school entirely. You do not need to implement this yet — Part 10 covers deployment. Just reason through what the requirements are.

## Before You Start — Think About This

1. IP addresses like `192.168.1.x` start with `192.168` — these are called "private" addresses. Devices with private addresses cannot be reached directly from the public internet. Why would this be a design choice?
2. A router connects two or more networks. When a packet arrives at a router, how does the router decide where to send it? What information does it use?
3. A switch and a router are different devices. A switch connects devices within the same network. A router connects different networks. In a typical school, where would each one appear?

## When You're Stuck

- On Windows: `ipconfig` shows your IP address, subnet mask, and default gateway.
- On macOS/Linux: `ifconfig` or `ip addr` shows the same information.
- To trace the route to a device: `tracert 192.168.x.x` (Windows) or `traceroute 192.168.x.x` (macOS/Linux).
- A subnet mask of `255.255.255.0` means the first three numbers of the IP address identify the network. Two addresses with the same first three numbers are on the same network.

## Once It Works — Go Further

1. Look up what a VLAN (Virtual Local Area Network) is. Many schools separate teacher devices from student devices using VLANs. How does this affect the library's accessibility?
2. Port forwarding: if the school's internet router were configured to forward traffic on a specific port to the Pi, the library could be reached from the public internet. What are the security implications of doing this?
