# Packet Capture Analysis using wireshark

## Overview

This project involves the analysis of a network packet capture to identify protocols, summarize network activity, and document findings. The provided packet capture data was analyzed to extract key insights about network communication, protocols used, and observed issues. Additionally, instructions were provided for exporting the capture as a `.pcap` file, and a markdown summary of the findings was generated.

---

## Objectives

- **Identify Protocols**: Identify at least three different protocols in the packet capture.
- **Export Instructions**: Provide steps to export the capture as a `.pcap` file.
- **Summarize Findings**: Summarize the network activity, packet details, and key observations in markdown format.
- **Generate README**: Document the analysis process and outcomes in this README file.

---

## Analysis Details

### Protocols Identified

The packet capture contains the following protocols:

- **TCP (Transmission Control Protocol)**: Used for reliable data transfer, including HTTPS connections on port 443.
- **TLSv1.2 and TLSv1.3 (Transport Layer Security)**: Used for secure communications with Microsoft and Google services.
- **QUIC (Quick UDP Internet Connections)**: Used for modern, UDP-based secure communication with Google servers.
- **Additional protocols observed**: ARP, ICMPv6, DNS, MDNS, LLMNR, and ICMP.

---

### Packet Capture Export

The provided data was a text-based summary, not raw packet data, so direct conversion to a `.pcap` file was not possible. Instructions were provided for exporting a capture using **Wireshark**:

1. Open the capture in Wireshark.
2. Go to **File > Export Specified Packets**.
3. Select **PCAP** format, specify a file name (e.g., `capture.pcap`), and save.

> **Note**: Raw packet data is required for `.pcap` export, which was not available in the provided text.

---

## Summary of Findings

A detailed summary was generated in markdown format, covering:

- **Secure Communications**: TLSv1.2/TLSv1.3 and QUIC for connections to Microsoft (`watson.events.data.microsoft.com`, `activity.windows.com`) and Google (`instantmessaging-pa.googleapis.com`) servers.
- **Network Discovery**: ARP, ICMPv6, DNS, MDNS, and LLMNR for local and remote address resolution.
- **Issues**: TCP duplicate ACKs, retransmissions, missing segments, and unanswered ICMP Echo requests, indicating potential network instability.
- **Packet Details**: Specific examples of TCP, TLS, QUIC, DNS, ARP, ICMPv6, MDNS, LLMNR, and ICMP traffic, with packet numbers and descriptions.

---

## Key Observations

- The device (`192.168.0.114`) communicates with Microsoft telemetry and Google services.
- **QUIC** usage indicates modern web applications.
- **Local network discovery** suggests a TP-Link router (`192.168.0.1`) environment.
- **TCP issues** (e.g., duplicate ACKs, retransmissions) suggest network congestion or packet loss.

---

## Files Generated

- **Network Packet Capture Summary** (`c61a0867-9a94-4838-a5f7-25606e40516c`): A markdown file summarizing the packet capture analysis, including protocols, packet details, and observations.
- **README.md** (this file): Documents the analysis process and outcomes.

---


