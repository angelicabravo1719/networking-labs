# 02 — TCP Handshake (How Connections Start)

## Goal (plain English)
Show the **TCP 3-way handshake**:
- This is how a reliable connection starts before data is exchanged (common for HTTPS over TCP/443).

## What I did
1) Opened Wireshark and started a capture on my active interface (Wi-Fi).
2) Triggered a new connection by opening a website or app connection.
3) Filtered to the handshake traffic and identified:
   - SYN → SYN/ACK → ACK
4) Saved the capture + screenshot for evidence.

## Wireshark filters used
- Show TCP packets:
  - `tcp`
- Focus on a specific port (common for HTTPS):
  - `tcp.port == 443`
- Find handshake SYN packets:
  - `tcp.flags.syn == 1 and tcp.flags.ack == 0`
- Or just SYN packets (includes SYN/ACK too):
  - `tcp.flags.syn == 1`

## What I observed / how to explain it
- **SYN**: my computer says “Can we start a connection?”
- **SYN/ACK**: the server replies “Yes — I’m ready.”
- **ACK**: my computer confirms “Great — connection is established.”

After that, the connection can carry application data (like TLS/HTTPS).

## How to confirm it’s the handshake
1) Look in the packet list “Info” column for:
   - `[SYN]`
   - `[SYN, ACK]`
   - `[ACK]`
2) Confirm the same 4-tuple:
   - Source IP/port ↔ Destination IP/port

## Evidence I saved (portfolio-friendly)
- Capture file: `captures/tcp_handshake.pcapng`
- Screenshot: `screenshots/tcp_handshake.png`
- These notes: `notes/02_tcp_handshake.md`

## Why this matters (interview-ready)
- “TCP is the foundation for many protocols. I captured a 3-way handshake in Wireshark to show
