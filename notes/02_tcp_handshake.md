----TCP 3-Way Handshake (HTTPS)



----Goal

Capture and explain the TCP 3-way handshake and identify the destination domain (SNI) for an HTTPS connection.



----Evidence Files

\- Capture: `captures/tcp\_handshake.pcapng`

\- Screenshot: `screenshots/tcp\_handshake.png`



----Filter Used

\- `tcp.port == 54368` (filtered to one client ephemeral port for a single connection)



----What I observed

\- SYN: client (10.108.165.224:54368) → server (52.182.143.214:443)

\- SYN-ACK: server → client

\- ACK: client → server (connection established)

\- TLSv1.3 Client Hello followed the handshake (HTTPS encryption negotiation)

\- SNI observed in Client Hello: `teams.events.data.microsoft.com`



----Why it matters

The TCP handshake proves a connection was established, and TLS SNI can reveal the destination domain even when the HTTP content is encrypted.



