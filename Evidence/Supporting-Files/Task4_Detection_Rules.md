# Task 4 - Detection Engineering

## 1. Wireshark Display Filters

### Filter 1: Executable download activity
`ip.addr == 107.175.82.242 && tcp.port == 9000`

Purpose: Displays traffic involving the endpoint associated with the observed executable download.

Limitation: An IP address and port alone do not prove malicious activity.

### Filter 2: HTTP requests to the observed domain
`http.host == "holtandberyl.com" && (http.request.uri == "/prw" || http.request.uri == "/crv")`

Purpose: Locates the two observed HTTP requests and their redirects.

Limitation: Short URL paths and redirects can occur during legitimate browsing.

### Filter 3: DNS error responses
`dns.flags.response == 1 && dns.flags.rcode != 0`

Purpose: Displays DNS error responses, including NXDOMAIN.

Limitation: Failed DNS lookups may be normal and require contextual review.

## 2. Defensive Detection Rule 1

Title: Executable Download Over TCP Port 9000
Status: Experimental
Log source: HTTP proxy or network monitoring logs

Detection logic:
- Destination IP: 107.175.82.242
- Destination port: 9000
- HTTP method: GET
- Requested path: /wilow/runner_ilove.exe

Expected alert: A client requests the recorded executable path.

Severity: High-priority investigation lead, subject to local validation.

False positives: Approved software downloads, lab traffic, or legitimate transfers over an unusual port.

Limitations: This rule is specific to the observed endpoint and path. An alert does not prove malware or execution.

SOC response: Review proxy logs, endpoint telemetry, the file hash, and the business justification. Do not execute the file during triage.

## 3. Defensive Detection Rule 2

Title: Repeated DNS NXDOMAIN Responses
Status: Experimental
Log source: DNS resolver logs

Detection logic:
- Query name: wpad.natureforce.com
- Response code: NXDOMAIN
- Multiple responses occur within a defined monitoring window.

Expected alert: Repeated failed DNS lookups for the specified name.

Severity: Low; informational until corroborated.

False positives: Normal WPAD discovery, missing DNS records, or configuration errors.

Limitations: One NXDOMAIN response is not suspicious by itself. The time window and threshold must be tuned.

SOC response: Check the querying asset, DNS configuration, lookup frequency, and related endpoint or proxy events.

## 4. Operational Notes

- Validate field names against the actual SIEM or proxy platform.
- Preserve timestamps, IP addresses, ports, and packet references.
- Tune thresholds to reduce false positives.
- Treat these rules as investigation aids, not automatic malware verdicts.
