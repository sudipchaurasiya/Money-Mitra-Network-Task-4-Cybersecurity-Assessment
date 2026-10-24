# Task 4 - Incident Response Plan

## 1. Purpose and Scope

This plan describes how a security team should respond to the observations recorded during the network investigation and the authorized Metasploitable 2 lab assessment.

The PCAP investigation and the lab vulnerability assessment concern different environments. They must not be treated as one confirmed incident without evidence linking them.

## 2. Preparation

- Maintain an inventory of authorized systems and their owners.
- Keep network diagrams, asset records, and incident contact details available.
- Enable centralized DNS, proxy, firewall, authentication, and endpoint logging.
- Synchronize system clocks and preserve time-zone information.
- Prepare an isolated analysis environment for suspicious files.
- Maintain verified backups and a tested recovery process.

## 3. Identification and Analysis

### Network investigation

- Preserve the original PCAP and record its SHA-256 hash.
- Review packets 23091 and 24916 for the executable HTTP request and response.
- Record the observed file hash: b789adce70c028a6d17be45ec34667aa95586350ee0c4057e75b138b1ad35061.
- Investigate the long encrypted connection to 195.63.128.106:443 using authorized endpoint and network logs.
- Review the holtandberyl.com requests and DNS errors in context.
- Do not label a lead malicious unless corroborating evidence supports that conclusion.

### Lab vulnerability assessment

- Record the exposed root bind shell on TCP 1524.
- Record anonymous FTP access on TCP 21.
- Review legacy web, Telnet, database, and other exposed services.
- Keep this lab assessment separate from the PCAP incident investigation.

## 4. Containment

If an authorized production investigation confirms a real threat:

- Isolate the affected endpoint using the organization's approved process.
- Restrict access to confirmed malicious or unnecessary network services.
- Preserve relevant logs and forensic evidence before destructive changes where practical.
- Block an indicator only after validation and approval, considering business impact.
- Do not contact suspicious external infrastructure or execute the recovered executable.

For the intentionally vulnerable lab, restrict access to the isolated lab network and stop unnecessary exposed services.

## 5. Eradication

After confirming compromise:

- Remove unauthorized persistence and malicious files using an approved response procedure.
- Patch or rebuild affected systems from trusted sources.
- Disable anonymous FTP, Telnet, and unnecessary services.
- Replace unsupported web and database software with supported versions.
- Rotate credentials or revoke tokens if exposure is established.
- Validate the system after remediation.

Do not claim eradication is complete until verification evidence is available.

## 6. Recovery

- Restore from known-good backups or trusted system images where needed.
- Reconnect systems only after required security checks pass.
- Monitor authentication, DNS, proxy, firewall, and endpoint events.
- Verify service availability and business functionality.
- Record recovery approval, monitoring period, and remaining risks.

## 7. Lessons Learned

- Improve asset inventory and service exposure reviews.
- Reduce unnecessary network access and segment sensitive systems.
- Improve DNS, proxy, firewall, and endpoint logging.
- Test detection rules against known benign and suspicious examples.
- Record evidence gaps and update procedures after the exercise.

## 8. Prioritized Recommendations

Priority 1 - Critical:
Remove or isolate the root bind shell on lab TCP 1524. Verify that no equivalent exposure exists on production assets.

Priority 2 - High:
Disable anonymous FTP unless explicitly required and approved. Restrict access and verify file permissions.

Priority 3 - High:
Upgrade unsupported Apache and PHP components and verify the installed versions after remediation.

Priority 4 - High:
Disable Telnet and use SSH for authorized remote administration.

Priority 5 - High:
Restrict database access to approved hosts and upgrade unsupported MySQL and PostgreSQL versions.

Priority 6 - High:
Review additional legacy services and disable those that are not required.

Priority 7 - High:
Investigate the executable download through approved endpoint and proxy evidence. Keep the file quarantined and do not execute it.

Priority 8 - Medium:
Investigate the long encrypted connection to 195.63.128.106:443 using available endpoint, network, and business-context evidence.

Priority 9 - Medium:
Review DNS error patterns and the holtandberyl.com requests without treating either as malicious based on the current evidence alone.

Priority 10 - Medium:
Improve centralized logging, alert validation, incident documentation, and periodic vulnerability reviews.

## 9. Evidence and Limitations

- Source PCAP SHA-256: 287d6dee90cfef71f98a97c42e30444608de2cf59d2f7392a0a6df8dbbc8274b.
- The executable was not executed.
- The executable's maliciousness has not been established.
- The purpose of the long encrypted connection remains unresolved.
- The lab services were observed through scans and selected checks; not every service was fully tested.
- No production compromise, successful exploitation, or completed remediation is claimed by this plan.
