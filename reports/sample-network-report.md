# Network Discovery and Traffic Analysis — Lab Report

**Status:** Completed report based on the screenshots supplied for this learning project  
**Date shown in terminal:** 2026-11-05  
**Environment visible:** Kali Linux  
**Nmap version shown:** 7.99  
**Wireshark interface shown:** `eth0`

> Privacy: private LAN IP addresses and hardware identifiers have been redacted from this public report. Only perform scans on systems and networks you own or have explicit permission to assess. The screenshots show a basic host-discovery test against a public hostname; obtain permission and follow applicable policies before testing external systems.

## 1. Executive summary

This exercise practised three foundational network-security tasks: host discovery with Nmap, reachability testing with ping, and packet inspection with Wireshark. The screenshots show Nmap reporting one host as up, one ping test receiving no replies, another ping test receiving replies, and SSDP, ARP, and ICMP traffic in a packet capture.

## 2. Scope and evidence

The report is limited to what can be verified from the supplied screenshots. The complete lab topology and authorisation details were not shown, so no wider network assessment is claimed.

## 3. Tools

- **Kali Linux:** operating system visible in the terminal screenshot.
- **Nmap 7.99:** host-discovery test.
- **Ping:** ICMP reachability tests.
- **Wireshark:** packet capture and protocol inspection.

## 4. Method and results

### 4.1 Nmap host discovery

Command shown:

```bash
nmap -sn google.com
```

Nmap resolved the hostname, reported the host as up with approximately 0.20 seconds latency, and completed with one IP address up and one host scanned.

The `-sn` option performs host discovery without a port scan. Therefore, this test does not provide evidence of open ports or running services.

### 4.2 Ping tests

| Target | Result | Interpretation |
|---|---|---|
| Private LAN target (redacted) | 454 transmitted, 0 received; 100% packet loss | No echo replies were received. This does not prove the target was offline. |
| `lasu.com` | Replies received from the resolved host | The target responded to ICMP echo requests. Visible response times were approximately 277–411 ms. |

A missing reply can be caused by filtering, firewall configuration, routing, or an unavailable host. Further authorised checks would be needed to determine the cause.

### 4.3 Wireshark capture

The screenshot shows a capture on `eth0` and the following protocols:

- **SSDP:** repeated service-announcement `NOTIFY` messages sent to multicast address `239.255.255.250`.
- **ARP:** broadcast requests asking which local device owns a particular IPv4 address.
- **ICMP:** echo request and reply traffic associated with a ping test.

These observations demonstrate the ability to recognise common network protocols in a packet capture. They do not establish compromise or a security vulnerability.

## 5. Skills demonstrated

- Basic Nmap host discovery.
- ICMP connectivity testing and packet-loss interpretation.
- Recognition of SSDP, ARP, and ICMP.
- Introductory packet analysis with Wireshark.
- Evidence-based technical documentation and privacy awareness.

## 6. Limitations

- No port scan or service enumeration is shown.
- The screenshots do not provide a complete network diagram or device inventory.
- A packet capture represents only traffic observed during its capture window.
- A host that does not respond to ping may still be active.

## 7. Conclusion

The exercise provided practical exposure to network discovery, connectivity testing, and packet analysis. It demonstrates foundational skills and an understanding of the limitations of basic network tests. Further work should document an authorised lab topology, collect redacted evidence, and explain additional observations without making unsupported security claims.

## 8. Evidence

The original screenshots were supplied during the project review. Before adding them to this public repository, redact private IP addresses, MAC addresses, device names, and any other identifying network information.
