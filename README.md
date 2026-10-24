# Money Mitra Network — Task 4 Cyber Security Assessment

**Submitted by:** Sudip Kumar Chaurasiya  
**College:** Model Institute of Technology (MIT)  
**Programme:** Bachelor of Information Technology (BIT)  
**Assessment date:** 24 October 2026

## Project Overview

This project documents a cyber security assessment using an intentionally vulnerable Metasploitable 2 lab and a separate supplied network packet capture.

The work includes service discovery, targeted service checks, packet-capture investigation, file identification and hashing, risk prioritization, detection logic, and incident-response recommendations.

The lab scan and PCAP investigation are separate evidence sets. Their findings are not assumed to describe the same incident.

## Main Findings

- A root bind shell was exposed on TCP/1524 in the intentionally vulnerable lab.
- Anonymous FTP login was accepted on TCP/21; the directory listing was empty.
- Legacy Apache/PHP and database service versions were observed.
- The supplied PCAP showed an executable request and matching HTTP 200 response from an external endpoint.
- The recovered executable was not executed.
- The purpose of a separate long-lived encrypted connection and several HTTP redirects remains unresolved.

These observations do not by themselves confirm malware execution, successful compromise, or data exfiltration.

## Submission Files

- `Money_Mitra_Network_Task4_Final_Report.pdf` — final assessment report.
- `Money_Mitra_Network_Task4_Evidence_Workbook.xlsx` — overview, IOC table, risk register, timeline, detection rules, recommendations, and evidence index.

## Evidence Folder Guide

- `Evidence/Lab-Scans/` — Nmap output, targeted checks, FTP results, HTTP headers, and lab screenshots.
- `Evidence/PCAP-Analysis/` — packet-analysis screenshots, extracted fields, connection summaries, and file verification notes.
- `Evidence/Supporting-Files/` — IOC table, risk register, event timeline, detection rules, and incident-response plan.

## Handling and Limitations

The recovered executable was not executed. The original PCAP and recovered executable are not included in this public repository. Findings are limited to the recorded evidence, and unresolved network observations are not labelled malicious without corroboration.

The vulnerable lab is separate from the supplied PCAP investigation. The lab findings should not be interpreted as proof of compromise in a production environment.

## Reproducibility

The report records the relevant commands, observations, and evidence references. Supporting outputs are provided where available. A TShark plugin warning was observed during analysis, and critical queries should be repeated with a healthy tool installation if higher-assurance forensic validation is required.
