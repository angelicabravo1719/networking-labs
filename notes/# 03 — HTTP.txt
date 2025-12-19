# 03 — HTTP (Unencrypted Web Traffic)

## Goal (plain English)
Show what **HTTP** looks like on the network and why it’s considered **insecure**:
- With HTTP, the request/response can be read in “plain text” by anyone who can sniff the traffic.

## What I did
1) Opened Wireshark and started a capture on my active interface (Wi-Fi).
2) Visited an **HTTP-only** site in a browser so traffic would be visible.
   - Recommended examples:
     - http://neverssl.com (stays HTTP)
     - http://http.badssl.com (HTTP demo)
3) Stopped the capture and filtered to only HTTP traffic.

## Wireshark filters used
- Show HTTP packets:
  - `http`
- If you need to confirm it’s HTTP over port 80:
  - `tcp.port == 80`

## What I observed / how to explain it
- I could see **HTTP methods** like `GET` and `POST` and the HTTP version (ex: `HTTP/1.1`).
- I could see readable details such as:
  - **Host** header (the domain)
  - **User-Agent** (browser info)
  - **Request path** (ex: `/online/` or `/index.html`)
- This demonstrates that with HTTP, **metadata and sometimes content** can be viewed by an attacker on the same network.

## How to find the “website” in HTTP
1) Click an HTTP `GET` packet.
2) In the packet details, expand:
   - `Hypertext Transfer Protocol`
3) Look for:
   - `Host: ...`
   - `GET /...`

## Evidence I saved (portfolio-friendly)
- Capture file: `captures/http_get.pcapng`
- Screenshot: `screenshots/http_filter.png` (showing the `http` filter + a visible `GET`)
- These notes: `notes/03_http.md`

## Why this matters (interview-ready)
- “I captured HTTP traffic to show that it’s **unencrypted**. In Wireshark I could read the `GET` request and headers like the `Host` value. That’s why HTTPS is the standard—HTTP can expose sensitive info on the wire.”

## Privacy note
I used a demo HTTP site and avoided logging into anything sensitive during capture.
