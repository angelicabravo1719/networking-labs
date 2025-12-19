# 04 — HTTPS (TLS) and SNI (Encrypted Web Traffic)

## Goal (plain English)
Show what **HTTPS** looks like in Wireshark and what you *can* and *cannot* see:
- HTTPS is **HTTP inside encryption** (TLS), so Wireshark can’t read the web page content.
- But you can still see some **metadata**, like the TLS handshake and often the **SNI** hostname.

## Key concept (super important)
Wireshark does **not** label encrypted web traffic as “https”.
- HTTPS traffic is usually decoded as:
  - **TLS** (HTTPS over TCP/443), or
  - **QUIC** (often HTTPS over UDP/443 = HTTP/3)

That’s why typing `https` in the filter bar won’t work.

## What I did
1) Started Wireshark capture on my active interface.
2) Visited an HTTPS website in the browser (examples):
   - https://example.com
   - https://www.wikipedia.org
3) Stopped the capture.
4) Filtered for TLS/QUIC and located the **Client Hello** to find SNI.

## Wireshark filters used (TLS / HTTPS over TCP 443)
- Show TLS packets:
  - `tls`
- Show TLS Client Hello (start of handshake):
  - `tls.handshake.type == 1`
- Show traffic on HTTPS port:
  - `tcp.port == 443`

## Wireshark filters used (QUIC / HTTP/3 over UDP 443)
- Show QUIC packets:
  - `quic`
- Or show UDP 443 (often QUIC):
  - `udp.port == 443`

## Where to find SNI in the packet details
1) Filter: `tls.handshake.type == 1`
2) Click a packet that says **Client Hello**
3) Expand:
   - `Transport Layer Security`
   - `Handshake Protocol: Client Hello`
   - `Extensions`
   - `server_name`
4) You’ll see the hostname (example from my capture: `ecs.office.com`)

## What SNI tells me (and what it doesn’t)
SNI tells me:
- “My machine attempted to connect to **this hostname** over TLS.”

SNI does NOT prove:
- That I manually typed that website into a browser.
- The exact page/URL visited (paths are encrypted in HTTPS).
- The content of what was sent/received (it’s encrypted).

So `ecs.office.com` could be:
- A background connection from Microsoft services/apps (ex: Teams / Office / Windows services),
- not necessarily something I directly browsed to.

## What I observed / how to explain it
- I saw the **TLS handshake** beginning with Client Hello.
- I could identify the destination as HTTPS traffic using port 443.
- I could often identify the **hostname** using SNI (example: `ecs.office.com`).
- I could **not** read the HTTP GET path/content like I could with plain HTTP, because it’s encrypted.

## Evidence I saved
- Capture file: `captures/https_tls_handshake.pcapng` (or `captures/tls_handshake.pcapng`)
- Screenshot: `screenshots/tls_client_hello_sni.png` (showing Client Hello + SNI)
- These notes: `notes/04_https_tls.md`

## Why this matters
- “I compared HTTP vs HTTPS in Wireshark. With HTTP I could read requests in plain text. With HTTPS I could only see the TLS handshake and metadata like SNI. That demonstrates how TLS protects confidentiality in transit, while still leaving some observable connection details.”

## Privacy note
I didn’t decrypt traffic. I only used handshake metadata (SNI/ports) and avoided sensitive logins during capture.
