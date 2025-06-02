# Summary of Findings

The packet capture shows network activity involving a local device (`192.168.0.114`) communicating with external servers (e.g., `20.189.173.22`, `20.189.173.21`, `20.230.46.154`) and performing local network discovery. The traffic includes:

---

## Secure Communications

- **TLSv1.2 and TLSv1.3** connections to Microsoft services:
  - `watson.events.data.microsoft.com`
  - `activity.windows.com`
- **Google services** accessed via:
  - `instantmessaging-pa.googleapis.com`
- **QUIC protocol** used with Google servers, indicating modern UDP-based secure connections.
- **TCP connections on port 443** for HTTPS traffic:
  - Includes handshakes, data transfers, and termination sequences.

---

## Network Discovery and Resolution

- **ARP requests** from the router (`TPLink_ac:2b:20`) to resolve IPs:
  - E.g., `192.168.0.110`, `192.168.0.114`
- **ICMPv6 Neighbor Solicitations** for IPv6 resolution.
- **DNS queries** to resolve:
  - `watson.events.data.microsoft.com`
  - `instantmessaging-pa.googleapis.com`
- **MDNS and LLMNR** queries:
  - For local names like `wpad.local`, `wpad`
  - Likely for Web Proxy Auto-Discovery (WPAD)

---

## Issues Observed

- **TCP anomalies:**
  - Duplicate ACKs (packets 2, 321, 322)
  - Retransmissions (packet 323)
  - Missing segments (packets 6, 7)
  - Indicate possible network congestion or packet loss
- **Unanswered ICMP Echo Requests**:
  - Packets 280, 291 to `192.168.0.114` not responded to
  - Suggests host may be non-responsive or firewalled

---

## Packet Details

### TCP Traffic

- Multiple connections to port 443 (HTTPS)
- Example:
  - Packet 15: SYN from `192.168.0.114:7240` to `20.189.173.22:443`
  - Packet 30: SYN-ACK
  - Packet 31: ACK
- Includes full **TLS handshake**:
  - Client Hello, Server Hello, Certificate exchange
  - Application data transfer

### TLS Traffic

- TLSv1.2 and TLSv1.3 used
- Example:
  - Packet 32: Client Hello with SNI=`watson.events.data.microsoft.com`
  - Packet 54: Server Hello and certificate
- TLSv1.3 (e.g., packet 116) to `activity.windows.com`

### QUIC Traffic

- Packets 22–29, 61–78
- Communication with Google IPv6 servers:
  - `2404:6800:4007:80b::200a`
  - `2404:6800:4007:81b::200a`
- Includes:
  - Initial
  - Handshake
  - Protected Payload
  - CRYPTO, PING, PADDING frames

### DNS Queries

- Queries for **A** and **AAAA** records
- Example:
  - Packet 13: AAAA query for `watson.events.data.microsoft.com`
  - Packet 14: Resolved with CNAME chain

### ARP and ICMPv6

- ARP requests/replies:
  - Packet 4 (request), Packet 12 (reply)
- ICMPv6 Neighbor Solicitations:
  - Packet 5

### MDNS and LLMNR

- Repeated queries for `wpad.local`, `wpad`
- Packets 118–125, 128–130, 133

### ICMP

- Echo requests:
  - Packets 280, 291 from `192.168.0.1` to `192.168.0.114`
  - No responses received

---

## Key Observations

- **Device 192.168.0.114** is actively communicating with:
  - Microsoft telemetry servers
  - Google services
- **QUIC** protocol usage suggests:
  - Modern web apps with performance-focused protocols
- **Local network discovery** indicates:
  - Device is part of LAN behind TP-Link router (`192.168.0.1`)
- **TCP reliability issues** suggest:
  - Potential network instability or congestion
