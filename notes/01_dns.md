DNS Lookup Capture



----Goal

Capture and explain a DNS query + response.



Steps

1\. Started a Wireshark capture on my active adapter

2\. Ran `nslookup google.com` and `nslookup openai.com`

3\. Applied the display filter `dns`

4\. Saved the capture as `captures/dns\_lookup.pcapng`

5\. Took a screenshot as `screenshots/dns\_lookup.png`



----What I observed

\- Query: my computer asked a DNS server for the IP address of a domain

\- Response: the DNS server returned one or more IP addresses



----Why it matters

DNS traffic and DNS logs are often the first clue in investigations to understand what systems tried to reach.



