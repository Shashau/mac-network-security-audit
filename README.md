# Local Mac Network Security Audit & Vulnerability Assessment

## Overview

This project is a hands-on cybersecurity assessment of my own Mac system.

The goal was to identify listening network ports, determine which processes were using those ports, verify services with Nmap, and check the status of the macOS firewall.

## Tools Used

- Nmap
- macOS Terminal
- lsof
- macOS Application Firewall
- Docker
- OWASP Juice Shop

## Objectives

- Identify open network ports
- Identify processes using listening ports
- Compare Nmap service detection with actual processes
- Check firewall status
- Identify potential security risks
- Document security findings

## Scope

This assessment was performed only on my own Mac and a locally hosted OWASP Juice Shop lab.

No unauthorized systems were scanned.

## Key Findings

- Several macOS services were listening on local ports.
- Nmap service detection was verified using `lsof`.
- Port 3000 was associated with the local OWASP Juice Shop lab.
- The Juice Shop container was stopped after testing.
- The macOS firewall was found to be disabled during the audit.

## Learning Outcome

This project helped me understand how cybersecurity professionals identify exposed services, verify processes behind network ports, and document security findings.

## Methodology

1. Performed a localhost Nmap service scan.
2. Identified listening TCP ports.
3. Used `lsof` to verify the processes associated with the ports.
4. Compared Nmap service detection with operating-system process information.
5. Checked the macOS Application Firewall status.
6. Stopped the local OWASP Juice Shop lab after testing.
7. Stored the collected evidence in the `evidence` directory.

## Findings

### Open Ports

| Port | Process | Observation |
|------|---------|-------------|
| 5000 | ControlCenter | macOS service |
| 7000 | ControlCenter | macOS service |
| 8021 | launchd | Local-only service |
| 49154 | rapportd | macOS communication service |
| 58736 | rapportd | Listening service |
| 58737 | rapportd | Listening service |

### Firewall

The macOS Application Firewall was disabled during the assessment.

This was intentional for the testing environment and was documented as a security configuration finding.

### Nmap Verification

Nmap incorrectly identified port 49154 as a MikroTik bandwidth-test service. Process-level verification using `lsof` showed that the port was actually being used by `rapportd`.

This demonstrates that automated service detection should be verified using additional operating-system information.

## Risk Assessment

| Finding | Risk Level | Reason |
|---------|------------|--------|
| Firewall disabled | Medium | Provides less inbound connection filtering |
| Multiple listening services | Low–Medium | Services increase the system's network attack surface |
| Nmap service misidentification | Informational | Detection tools can produce inaccurate service fingerprints |
| OWASP Juice Shop | Informational | Intentionally vulnerable lab; stopped after testing |

## Recommendations

- Enable the macOS Application Firewall when the system is not being used for controlled testing.
- Keep macOS and installed applications updated.
- Disable unnecessary services when appropriate.
- Verify automated security-tool results using operating-system information.
- Perform security testing only on systems you own or have permission to test.

## Conclusion

This assessment provided practical experience with network reconnaissance, port analysis, process identification, service verification, firewall assessment, and security documentation.

The project demonstrates a basic real-world cybersecurity workflow: identify exposed services, verify what is running, assess potential risks, and document the results.