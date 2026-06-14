---
title: "9.1 DNS Mystery"
parent: Networking
nav_order: 1
---

# Exercise 9.1 — DNS Mystery

## The Story

The library app is finally running on the Raspberry Pi. You tell the school's librarian how to access it: "Just go to `192.168.1.47:5000` in your browser."

She writes it down on a piece of paper. She calls a colleague. "Go to the library system." He asks for the address. She reads out "one-nine-two-dot-one-six-eight-dot-one-dot-four-seven-colon-five-zero-zero-zero." He writes it down wrong. He gets the wrong page.

Two weeks later, the Raspberry Pi gets a new IP address when the router is restarted. All the paper slips are wrong. Every device that was "configured" to use the library must be updated.

You realize that IP addresses are for computers, not for humans. There must be a better way.

Then you hear about a teacher in another school building who typed `library.elasticnode.com` into his browser and the library loaded immediately. But when you try the same URL on your laptop, the browser says "Server not found."

Both laptops are on the same Wi-Fi network.

Why does it work on his laptop and not yours?

## What to Do

### Part A — Experience the IP address problem

Find the IP address of the Raspberry Pi. Tell a classmate or family member to visit that address in their browser. Observe:
- Can they remember it?
- Can they type it without error?
- What would happen if the Pi's IP address changed tomorrow?

Write down the specific problems with using IP addresses as the way people access services.

### Part B — Investigate the DNS mystery

On the laptop where `library.elasticnode.com` works, find which DNS server it is using. (Look up how to check DNS settings on your operating system.)

On the laptop where it does not work, check the same thing.

Write down what is different. Why would using a different DNS server cause a name to not be found?

### Part C — Understand name resolution

Think through what happens between the moment you type `library.elasticnode.com` and the moment the page loads:
1. Your browser needs an IP address — it does not know how to connect to a name
2. Something has to translate the name into an IP address
3. If the translator does not know the name, it cannot give an answer

Write a step-by-step description of what you think happens. Be as specific as you can.

Then look up "DNS resolution" and compare what you described to how it actually works.

### Part D — Answer the fundamental question

Write two short paragraphs:
1. What problem was DNS invented to solve? (Before DNS, how did computers find each other by name? Look up the history — specifically what a "hosts file" is and why it stopped working.)
2. Why does the answer to "what is the IP address of library.elasticnode.com?" depend on which DNS server you ask?

## Before You Start — Think About This

1. Every device on the internet has an IP address — a number like `142.250.180.46`. Why can't we just use numbers for everything? What specific problems do numbers create that names solve?
2. The name `library.elasticnode.com` does not exist on the public internet — no public DNS server knows about it. It only exists in the Pi's private DNS. How can a private name work on the local network without being registered publicly?
3. When you type `google.com` in a browser, your computer asks a DNS server for the IP address. How does your computer know which DNS server to ask? Who configured that?

## When You're Stuck

- On Windows, open Command Prompt and type `ipconfig /all` — the DNS server addresses are listed there.
- On macOS, open System Preferences → Network → Advanced → DNS.
- The hosts file is at `C:\Windows\System32\drivers\etc\hosts` on Windows and `/etc/hosts` on macOS/Linux. Open it and read it. This is the pre-DNS method.

## Once It Works — Go Further

1. Open the hosts file on your computer and add a line that maps a fake name (like `myfakesite`) to `127.0.0.1` (your own computer). Then open `http://myfakesite` in a browser. What happens? This is the hosts-file approach to name resolution — and why it does not scale.
2. Look up how many DNS queries your computer makes in a typical minute. Open Wireshark (a network monitoring tool) and filter for DNS traffic. What names is your computer looking up?
