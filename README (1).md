# PENETRATION TESTING REPORT

### Footprinting & Network Scanning Phases

**W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS**

## Report Information

| Field | Detail |
|---|---|
| **Pentester Name** | [Aleeha Hashmi] |
| **Program/Batch** | [B083-Networkwalks] |
| **Date** | [13 November 2026] |
| **Modules Completed** | W2-PM1 (Multiple Kali Tools)<br>W2-PM5 (Zenmap Scanning) |
| **Client/Target** | `networkwalks.com` for authorized educational reconnaissance<br>My own local LAN network for Zenmap scanning |
| **Permission Secured?** | Yes — only authorized systems and my own local network were used |
| **Phases Covered** | **Phase 1:** Reconnaissance & Footprinting<br>**Phase 2:** Scanning & Network Discovery |

## 1. Liability Disclaimer

I performed these activities only on systems and devices where I had permission or that I owned myself. All materials are for education and research purposes only. Unauthorized access, scanning, or testing may lead to legal consequences. Always stay within the approved scope and obtain permission before performing security testing.

## 2. Introduction

This report covers footprinting the `networkwalks.com` domain using multiple Kali Linux tools (W2-PM1) and scanning my own local network with Zenmap (W2-PM5).

The footprinting activity demonstrates how public information can be collected from a website. The Zenmap activity demonstrates how live hosts can be discovered on a local network.

## 3. Tools Used

| Tool | Purpose |
|---|---|
| Kali Linux | Operating system used for reconnaissance |
| WHOIS | Find domain registration details, registrar, dates, and name servers |
| WhatWeb | Fingerprint web technologies, server, CMS, and libraries |
| nslookup | Resolve the domain name to its IP address using DNS |
| curl -I | Read HTTP response headers from the website |
| wafw00f | Detect whether a Web Application Firewall protects the site |
| Zenmap (Nmap GUI) | Scan the local subnet to find live hosts, IP addresses, and MAC addresses |
| Windows | Operating system used for the Zenmap scan |

## 4. Activities Performed

### 4.1 Footprinting & Reconnaissance

I performed reconnaissance against the `networkwalks.com` domain using WHOIS, WhatWeb, Nslookup, Curl, and Wafw00f.

#### WHOIS

```bash
whois networkwalks.com
```

Purpose: Obtain domain registration information, registrar details, dates, and name servers.

![WHOIS output](screenshots/1_whois.png)

#### WhatWeb

```bash
whatweb networkwalks.com
```

Purpose: Identify technologies used by the website, including the web server, CMS, and libraries.

![WhatWeb output](screenshots/2_whatweb.png)

#### DNS Lookup

```bash
nslookup networkwalks.com
```

Observed IP address: `192.232.216.135`

![Nslookup output](screenshots/3_nslookup.png)

#### HTTP Header Analysis

```bash
curl -I https://networkwalks.com
```

Purpose: Inspect HTTP response headers and review publicly exposed technical information.

![Curl output](screenshots/4_curl.png)

#### WAF Detection

```bash
wafw00f networkwalks.com
```

Observed result: **ModSecurity (SpiderLabs) WAF**

![Wafw00f output](screenshots/5_wafw00f.png)

### 4.2 Network Scanning with Zenmap

I used Zenmap to perform network discovery on my own local network.

Target subnet:

```text
192.168.100.0/24
```

Profile:

```text
Ping scan
```

Equivalent command:

```bash
nmap -sn 192.168.100.0/24
```

The scan identified six live hosts:

- `192.168.100.1`
- `192.168.100.4`
- `192.168.100.5`
- `192.168.100.7`
- `192.168.100.8`
- `192.168.100.9`

The scan reported:

```text
Nmap done: 256 IP addresses (6 hosts up)
```

![Zenmap scan results](screenshots/6_zenmap_scan.png)

#### Zenmap Topology

The Topology section displayed the discovered hosts connected to the local host.

![Zenmap topology](screenshots/7_zenmap_topology.png)

## 5. Risk Analysis / Impact

These are observations from the exercises, not confirmed vulnerabilities.

| # | Finding | Potential Impact | Risk Level |
|---|---|---|---|
| 1 | Web technology information exposed | May help identify software requiring security review | Medium |
| 2 | Server IP address identifiable | Provides information about web infrastructure | Low |
| 3 | HTTP technical information exposed | May assist further enumeration | Low |
| 4 | WAF technology identifiable | Reveals security architecture information | Low |
| 5 | Multiple live hosts visible on local network | Unknown devices may be present | Medium |

## 6. Recommendations

1. Review publicly exposed technology and CMS information.
2. Keep WordPress, plugins, libraries, and other software updated.
3. Review HTTP response headers.
4. Review DNS records regularly.
5. Keep the WAF enabled, configured, and monitored.
6. Perform network discovery only on authorized networks.
7. Investigate unknown devices.
8. Maintain accurate network topology documentation.
9. Perform all testing within an authorized scope.

## 7. Conclusion

During Week 2 of my Cybersecurity and Ethical Hacking internship, I completed practical activities covering footprinting, reconnaissance, and network scanning.

I used Kali Linux tools to collect publicly available information about `networkwalks.com`. I also used Zenmap to scan my own local subnet and identify six active hosts.

These exercises showed that information gathering is an important part of cybersecurity. They also demonstrated the importance of documenting commands, observations, screenshots, risks, and recommendations clearly.

## 8. Evidence Collected

The screenshots are stored in the `screenshots/` folder:

1. WHOIS output
2. WhatWeb output
3. Nslookup output
4. Curl HTTP headers
5. Wafw00f result
6. Zenmap scan results
7. Zenmap topology

## Repository Structure

```text
networkwalks-week2-repository/
├── README.md
└── screenshots/
    ├── 1_whois.png
    ├── 2_whatweb.png
    ├── 3_nslookup.png
    ├── 4_curl.png
    ├── 5_wafw00f.png
    ├── 6_zenmap_scan.png
    └── 7_zenmap_topology.png
```

-End-
