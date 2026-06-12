---
title: "7.1 Watch a Request"
parent: Web Architecture
nav_order: 1
---

# Exercise 7.1 — Watch a Request

## The Story

Every time you open a website, your browser sends a message to a server and the server sends a message back. This happens so fast that it is invisible. Most people use the web for years without ever seeing what those messages look like.

Before you write a single line of web application code, you will watch a real request happen. This is the most important exercise in Part 7 — because everything that follows (Flask, routes, responses, forms) is just a structured way of creating these messages.

## What to Do

### Step 1 — Open Developer Tools

Open any web browser (Chrome, Firefox, or Edge). Press `F12` to open Developer Tools. Click the **Network** tab.

### Step 2 — Watch a request

Type `http://example.com` in the address bar and press Enter. Watch the Network tab.

You will see one or more rows appear. Click the first row (the main document request). A panel opens on the right.

### Step 3 — Inspect the request

In the panel, find the **Headers** tab. Look at:

- **Request URL**: What was requested
- **Request Method**: Is it `GET` or something else?
- **Status Code**: What did the server respond with? (200 means OK)
- **Request Headers**: Information the browser sent to the server (browser type, accepted languages, etc.)
- **Response Headers**: Information the server sent back (content type, date, server software)

### Step 4 — Look at the response body

Click the **Response** or **Preview** tab. You will see the actual HTML that the server sent back. This is what the browser turned into the page you see.

### Step 5 — Explore

Try these and observe what changes in the Network tab:

1. Visit a page that does not exist on a website (add `/doesnotexist` to any URL). What status code appears?
2. Submit a search form on any website. What method does the search use — GET or POST? Look at the URL — does it change?
3. Visit a page that uses `https://` instead of `http://`. Is there any visible difference in the Network tab?

### Step 6 — Write down what you learned

After exploring, write down your answers to:
- What is the difference between a request and a response?
- What is an HTTP method? What are the two most common ones and when would you use each?
- What does a status code tell you?
- What is the `Content-Type` response header and what does it mean?

## Topics You Will Learn

- HTTP — the language browsers and servers use to communicate
- Request: URL, method (GET/POST), headers, body
- Response: status code, headers, body (HTML/JSON/etc.)
- Common status codes: 200 (OK), 301 (redirect), 404 (not found), 500 (server error)
- The difference between GET (retrieve) and POST (submit data)

## Before You Start — Think About This

1. When you type a URL and press Enter, the browser sends a request. Who receives it? How does the browser know where to send it?
2. The server sends back HTML. The browser then reads that HTML and may need to request more things (images, CSS, JavaScript). Watch the Network tab — how many requests does a typical page make?
3. A web page and a web application both use HTTP. What is the difference between them?

## Once It Works — Go Further

1. Use the Network tab to find a request for an image on any page. What is the `Content-Type` of the response? How is it different from an HTML response?
2. Look at the `User-Agent` header in any request. What information does it contain? Why would a server care about it?
