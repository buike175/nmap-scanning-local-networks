# Methodology

## 1. Define the scope
Before beginning, identify the lab network, the devices included, and the permission that authorises the activity. Do not scan public, workplace, school, or third-party networks without explicit approval.

## 2. Prepare the lab
Record:
- Date and time of the exercise
- Operating system
- Nmap version
- Lab topology or a simple network diagram
- Approved IP range or lab target (keep private details out of public commits)

## 3. Perform basic discovery
For an authorised lab subnet, Nmap's host-discovery mode can be used to identify responding hosts:

```bash
nmap -sn <authorised-lab-subnet>
```

Replace the placeholder with the subnet assigned to your own lab. Do not copy an address range from an unrelated network.

## 4. Review the output
Review the output carefully. Record only observations supported by the scan, and distinguish between:
- A host that responded to discovery
- A host that did not respond (which does not prove it is offline)
- A result that needs further verification

## 5. Document the exercise
Use the report template in `reports/sample-network-report.md`. Include the scope, environment, method, observations, limitations, and a short conclusion.

## 6. Protect information
Before publishing, redact public IP addresses, personal device names, MAC addresses, usernames, and any other information that could identify a person or expose a private network.

## Limitations
Host discovery can miss devices that do not respond to the probes used or that are filtered by network controls. Results are a snapshot of the lab at the time of the exercise, not a guarantee that every device was found.
