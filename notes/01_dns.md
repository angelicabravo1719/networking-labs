# 01 — DNS Lookup (Name → IP)

## Goal (plain English)
Show what **DNS** looks like on the network:
- DNS is how your computer turns a website name (like `example.com`) into an IP address.

## What I did
1) Opened Wireshark and started a capture on my active interface (Wi-Fi).
2) Triggered a DNS lookup by visiting a website or running a lookup command.
3) Stopped the capture and filtered to DNS traffic.
4) Saved the capture + screenshot for evidence.

## Wireshark filters used
- Show DNS packets:
  - `dns`
- If you want only DNS over the common port:
  - `udp.port == 53` (most common)
  - `tcp.port == 53` (sometimes)

## What I observed / how to explain it
- I saw a **DNS query** (my computer asking: “What is the IP for this domain?”)
- I saw a **DNS response** (the DNS server replying with one or more IPs)
- Common record types:
  - `A` = IPv4 address
  - `AAAA` = IPv6 address
  - `CNAME` = alias (points to another name)

## How to find the “website” in DNS
1) Click a DNS packet.
2) Expand:
   - `Domain Name System (query)`
3) Look for:
   - `Queries` → the domain name (ex: `example.com`)
   - `Answers` → returned IP address(es)

## Evidence I saved (portfolio-friendly)
- Capture file: `captures/dns_lookup.pcapng`
- Screenshot: `screenshots/dns_lookup.png`
- These notes: `notes/01_dns.md`

## Why this matters (interview-ready)
- “DNS is the first step before most web traffic. I captured a DNS query/response in Wireshark to show how domain names resolve to IPs, and how investigators can map network traffic back to domains.”

## Privacy note
I used non-sensitive browsing during capture and only recorded DNS resolution behavior.
