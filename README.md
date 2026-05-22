# IT/OT Cybersecurity Lab – Network Segmentation & Secure Architecture

> Designed at Lamar University's Center for Data, AI and Cybersecurity (CDAC) as part of federally-funded cybersecurity research infrastructure.  
> **Author:** Hossain Md Niaze Motaher | CompTIA Security+ | ISO/IEC 27001 Lead Implementer

---

## Overview

This lab demonstrates a production-inspired IT/OT network segmentation architecture separating enterprise IT systems from Operational Technology (OT) environments — modeled on real-world industrial and engineering network requirements.

The design draws directly from 13+ years of enterprise infrastructure experience, including 10+ years supporting Samsung R&D environments with 700+ users, 3,000+ assets, and 30+ production servers.

**Core objective:** Simulate a secure, audit-ready environment where IT and OT systems are isolated by default, with controlled, policy-enforced communication pathways and full logging visibility.

---

## Architecture

![IT/OT Segmented Network Architecture](./architecture-diagram-v2.jpg)

*Figure: VLAN-segmented IT/OT architecture with FortiGate firewall enforcement, controlled inter-zone communication, and isolated research testbed*

### Zone Structure (Purdue Model-Aligned)

| Zone | Description |
|---|---|
| **Enterprise Zone (IT)** | User workstations, enterprise applications, internet-facing services |
| **DMZ** | Controlled buffer between IT and OT; proxy and logging services |
| **Operations Zone (OT)** | Simulated industrial/lab devices, PLCs, engineering systems |
| **Admin Zone** | Privileged management access — FortiGate, switches, monitoring |
| **Research Testbed** | Fully isolated environment for security testing and simulation |

---

## VLAN Design

| VLAN ID | Name | Subnet | Purpose |
|---|---|---|---|
| 10 | IT-Users | 192.168.10.0/24 | End-user systems and enterprise access |
| 20 | OT-Systems | 192.168.20.0/24 | Industrial/lab devices (isolated) |
| 30 | Servers | 192.168.30.0/24 | Application, file, and system servers |
| 40 | Admin-Mgmt | 192.168.40.0/24 | Network management, privileged access |
| 50 | Testbed | 192.168.50.0/24 | Research and isolated security testing |

---

## Firewall Policy Matrix (FortiGate)

| Source Zone | Destination Zone | Policy | Notes |
|---|---|---|---|
| IT-Users | Internet | ALLOW | With logging, URL filtering |
| IT-Users | OT-Systems | RESTRICT | Specific ports only (authorized services) |
| OT-Systems | IT-Users | DENY | Default block; no unsolicited OT→IT traffic |
| OT-Systems | Internet | DENY | Air-gap principle for OT |
| Admin-Mgmt | All VLANs | ALLOW | MFA-enforced, full audit logging |
| Testbed | All Production | DENY | Fully isolated — no production exposure |
| Any | Any (unmatched) | DENY | Implicit deny-all |

---

## Security Design Principles

- **Defense-in-Depth** — layered controls at network, VLAN, and firewall policy levels
- **Least Privilege** — inter-zone traffic blocked by default; explicit allow rules only
- **Zero Trust Posture** — no implicit trust between zones, including IT↔OT
- **Audit Readiness** — all firewall policies log to centralized syslog; aligned with ISO/IEC 27001 controls A.13 (Network Security) and A.12.4 (Logging)
- **Reduced Attack Surface** — OT systems have no internet path; lateral movement is structurally prevented

---

## Technologies Used

| Category | Technology |
|---|---|
| Firewall / UTM | FortiGate (FortiOS) |
| Switching | FortiSwitch (VLAN trunk/access port config) |
| Proxy / Filtering | FortiProxy |
| Segmentation | 802.1Q VLAN tagging |
| Monitoring | Syslog, FortiGate traffic logs |
| Virtualization | VMware / Hyper-V (lab environment) |

---

## Compliance Alignment

This design maps to the following frameworks:

- **ISO/IEC 27001:2013** — A.13.1 (Network Controls), A.12.4 (Logging), A.9.4 (Access Control)
- **NIST SP 800-82** — Guide to ICS/OT Security (network segmentation recommendations)
- **Purdue Model** — Enterprise, DMZ, and Operations zone separation
- **CIS Controls v8** — Control 12 (Network Infrastructure Management), Control 13 (Network Monitoring)

---

## Key Outcomes

- Designed a segmented IT/OT architecture aligned with NIST, ISO 27001, and Purdue Model principles
- Applied firewall-enforced zone isolation to structurally prevent lateral movement between IT and OT
- Demonstrated audit-ready logging and access control aligned with enterprise compliance requirements
- Built a foundation extensible to SIEM integration, IDS/IPS deployment, and Zero Trust Network Access (ZTNA)
- Applied lessons from 13+ years of enterprise infrastructure experience (Samsung R&D, 700+ users, 3,000+ assets)

---

## Future Enhancements

- [ ] SIEM integration (Wazuh or Splunk) for centralized log correlation
- [ ] IDS/IPS deployment (Snort / Suricata) at DMZ boundary
- [ ] FortiGate HA (High Availability) failover configuration
- [ ] Zero Trust Network Access (ZTNA) policy layer
- [ ] Automated compliance reporting against ISO 27001 controls

---

## Related Work

This lab is part of ongoing cybersecurity research and infrastructure development at:

**CDAC — Center for Data, AI and Cybersecurity**  
Lamar University, Beaumont, TX  
Funded under DOE Grant No. DE CR-0000037

---

## Author

**Hossain Md Niaze Motaher**  
IT Infrastructure & Security Engineer  
CompTIA Security+ | ISO/IEC 27001 Lead Implementer  
MEng Industrial & Systems Engineering — Lamar University  

📧 tanoy021@gmail.com  
🔗 [LinkedIn](https://www.linkedin.com/in/niaze-motaher/)
