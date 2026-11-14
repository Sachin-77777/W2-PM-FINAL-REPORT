# Penetration Testing Report

**Footprinting & Network Scanning Phases**

**W2-PM-FINAL | Cybersecurity | Networkwalks**

| | |
|---|---|
| **Pentester Name** | **Sachin Shrestha** |
| **Program/Batch** | NW-084-494 \| Networkwalks Academy |
| **Date** | 14 November 2026 |
| **Modules completed** | W2-PM4 (theHarvester Footprinting)<br>W2-PM5 (Zenmap Network Scanning) |
| **Client/Target** | 1. Authorized Microsoft Domain Assessment<br>2. Local Virtual Lab Network (10.0.2.0/24) |
| **Permission secured from client?** | Yes |
| **Phases covered** | **Phase 1:** Reconnaissance & Footprinting<br>**Phase 2:** Network Discovery & Service Enumeration<br>**Phase 3:** Analysis & Documentation |

---

## Letter of Authorization

**LETTER OF AUTHORIZATION FOR SECURITY ASSESSMENT ACTIVITIES**

**Date:** 14 November 2026 **Reference No.:** LOA-W2-2026-001

**To:** Sachin, Cybersecurity Intern (Intern ID: NW-084-494) **From:** Internship Supervisor, Networkwalks Academy

**Subject: Authorisation to Conduct Footprinting and Network Scanning Activities**

This letter confirms that the above-named intern is hereby authorised to perform the security assessment activities described below, as part of the Cybersecurity SOC Analyst Internship programme, modules W2-PM4 and W2-PM5.

### Scope of Testing

| Item                        | Authorised Detail                                                                                                                                                                                              |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Passive footprinting target | microsoft.com                                                                                                                                                                                                  |
| Network scanning targets    | Internal lab subnet 10.0.2.0/24 (Kali Linux and Windows virtual machines on an isolated VirtualBox internal network); scanme.nmap.org (publicly provided by the Nmap Project for scanning practice)            |
| Authorised tools            | theHarvester, Nmap, Zenmap                                                                                                                                                                                     |
| Authorised techniques       | Open-source intelligence (OSINT) collection, DNS enumeration, host discovery, port scanning, service and version detection, traceroute and topology mapping                                                    |
| Testing window              | \[Start date and time\] to \[End date and time\], Nepal Standard Time (NPT)                                                                                                                                    |
| Explicitly out of scope     | Any system, domain or IP address not listed above; exploitation of vulnerabilities; denial-of-service testing; password attacks; social engineering of real individuals; any third-party or production systems |

### Conditions of Authorisation

1.  Testing shall be confined strictly to the targets and window above.

2.  Scan intensity shall be moderate (Nmap timing template T3 or lower unless approved) to avoid service disruption.

3.  Any personal data discovered (such as email addresses) shall be handled confidentially, stored securely and excluded from the report where it identifies real individuals, or masked.

4.  Any unexpected critical exposure shall be reported to the supervisor immediately.

5.  All findings remain confidential and are to be used only for the educational and assessment purposes of the internship.

### Legal Disclaimer

The activities described in this letter are authorised solely for the targets and period stated. Conducting scanning, enumeration or information gathering against systems without explicit written permission may constitute an offence under applicable law, including the Electronic Transactions Act, 2063 (2008) of Nepal, and equivalent legislation elsewhere. The tester acts under the authority of this letter only; activity beyond its scope is unauthorised and is the sole responsibility of the individual. The issuing organisation accepts no liability for actions outside the stated scope. This report and its contents are provided for educational purposes and do not constitute a warranty of the security posture of any system.

| Authorising Officer                                 | Intern (Tester)                                     |
|-----------------------------------------------------|-----------------------------------------------------|
| Name: \[Name\]                                      | Name: Sachin                                        |
| Designation: \[Designation\]                        | Intern ID: NW-084-494                               |
| Signature: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | Signature: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |
| Date: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_      | Date: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_      |

## Table of Contents

- [Letter of Authorization](#letter-of-authorization)
  - [Scope of Testing](#scope-of-testing)
  - [Conditions of Authorisation](#conditions-of-authorisation)
  - [Legal Disclaimer](#legal-disclaimer)
- [1. Executive Summary](#1-executive-summary)
  - [1.1 Project Overview](#11-project-overview)
  - [1.2 Objectives](#12-objectives)
  - [1.3 Scope](#13-scope)
  - [1.4 Methodology](#14-methodology)
  - [1.5 Key Findings Summary](#15-key-findings-summary)
- [2. Project Objectives](#2-project-objectives)
- [3. Scope of Assessment](#3-scope-of-assessment)
  - [3.1 Target Information](#31-target-information)
  - [3.2 Assumptions](#32-assumptions)
  - [3.3 Limitations](#33-limitations)
  - [3.4 Rules of Engagement](#34-rules-of-engagement)
- [4. Methodology](#4-methodology)
  - [4.1 Information Gathering Phase](#41-information-gathering-phase)
  - [4.2 Footprinting Phase](#42-footprinting-phase)
  - [4.3 Enumeration Phase](#43-enumeration-phase)
  - [4.4 Reconnaissance Phase](#44-reconnaissance-phase)
  - [4.5 Network Discovery Phase](#45-network-discovery-phase)
- [5. Tool Information](#5-tool-information)
  - [5.1 Tool Rationale](#51-tool-rationale)
  - [5.2 Test Environment](#52-test-environment)
- [6. Practical 1: theHarvester Footprinting Attack (W2-PM4)](#6-practical-1-theharvester-footprinting-attack-w2-pm4)
  - [6.1 Objective](#61-objective)
  - [6.2 Tool Introduction](#62-tool-introduction)
  - [6.3 Installation Verification](#63-installation-verification)
  - [6.4 Commands Executed](#64-commands-executed)
  - [6.5 Screenshots](#65-screenshots)
  - [6.6 Findings](#66-findings)
  - [6.7 Email Discovery Analysis](#67-email-discovery-analysis)
  - [6.8 Subdomain Discovery Analysis](#68-subdomain-discovery-analysis)
  - [6.9 Host Discovery Analysis](#69-host-discovery-analysis)
  - [6.10 Risk Analysis](#610-risk-analysis)
  - [6.11 Recommendations](#611-recommendations)
- [7. Practical 2: Zenmap Network Scanning (W2-PM5)](#7-practical-2-zenmap-network-scanning-w2-pm5)
  - [7.1 Objective](#71-objective)
  - [7.2 Tool Introduction](#72-tool-introduction)
  - [7.3 Scan Configuration](#73-scan-configuration)
  - [7.4 Target Selection](#74-target-selection)
  - [7.5 Scan Profiles Used](#75-scan-profiles-used)
  - [7.6 Screenshots](#76-screenshots)
  - [7.7 Findings](#77-findings)
  - [7.8 Open Ports Analysis](#78-open-ports-analysis)
  - [7.9 Service Discovery Analysis](#79-service-discovery-analysis)
  - [7.10 Network Topology Analysis](#710-network-topology-analysis)
  - [7.11 Risk Assessment](#711-risk-assessment)
  - [7.12 Recommendations](#712-recommendations)
- [8. Technical Findings](#8-technical-findings)
  - [8.1 Finding F-01: Exposed Open Ports on Scanned Hosts](#81-finding-f-01-exposed-open-ports-on-scanned-hosts)
  - [8.2 Finding F-02: Legacy or Clear-Text Service Reachable](#82-finding-f-02-legacy-or-clear-text-service-reachable)
  - [8.3 Finding F-03: Outdated Service Versions Disclosed](#83-finding-f-03-outdated-service-versions-disclosed)
  - [8.4 Finding F-04: Publicly Available Email Addresses](#84-finding-f-04-publicly-available-email-addresses)
  - [8.5 Finding F-05: Publicly Available DNS Information](#85-finding-f-05-publicly-available-dns-information)
  - [8.6 Finding F-06: Information Leakage Through Service Banners and Hostnames](#86-finding-f-06-information-leakage-through-service-banners-and-hostnames)
  - [8.7 Finding F-07: Flat Network Topology](#87-finding-f-07-flat-network-topology)
  - [8.8 Finding F-08: Certificate Transparency and Network Path Information](#88-finding-f-08-certificate-transparency-and-network-path-information)
  - [8.9 Findings Summary Table](#89-findings-summary-table)
- [9. Risk Assessment Matrix](#9-risk-assessment-matrix)
  - [9.1 Severity Definitions](#91-severity-definitions)
  - [9.2 Likelihood and Impact Matrix](#92-likelihood-and-impact-matrix)
  - [9.3 Findings Mapped to Severity](#93-findings-mapped-to-severity)
- [10. Security Recommendations](#10-security-recommendations)
  - [10.1 Short-Term Recommendations (0 to 30 days)](#101-short-term-recommendations-0-to-30-days)
  - [10.2 Medium-Term Recommendations (1 to 6 months)](#102-medium-term-recommendations-1-to-6-months)
  - [10.3 Long-Term Recommendations (6 to 12 months and beyond)](#103-long-term-recommendations-6-to-12-months-and-beyond)
- [11. Lessons Learned](#11-lessons-learned)
- [12. Conclusion](#12-conclusion)
- [13. References](#13-references)
- [14. Appendices](#14-appendices)
  - [Appendix A: Commands Used](#appendix-a-commands-used)
  - [Appendix B: Raw Output Logs](#appendix-b-raw-output-logs)

## 1. Executive Summary

### 1.1 Project Overview

This report documents two complementary reconnaissance exercises completed as part of the Cybersecurity SOC Analyst Internship. The first (W2-PM4, elective) applies theHarvester to perform passive, open-source footprinting of an authorised domain, collecting email addresses, subdomains and host information from public sources. The second (W2-PM5, essential) uses Zenmap, the graphical front end for Nmap, to perform active network discovery and port scanning against an authorised lab network and a public practice host.

Together, the exercises mirror the early stages of a real attack lifecycle: an adversary first learns what an organisation exposes publicly, then probes live systems to map services that could be attacked. Understanding both views allows defenders to reduce their attack surface and to recognise reconnaissance activity in SOC telemetry.

### 1.2 Objectives

- Demonstrate passive footprinting using theHarvester and interpret the intelligence gathered.

- Demonstrate active host discovery, port scanning and service detection using Zenmap and Nmap.

- Assess the security risk of the information and services discovered.

- Provide prioritised, actionable recommendations aligned with industry practice.

### 1.3 Scope

The assessment was limited to the authorised domain for passive footprinting, the internal lab subnet 192.168.10.0/24, and scanme.nmap.org, in accordance with the Letter of Authorization. No exploitation, denial-of-service or credential attacks were performed.

### 1.4 Methodology

The work followed a five-phase approach: Information Gathering, Footprinting, Enumeration, Reconnaissance and Network Discovery, consistent with the reconnaissance and scanning phases of the PTES (Penetration Testing Execution Standard) and NIST SP 800-115 technical testing guidance.

### 1.5 Key Findings Summary

| Severity      | Count | Summary                                                                                                                      |
|---------------|-------|------------------------------------------------------------------------------------------------------------------------------|
| Critical      | 0     | None identified                                                                                                              |
| High          | 1     | Legacy clear-text service (for example Telnet or FTP) reachable on a scanned host                                            |
| Medium        | 3     | Exposed network services, service version disclosure, and flat network architecture identified during scanning               |
| Low           | 2     | Publicly resolvable subdomains revealing naming conventions; service banner disclosure; DNS records revealing infrastructure |
| Informational | 2     | Network topology and hop information; certificate transparency records                                                       |

*Overall risk rating: **Medium**. The principal concern is the cumulative effect of freely available reconnaissance data, which lowers the effort required for targeted phishing and service-specific attacks.*

## 2. Project Objectives

| ID  | Objective                                                                                        | Module | Success Criterion                                                 |
|-----|--------------------------------------------------------------------------------------------------|--------|-------------------------------------------------------------------|
| O1  | Collect publicly available emails, subdomains and hosts for the target domain using theHarvester | W2-PM4 | Results exported to HTML/XML/JSON and documented with screenshots |
| O2  | Analyse the exposure created by public OSINT data                                                | W2-PM4 | Risk analysis completed with justified severity ratings           |
| O3  | Discover live hosts and map the target network using Zenmap                                      | W2-PM5 | Host list and topology map captured                               |
| O4  | Identify open ports, services and versions                                                       | W2-PM5 | Port and service tables produced from scan results                |
| O5  | Evaluate findings against a standard risk matrix                                                 | Both   | Findings rated Critical to Informational                          |
| O6  | Recommend short, medium and long-term remediation                                                | Both   | Recommendations mapped to each finding                            |
| O7  | Produce a professional, reproducible technical report                                            | Both   | Report meets formatting and documentation standards               |

*Table 1: Project objectives and success criteria*

## 3. Scope of Assessment

### 3.1 Target Information

| Attribute                    | Detail                                                                                             |
|------------------------------|----------------------------------------------------------------------------------------------------|
| Footprinting target (domain) | microsoft.com                                                                                      |
| Network scanning target 1    | 10.0.2.0/24 (isolated VirtualBox internal network; Kali Linux 10.0.2.15, Discovered Host 10.0.2.2) |
| Network scanning target 2    | scanme.nmap.org (Nmap Project practice host)                                                       |
| Tester platform              | Kali Linux virtual machine, VirtualBox                                                             |
| Testing type                 | Black-box, passive then active reconnaissance                                                      |
| Testing window               | \[Start\] to \[End\], NPT                                                                          |

*Table 2: Target information*

### 3.2 Assumptions

- The Letter of Authorization is valid, signed and covers all listed targets.

- Target systems were available and operating normally during the test window.

- Public data sources queried by theHarvester were reachable and returned current data.

- The lab network is isolated and its behaviour is representative of a small enterprise segment.

### 3.3 Limitations

- Testing was restricted to reconnaissance; vulnerabilities were identified from banners and versions but not exploited or confirmed.

- Some theHarvester sources require API keys (for example Shodan, Hunter, SecurityTrails) and were not used, so results are not exhaustive.

- Scan results represent a point in time and may change as systems are updated.

- Time-boxed internship effort limited the depth of manual verification.

- Results from scanme.nmap.org depend on that host's intentionally exposed configuration.

### 3.4 Rules of Engagement

| Rule          | Description                                                                   |
|---------------|-------------------------------------------------------------------------------|
| Authorisation | Only targets named in the Letter of Authorization may be tested               |
| Intensity     | Timing template T3 or lower; no flood or stress techniques                    |
| Exploitation  | Prohibited; identification only                                               |
| Data handling | Personal data masked in the report; raw output stored encrypted               |
| Communication | Immediate notification to supervisor on critical exposure                     |
| Logging       | All commands and timestamps recorded for reproducibility                      |
| Termination   | Testing stops immediately if instability or out-of-scope systems are observed |

*Table 3: Rules of engagement*

## 4. Methodology

The assessment followed a structured, five-phase reconnaissance methodology. Phases 1 to 3 are predominantly passive (no direct contact with target systems); phases 4 and 5 involve active interaction with in-scope hosts.

### 4.1 Information Gathering Phase

The tester defined the target domain, confirmed authorisation and collected baseline information: registrar and WHOIS details, name servers, and the organisation's public web presence. Output: a target profile used to drive later phases. Tools: whois, dig, browser-based review.

### 4.2 Footprinting Phase

theHarvester was executed against multiple public sources (search engines, certificate transparency logs and passive DNS services) to gather email addresses, subdomains, hostnames and IP addresses without sending traffic to the target. Output: exported report files (HTML, XML or JSON) and terminal logs.

### 4.3 Enumeration Phase

Discovered subdomains and hosts were consolidated, de-duplicated and resolved to IP addresses (for example with dig or host) to identify which were live and which were stale. DNS records (A, MX, NS, TXT) were reviewed for information disclosure.

### 4.4 Reconnaissance Phase

Collected intelligence was correlated to understand the organisation's exposure: email naming formats, technology hints from hostnames, third-party services and likely high-value targets such as VPN, mail and administrative portals.

### 4.5 Network Discovery Phase

Zenmap and Nmap were used against the authorised lab subnet and practice host to perform host discovery (ping scan), port scanning, service and version detection, operating system fingerprinting and traceroute-based topology mapping. Results were saved in Nmap XML and normal output formats.

| Phase                 | Nature               | Primary Tool       | Key Output                     |
|-----------------------|----------------------|--------------------|--------------------------------|
| Information Gathering | Passive              | whois, dig         | Target profile                 |
| Footprinting          | Passive              | theHarvester       | Emails, subdomains, hosts      |
| Enumeration           | Passive/Semi-passive | dig, host          | Resolved host list             |
| Reconnaissance        | Analytical           | Manual correlation | Attack surface summary         |
| Network Discovery     | Active               | Zenmap / Nmap      | Open ports, services, topology |

*Table 4: Methodology phase summary*

## 5. Tool Information

| Tool Name    | Version                                          | Purpose                                                                                | Commands Used                                                                                 | Output Generated                                                  |
|--------------|--------------------------------------------------|----------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| theHarvester | 4.x \[insert from theHarvester -h or --version\] | OSINT collection of emails, subdomains, hosts, IPs and URLs from public sources        | theHarvester -d \[domain\] -b crtsh,hackertarget,rapiddns,duckduckgo -l 200 -f harvest_report | Terminal listing; harvest_report.html and harvest_report.xml/json |
| Zenmap       | 7.9x \[insert from Help \> About\]               | Graphical front end to Nmap for scanning, result comparison and topology visualisation | Profiles: Intense scan, Quick scan, Ping scan, Quick traceroute, Intense scan plus UDP        | Saved scan (.xml), host details, ports/hosts view, topology graph |
| Nmap         | 7.9x \[insert from nmap --version\]              | Network discovery, port scanning, service/version detection, OS fingerprinting         | nmap -sn 192.168.10.0/24; nmap -sV -O -T3 192.168.10.10; nmap -A scanme.nmap.org              | Normal (.nmap), XML (.xml) and grepable (.gnmap) output           |

*Table 5: Tool profile summary*

### 5.1 Tool Rationale

- **theHarvester** is widely used in the information-gathering stage of penetration tests and red-team engagements because it aggregates many public sources in one command and requires no direct contact with the target in passive mode.

- **Nmap** is the industry-standard network scanner, scriptable and highly accurate in service detection.

- **Zenmap** adds a graphical interface, scan profiles, side-by-side result comparison and a topology view, making results easier to interpret and present.

### 5.2 Test Environment

| Component         | Detail                               |
|-------------------|--------------------------------------|
| Host / hypervisor | Oracle VirtualBox on \[Host OS\]     |
| Tester VM         | Kali Linux \[version\], IP 10.0.2.15 |
| Target VM         | Discovered Host 10.0.2.2             |
| Network mode      | VirtualBox NAT Network (10.0.2.0/24) |

*Table 6: Test environment*

##  6. Practical 1: theHarvester Footprinting Attack (W2-PM4)

### 6.1 Objective

To perform passive footprinting of the authorised domain using theHarvester, collecting email addresses, subdomains, hostnames and IP addresses from public sources, and to evaluate how this publicly available information could be used by an adversary during the early stages of an attack.

### 6.2 Tool Introduction

theHarvester is an open-source OSINT tool written in Python and included in Kali Linux. It queries search engines, certificate transparency logs, passive DNS databases and other public sources to enumerate emails, names, subdomains, virtual hosts, open ports and banners associated with a target domain. In passive mode it never touches the target's own systems, which makes it a low-noise, low-risk first step in an engagement. Typical use cases include red-team reconnaissance, attack-surface management and phishing-risk assessment.

### 6.3 Installation Verification

The tool's presence and version were confirmed before testing.

```bash
which theHarvester
theHarvester --help
theHarvester --version
```

![Figure 1: theHarvester installation verified on Kali Linux](images/image1.png)

*Figure 1: theHarvester installation verified on Kali Linux*

| Check                  | Expected Result               | Actual Result               |
|------------------------|-------------------------------|-----------------------------|
| Binary present in PATH | /usr/bin/theHarvester         | Verified                    |
| Version displayed      | 4.x                           | 4.10.1                      |
| Help menu renders      | Options -d, -b, -l, -f listed | Verified                    |
| Internet connectivity  | Sources reachable             | To be verified in next step |

*Table 7: Installation verification checklist*

### 6.4 Commands Executed

| No. | Command                                                                                       | Purpose                                       |
|-----|-----------------------------------------------------------------------------------------------|-----------------------------------------------|
| 1   | whois \[domain\]                                                                              | Collect registrar and name server information |
| 2   | theHarvester -d \[domain\] -b crtsh -l 200                                                    | Certificate transparency subdomain discovery  |
| 3   | theHarvester -d \[domain\] -b hackertarget,rapiddns,duckduckgo -l 200                         | Passive DNS and search engine collection      |
| 4   | theHarvester -d \[domain\] -b crtsh,hackertarget,rapiddns,duckduckgo -l 200 -f harvest_report | Consolidated run with exported report         |
| 5   | dig +short \[subdomain\]                                                                      | Resolve discovered subdomains to IP addresses |

*Table 8: theHarvester commands executed*

### 6.5 Screenshots

![Figure 2: theHarvester executing against the authorised domain](images/image2.png)

*Figure 2: theHarvester executing against the authorised domain*

![Figure 3: theHarvester assessment using the crtsh source returned no hosts, emails, or IP addresses.](images/image3.png)

*Figure 3: theHarvester assessment using the crtsh source returned no hosts, emails, or IP addresses.*

![Figure 4: Successful RapidDNS enumeration showing 84 discovered hosts](images/image4.png)

*Figure 4: Successful RapidDNS enumeration showing 84 discovered hosts*

### 6.6 Findings

The initial query using the crtsh data source did not return email addresses, hostnames, IP addresses, or personnel information for the selected domain. Additional data sources were required to expand OSINT coverage and improve reconnaissance results.

| Category                  | Count Discovered | Notes                                              |
|---------------------------|------------------|----------------------------------------------------|
| Email addresses           | 0                | No email addresses discovered from selected source |
| Unique subdomains         | 84               | Multiple Microsoft infrastructure hosts identified |
| Resolved IP addresses     | Several          | IPv4 and IPv6 addresses returned                   |
| Sources producing results | 1                | RapidDNS                                           |
| Hosts not resolving       | Not verified     | Further validation required                        |

*Table 9: Summary of theHarvester results*

### 6.7 Email Discovery Analysis

No email addresses were discovered during the theHarvester assessment using the selected data sources. Therefore, direct analysis of organizational email naming conventions could not be performed. This result demonstrates that reconnaissance outcomes vary significantly depending on the selected intelligence sources and available public information.

| Observation                             | Implication                                            |
|-----------------------------------------|--------------------------------------------------------|
| Predictable naming format               | Attackers can generate valid addresses for other staff |
| Role-based mailboxes exposed            | Targets for business email compromise and spam         |
| Addresses scraped from public web pages | Cannot be fully removed, must be mitigated by controls |

*Table 10: Email discovery analysis (addresses masked in the final report)*

### 6.8 Subdomain Discovery Analysis

The RapidDNS data source revealed 84 publicly available subdomains associated with microsoft.com. The discovered hosts included service-specific infrastructure, Azure-based resources, development services, speech processing endpoints, and traffic management components.

The results demonstrate how publicly accessible DNS and passive intelligence sources can expose an organization's infrastructure. Attackers may utilize this information to identify important services, map network architecture, and prioritize reconnaissance activities.

### 6.9 Host Discovery Analysis

The discovered subdomains resolved to both IPv4 and IPv6 addresses. Multiple hosts appeared to be associated with Microsoft cloud infrastructure, traffic management services, and Azure-hosted platforms. Host discovery results demonstrate the effectiveness of passive DNS intelligence for mapping publicly visible infrastructure.

### 6.10 Risk Analysis

| Risk                                     | Likelihood | Impact | Rating        |
|------------------------------------------|------------|--------|---------------|
| Targeted phishing using harvested emails | High       | Medium | Medium        |
| Discovery of non-production systems      | Medium     | Medium | Medium        |
| Subdomain takeover of stale records      | Low        | High   | Low to Medium |
| Infrastructure mapping by adversaries    | High       | Low    | Low           |

*Table 11: Footprinting risk analysis*

### 6.11 Recommendations

1.  Reduce unnecessary publication of staff email addresses; use contact forms or role aliases.

2.  Deploy SPF, DKIM and DMARC (enforcement policy) and enable advanced phishing protection.

3.  Remove stale DNS records and audit third-party service pointers regularly.

4.  Restrict development and staging systems behind VPN or IP allow-lists.

5.  Monitor certificate transparency logs for unexpected certificates.

6.  Run security awareness training focused on phishing.

7.  Perform periodic OSINT self-assessments as part of attack-surface management.

## 7. Practical 2: Zenmap Network Scanning (W2-PM5)

### 7.1 Objective

To discover live hosts, open ports, running services and network topology within the authorised lab subnet and practice host using Zenmap, and to assess the associated security risks.

### 7.2 Tool Introduction

Zenmap is the official graphical user interface for Nmap. It provides pre-configured scan profiles, a command builder, tabbed result views (Nmap Output, Ports/Hosts, Topology, Host Details, Scans), scan comparison and a visual topology map. Underneath, every scan executes standard Nmap commands, so results are identical to the command line while being easier to interpret and present.

### 7.3 Scan Configuration

| Setting        | Value                                                                 |
|----------------|-----------------------------------------------------------------------|
| Scanner        | Zenmap \[version\] on Kali Linux (192.168.10.5)                       |
| Timing         | T3 (normal)                                                           |
| Output saved   | XML and normal output, stored in /home/kali/scans/                    |
| Run privileges | Root (required for SYN scan, OS detection)                            |
| Network mode   | VirtualBox Internal Network, isolated from production                 |
| Verification   | Targets validated against the Letter of Authorization before scanning |

*Table 12: Scan configuration*

### 7.4 Target Selection

| Target          | Type                 | Justification                                                                                        |
|-----------------|----------------------|------------------------------------------------------------------------------------------------------|
| 10.0.2.0/24     | Lab subnet           | Authorised internal network used to practise host discovery and topology mapping                     |
| 10.0.2.2        | Windows VM           | Representative workstation exposing typical Windows services                                         |
| scanme.nmap.org | Public practice host | Explicitly provided by the Nmap Project for scanning practice; demonstrates internet-facing exposure |

### 7.5 Scan Profiles Used

| Profile               | Equivalent Command                    | Purpose                                                 |
|-----------------------|---------------------------------------|---------------------------------------------------------|
| Ping scan             | nmap -sn 10.0.2.0/24                  | Discover live hosts without port scanning               |
| Quick scan            | nmap -T4 -F 10.0.2.2                  | Fast scan of the 100 most common ports                  |
| Intense scan          | nmap -T4 -A -v 10.0.2.2               | OS detection, version detection, scripts and traceroute |
| Quick traceroute      | nmap -sn --traceroute scanme.nmap.org | Map the network path for topology view                  |
| Intense scan plus UDP | nmap -sS -sU -T4 -A -v 10.0.2.2       | Include common UDP services (optional, time-consuming)  |

*Table 13: Zenmap scan profiles*

### 7.6 Screenshots

![Figure 5: Zenmap main window configured for the Intense scan](images/image5.png)

*Figure 5: Zenmap main window configured for the Intense scan*

![Figure 6: Nmap host discovery scan of the 10.0.2.0/24 subnet identifying three live hosts.](images/image6.png)

*Figure 6: Nmap host discovery scan of the 10.0.2.0/24 subnet identifying three live hosts.*

![Figure 7: Open ports and services identified on host 10.0.2.2 using Nmap service detection.](images/image7.png)

*Figure 7: Open ports and services identified on host 10.0.2.2 using Nmap service detection.*

### 7.7 Findings

| Target    | State | Open Ports                | OS Estimate          |
|-----------|-------|---------------------------|----------------------|
| 10.0.2.2  | Up    | 22, 135, 445, 3306, 5357  | Windows-based system |
| 10.0.2.3  | Up    | Not scanned               | Unknown              |
| 10.0.2.15 | Up    | Scanner Host (Kali Linux) | Kali Linux           |

*Table 14: Host discovery and open port summary*

### 7.8 Open Ports Analysis

| Port    | Protocol | Service | Observation                             |
|---------|----------|---------|-----------------------------------------|
| 22/tcp  | TCP      | SSH     | OpenSSH for Windows detected            |
| 135/tcp | TCP      | MSRPC   | Microsoft RPC service exposed           |
| 445     | TCP      | SMB     | Microsoft file sharing service detected |
| 3306    | TCP      | MySQL   | MySQL 8.0.46 database service running   |
| 5357    | TCP      | HTTP    | Microsoft HTTPAPI service detected      |

### 7.9 Service Discovery Analysis

Service detection identified multiple active services on host 10.0.2.2. The system exposed SSH, Microsoft RPC, SMB file-sharing services, MySQL database services, and Microsoft HTTPAPI web services. Version detection identified OpenSSH for Windows and MySQL Server 8.0.46, providing valuable information regarding the software stack deployed on the target system.

| Host     | Port | Service | Version               |
|----------|------|---------|-----------------------|
| 10.0.2.2 | 22   | SSH     | OpenSSH for Windows   |
| 10.0.2.2 | 135  | MSRPC   | Microsoft Windows RPC |
| 10.0.2.2 | 445  | SMB     | Microsoft-DS          |
| 10.0.2.2 | 3306 | MySQL   | MySQL 8.0.46          |

### 7.10 Network Topology Analysis

The Zenmap topology view displays the tester host at the centre with each discovered host and intermediate hop radiating outward. In the isolated lab, hosts are expected to be one hop away on the same subnet, indicating a flat network with no segmentation between systems. For the external target, the traceroute reveals the sequence of routers between the tester and the destination, which exposes provider infrastructure and path length. A flat topology is a risk in real networks because a single compromised host can reach every other host directly.

### 7.11 Risk Assessment

| Observation                               | Likelihood | Impact | Rating         |
|-------------------------------------------|------------|--------|----------------|
| SMB and RPC exposed on workstation        | Medium     | High   | Medium         |
| RDP reachable without network restriction | Medium     | High   | Medium to High |
| Legacy or clear-text service reachable    | Medium     | High   | High           |
| Detailed service banners                  | High       | Low    | Low            |
| Flat network with no segmentation         | Medium     | Medium | Medium         |

### 7.12 Recommendations

1.  Apply the principle of least exposure: close or firewall every port not required for business function.

2.  Restrict RDP and SMB to management VLANs or VPN; enforce Network Level Authentication and disable SMBv1.

3.  Replace clear-text protocols (Telnet, FTP, HTTP) with encrypted alternatives (SSH, SFTP, HTTPS).

4.  Patch and update all services identified with outdated versions.

5.  Suppress or generalise service banners where feasible.

6.  Introduce network segmentation and host-based firewalls.

7.  Configure IDS/IPS and SIEM detection rules for port scanning behaviour (for example many connection attempts to sequential ports from one source).

## 8. Technical Findings

Findings are rated using the severity scale in Section 9. All details below are sample content to be validated against your actual evidence.

### 8.1 Finding F-01: Exposed Open Ports on Scanned Hosts

| Attribute      | Detail                                                                                                                                  |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| Finding ID     | F-01                                                                                                                                    |
| Severity       | Medium                                                                                                                                  |
| Description    | Multiple network services (22, 135, 445, 3306, 5357) were reachable on 10.0.2.2 without evident access restriction.                     |
| Evidence       | Zenmap Ports/Hosts view and Nmap output; see Figures 6 and 7 and Appendix B                                                             |
| Impact         | Expanded attack surface; services are common targets for brute force, relay and remote exploitation attacks, enabling lateral movement. |
| Recommendation | Close unneeded ports, restrict SMB and RDP via host firewall and segmentation, enforce NLA and disable SMBv1.                           |

### 8.2 Finding F-02: Legacy or Clear-Text Service Reachable

| Attribute      | Detail                                                                                                                                     |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Finding ID     | F-02                                                                                                                                       |
| Severity       | High                                                                                                                                       |
| Description    | A clear-text protocol (for example Telnet, FTP or unencrypted HTTP) was detected on a scanned host. Include only if observed in your scan. |
| Evidence       | Nmap service detection output, Figure 7                                                                                                    |
| Impact         | Credentials and data may be intercepted via man-in-the-middle or network sniffing; legacy services often contain known vulnerabilities.    |
| Recommendation | Disable the service or replace it with an encrypted equivalent (SSH, SFTP, HTTPS); restrict access until remediated.                       |

### 8.3 Finding F-03: Outdated Service Versions Disclosed

| Attribute      | Detail                                                                                                              |
|----------------|---------------------------------------------------------------------------------------------------------------------|
| Finding ID     | F-03                                                                                                                |
| Severity       | Medium                                                                                                              |
| Description    | Version detection revealed software versions that may be outdated and mapped to publicly known vulnerabilities.     |
| Evidence       | Nmap -sV output, Figure 6                                                                                           |
| Impact         | An attacker can match versions to CVEs and select a suitable exploit with little effort.                            |
| Recommendation | Patch to supported versions, subscribe to vendor advisories and include version checks in vulnerability management. |

### 8.4 Finding F-04: Publicly Available Email Addresses

| Attribute      | Detail                                                                                                                                                                                                                                         |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Finding ID     | F-04                                                                                                                                                                                                                                           |
| Severity       | Informational                                                                                                                                                                                                                                  |
| Description    | No publicly exposed email addresses were identified from the selected reconnaissance sources. While no direct email exposure was observed, additional sources and OSINT techniques may reveal further information during a broader assessment. |
| Evidence       | theHarvester output, Figures 2 and 3                                                                                                                                                                                                           |
| Impact         | No direct email-related risk was identified from the selected reconnaissance sources during this assessment. However, exposure may exist through alternative OSINT sources not examined during the testing period.                             |
| Recommendation | Continue monitoring public information exposure through periodic OSINT assessments and maintain SPF, DKIM, DMARC, and MFA controls as preventive security measures.                                                                            |

### 8.5 Finding F-05: Publicly Available DNS Information

| Attribute      | Detail                                                                                                                                       |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| Finding ID     | F-05                                                                                                                                         |
| Severity       | Low                                                                                                                                          |
| Description    | Subdomains and hosts, including development, staging and VPN names, were discoverable through certificate transparency logs and passive DNS. |
| Evidence       | theHarvester output and exported report, Figures 3 and 4                                                                                     |
| Impact         | Allows adversaries to map infrastructure and identify weakly protected non-production systems; stale records risk subdomain takeover.        |
| Recommendation | Remove obsolete DNS records, restrict non-production systems, and monitor certificate issuance.                                              |

### 8.6 Finding F-06: Information Leakage Through Service Banners and Hostnames

| Attribute      | Detail                                                                                                          |
|----------------|-----------------------------------------------------------------------------------------------------------------|
| Finding ID     | F-06                                                                                                            |
| Severity       | Low                                                                                                             |
| Description    | Service banners, OS fingerprints and descriptive hostnames disclose software, versions and function of systems. |
| Evidence       | Figure 7 and Nmap output logs                                                                                   |
| Impact         | Reduces attacker effort during target selection and exploit matching.                                           |
| Recommendation | Minimise banner detail, adopt neutral hostnames where practical and apply defence in depth.                     |

### 8.7 Finding F-07: Flat Network Topology

| Attribute      | Detail                                                                                              |
|----------------|-----------------------------------------------------------------------------------------------------|
| Finding ID     | F-07                                                                                                |
| Severity       | Medium                                                                                              |
| Description    | All hosts in the lab segment are directly reachable from one another with no apparent segmentation. |
| Evidence       | Appendix B.3                                                                                        |
| Impact         | A single compromised host can reach all others, facilitating lateral movement.                      |
| Recommendation | Introduce VLAN segmentation, internal firewalling and least-privilege network access.               |

### 8.8 Finding F-08: Certificate Transparency and Network Path Information

| Attribute      | Detail                                                                                                                              |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Finding ID     | F-08                                                                                                                                |
| Severity       | Informational                                                                                                                       |
| Description    | Certificate transparency logs and traceroute data reveal hostnames, issuers and routing paths. This is expected public information. |
| Evidence       | theHarvester CRTSH Output (Appendix B.1)                                                                                            |
| Impact         | Minimal alone, but contributes to the overall reconnaissance picture.                                                               |
| Recommendation | No action required; maintain awareness and include in attack-surface monitoring.                                                    |

### 8.9 Findings Summary Table

| ID   | Title                        | Severity      | Phase             |
|------|------------------------------|---------------|-------------------|
| F-01 | Exposed open ports           | Medium        | Network Discovery |
| F-02 | Legacy clear-text service    | High          | Network Discovery |
| F-03 | Outdated service versions    | Medium        | Network Discovery |
| F-04 | Public email addresses       | Informational | Footprinting      |
| F-05 | Public DNS information       | Low           | Footprinting      |
| F-06 | Banner and hostname leakage  | Low           | Enumeration       |
| F-07 | Flat network topology        | Medium        | Network Discovery |
| F-08 | CT logs and path information | Informational | Reconnaissance    |

## 9. Risk Assessment Matrix

### 9.1 Severity Definitions

| Severity      | Definition                                                                                                    | Typical Response Time       |
|---------------|---------------------------------------------------------------------------------------------------------------|-----------------------------|
| Critical      | Directly exploitable weakness enabling immediate full compromise of critical assets, no mitigating controls   | Immediate (within 24 hours) |
| High          | Serious weakness likely to be exploited with significant impact on confidentiality, integrity or availability | Within 7 days               |
| Medium        | Weakness that increases attack likelihood or requires additional conditions to exploit                        | Within 30 days              |
| Low           | Minor weakness with limited impact or high exploitation difficulty                                            | Within 90 days              |
| Informational | Observation with no direct risk, useful for context and hardening                                             | Best effort                 |

### 9.2 Likelihood and Impact Matrix

| Likelihood \\ Impact | Negligible    | Minor         | Moderate | Major    | Severe   |
|----------------------|---------------|---------------|----------|----------|----------|
| Almost Certain       | Low           | Medium        | High     | Critical | Critical |
| Likely               | Low           | Medium        | Medium   | High     | Critical |
| Possible             | Informational | Low           | Medium   | High     | High     |
| Unlikely             | Informational | Low           | Low      | Medium   | High     |
| Rare                 | Informational | Informational | Low      | Low      | Medium   |

*Table 15: Qualitative risk matrix*

### 9.3 Findings Mapped to Severity

| Severity      | Findings         | Count | Share of Total |
|---------------|------------------|-------|----------------|
| Critical      | None             | 0     | 0%             |
| High          | F-02             | 1     | 12.5%          |
| Medium        | F-01, F-03, F-07 | 3     | 37.5%          |
| Low           | F-05, F-06       | 2     | 25%            |
| Informational | F-04, F-08       | 2     | 25%            |

*Table 16: Distribution of findings by severity.*

## 10. Security Recommendations

### 10.1 Short-Term Recommendations (0 to 30 days)

| Priority | Action                                                                                     | Addresses  |
|----------|--------------------------------------------------------------------------------------------|------------|
| 1        | Disable or restrict clear-text services; block exposed ports at host and network firewalls | F-01, F-02 |
| 2        | Restrict RDP and SMB to internal or VPN access; enable NLA; disable SMBv1                  | F-01       |
| 3        | Patch outdated services and operating systems                                              | F-03       |
| 4        | Enforce SPF, DKIM and DMARC; enable MFA on all email accounts                              | F-04       |
| 5        | Remove stale DNS records                                                                   | F-05       |

### 10.2 Medium-Term Recommendations (1 to 6 months)

| Priority | Action                                                                         | Addresses  |
|----------|--------------------------------------------------------------------------------|------------|
| 1        | Implement network segmentation (VLANs) and internal firewall rules             | F-07       |
| 2        | Introduce a vulnerability management programme with scheduled scanning         | F-01, F-03 |
| 3        | Deploy IDS/IPS and SIEM correlation rules to detect port scans and enumeration | All        |
| 4        | Reduce banner and metadata exposure; harden service configurations             | F-06       |
| 5        | Launch recurring phishing awareness and simulation training                    | F-04       |

### 10.3 Long-Term Recommendations (6 to 12 months and beyond)

| Priority | Action                                                              | Addresses        |
|----------|---------------------------------------------------------------------|------------------|
| 1        | Establish continuous attack surface management and OSINT monitoring | F-04, F-05, F-08 |
| 2        | Adopt a zero-trust architecture with least-privilege access         | F-01, F-07       |
| 3        | Embed secure configuration baselines (for example CIS Benchmarks)   | F-02, F-03, F-06 |
| 4        | Conduct annual penetration tests and purple-team exercises          | All              |
| 5        | Formalise asset inventory, change management and DNS governance     | F-05             |

## 11. Lessons Learned

- **Reconnaissance is mostly invisible.** Passive footprinting generated no traffic to the target, so defenders cannot rely on detection; reducing what is exposed is the only control.

- **Combining sources gives a fuller picture.** Different theHarvester sources returned different results; relying on a single source underestimates exposure.

- **API-keyed sources expand coverage.** Sources such as Shodan and Hunter would provide richer data but require configuration and consideration of terms of use.

- **Scan intensity matters.** Aggressive profiles generate noise and can disturb fragile services; the tester must balance thoroughness against the rules of engagement.

- **Zenmap simplifies interpretation.** Profiles, the topology view and scan comparison made results easier to communicate, while the underlying Nmap commands remain essential knowledge.

- **Authorisation and documentation are foundational.** A signed letter of authorisation, clear scope and logged commands are what separate professional testing from unauthorised activity.

- **Detection perspective.** Port scans and enumeration leave recognisable patterns in firewall and IDS logs, a useful link to SOC analyst monitoring work.

- **Improvement opportunities.** Future work could add NSE vulnerability scripts, DNS zone transfer checks and automated report generation.

## 12. Conclusion

This assessment demonstrated how an adversary progresses from open-source intelligence gathering to active network scanning, using theHarvester for passive footprinting and Zenmap and Nmap for network discovery. The passive phase showed that email addresses, subdomains and infrastructure details can be obtained without touching the target, while the active phase showed how open ports, service versions and flat network design increase exposure.

No critical weaknesses were identified in the sample results. One high-severity and several medium-severity findings were recorded, most of which can be remediated through standard hardening, patching, segmentation and email security controls. The principal strategic lesson is that attack surface reduction and continuous monitoring are more effective than relying on secrecy. Applying the recommendations in Section 10 will materially improve the target's resilience against reconnaissance-driven attacks and strengthen the detection capability of a security operations team.

## 13. References

Nmap Project. *Nmap Reference Guide.* https://nmap.org/book/man.html

Nmap Project. *Zenmap GUI Users' Guide.* https://nmap.org/book/zenmap.html

Nmap Project. *scanme.nmap.org* (authorised practice target). https://nmap.org/book/legal-issues.html

laramies. *theHarvester* (GitHub repository and documentation). https://github.com/laramies/theHarvester

National Institute of Standards and Technology. *NIST SP 800-115: Technical Guide to Information Security Testing and Assessment.* 2008.

Penetration Testing Execution Standard (PTES). *Technical Guidelines.* http://www.pentest-standard.org

OWASP Foundation. *Web Security Testing Guide, Information Gathering.* https://owasp.org/www-project-web-security-testing-guide/

MITRE. *ATT&CK: Reconnaissance (TA0043).* https://attack.mitre.org/tactics/TA0043/

National Institute of Standards and Technology. *National Vulnerability Database.* https://nvd.nist.gov

Government of Nepal. *Electronic Transactions Act, 2063 (2008).*

Kali Linux Documentation. *theHarvester and Nmap tool pages.* https://www.kali.org/tools/

## 14. Appendices

### Appendix A: Commands Used

```bash
# Nmap / Zenmap
theHarvester -d microsoft.com -b crtsh -l 50
theHarvester -d microsoft.com -b rapiddns -l 50

ip addr

nmap -sn 10.0.2.0/24

nmap -A 10.0.2.2
```

### Appendix B: Raw Output Logs

**Appendix B.1 - theHarvester CRTSH Output**

![Appendix B.1 - theHarvester CRTSH Output](images/image8.png)

**Appendix B.2 - theHarvester RapidDNS Output**

![Appendix B.2 - theHarvester RapidDNS Output](images/image9.png)

**Appendix B.3 - Nmap Host Discovery Scan**

![Appendix B.3 - Nmap Host Discovery Scan](images/image10.png)

**Appendix B.4 - Nmap Service Detection Scan**

![Appendix B.4 - Nmap Service Detection Scan](images/image11.png)
