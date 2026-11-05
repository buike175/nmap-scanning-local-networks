# Findings and Analysis

## Exercise summary

This page records observations visible in the screenshots supplied for this project. The screenshots show Kali Linux, Nmap 7.99, terminal connectivity tests, and a Wireshark capture on interface `eth0`.

**Privacy note:** Private LAN addresses and hardware identifiers are intentionally omitted from this public report. Keep original screenshots private or redact them before committing.

## 1. Nmap host-discovery test

Command shown:

```bash
nmap -sn google.com
```

Observed results:
- Nmap version: 7.99
- The hostname resolved to an IPv4 address.
- Nmap reported the host as up, with approximately 0.20 seconds of latency.
- The output reported one IP address up and one host scanned.
- A reverse-DNS name was displayed for the resolved address.

Interpretation: The host-discovery test received enough response to report the target as reachable at the time of the test. The `-sn` option performs host discovery without a port scan, so this output does not identify open ports or services.

## 2. ICMP connectivity tests

Two ping tests are visible:

| Test | Observed result | Interpretation |
|---|---|---|
| Private lab address (redacted) | 454 packets transmitted, 0 received; 100% packet loss | No ICMP echo replies were received during this test. This alone does not prove the device was offline. |
| `lasu.com` | ICMP echo replies received from the resolved host | The target responded to ICMP echo requests during the capture shown. Visible response times were approximately 277–411 ms. |

Possible reasons for no reply include a host being unavailable, ICMP filtering, firewall rules, or network configuration. More evidence would be needed to distinguish these possibilities.

## 3. Wireshark packet observations

The screenshot shows a live capture on `eth0`. The visible packet list includes:

| Protocol | Visible evidence | What it means |
|---|---|---|
| SSDP | Repeated `NOTIFY * HTTP/1.1` messages sent to multicast address `239.255.255.250` | Devices are advertising service-discovery information using SSDP. |
| ARP | Broadcast `Who has ...?` requests | A device is asking which local interface owns an IPv4 address so it can learn the corresponding link-layer address. |
| ICMP | Echo request and echo reply packets | The capture includes ping traffic and a reply from the remote host. |

The visible capture shows local discovery traffic and ICMP communication. It does not, by itself, establish that a device is compromised or that a vulnerability exists.

## 4. Key learning outcomes

- Used Nmap host-discovery mode and interpreted its summary.
- Used ping to test reachability and compared successful replies with packet loss.
- Identified SSDP, ARP, and ICMP in a Wireshark capture.
- Learned that a lack of ping replies is not conclusive proof that a host is offline.
- Practised separating observed evidence from assumptions.

## 5. Limitations and next steps

- The screenshots do not show a port scan, service enumeration, or vulnerability assessment.
- A single capture is only a snapshot of traffic during the capture period.
- Host firewalls, filtering, and network configuration can affect discovery results.
- Record the exact lab topology, operating system version, Nmap version, date, and scope in future exercises.
- Save redacted screenshots and sanitised output excerpts as supporting evidence.

## Conclusion

The exercise demonstrates introductory network discovery, connectivity testing, and packet-protocol identification. The strongest verified outcomes are a successful Nmap host-discovery result, one ping test with no replies, another with replies, and visible SSDP, ARP, and ICMP traffic in Wireshark.
