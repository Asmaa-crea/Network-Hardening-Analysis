# Risk Assessment Report: Network Hardening Analysis

## Training Information
* **Course:** Course 3
* **Activity:** Activity: Network Hardening Analysis
* **Task Type:** Hands-on training assignment focusing on implementing network security controls and defensive measures.
  ## Introduction & Objective
The purpose of this analysis is to evaluate the current security posture of the network infrastructure, identify potential vulnerabilities, and implement network hardening strategies. By auditing open ports, protocols, and system configurations, this lab aims to mitigate security risks, prevent unauthorized access, and ensure the deployment of robust defensive security controls as practiced in the training.
## Scenario & Identified Vulnerabilities
The organization recently suffered a major data breach that compromised customers' personally identifiable information (PII), including names and addresses. A post-incident review of the organization's network infrastructure revealed four critical vulnerabilities that must be addressed immediately to prevent future breaches:

1. Shared employee passwords across the organization.
2. The database administrator password is still set to its default value.
3. Firewalls completely lack inbound and outbound traffic filtering rules.
4. Multifactor Authentication (MFA) is not implemented.

   ## Part 1: Recommended Network Hardening Tools & Methods

Based on the architectural and behavioral flaws identified within the infrastructure, the following specific tools and methods are recommended for implementation:

| Identified Vulnerability | Recommended Hardening Tool/Method | Core Objective & Mitigation Mechanism |
| :--- | :--- | :--- |
| **1. Shared Employee Passwords** | Strong Password Policies & PAM | Enforce strong, unique cryptographic passphrases and prohibit credential sharing across different accounts. |
| **2. Default Database Password** | Password Rotation & NIST Standards | Force immediate rotation of vendor default administrative credentials. Implement hashing and salting to secure database passwords. |
| **3. No Firewall Traffic Filtering** | Port Filtering & Firewall Rulesets | Disable all unused ports and implement strict inbound/outbound rulesets to permit only verified, business-critical traffic. |
| **4. MFA Not Implemented** | Multifactor Authentication (MFA) | Introduce a mandatory secondary verification layer (OTP/Authenticator app) so compromised passwords alone cannot grant access. |

## Part 2: Explanation of Recommendations & Implementation Frequency

### 1. Port Filtering & Firewall Maintenance
* **Why it is effective:** Firewalls act as the perimeter boundary defense. Operating without filtering rules allows unchecked lateral movement and arbitrary external connections. Implementing strict **Port Filtering** drastically diminishes the organization's attack surface by dropping unauthorized scanning attempts and blocking exploit vectors targeting open, unmonitored ports. Egress filtering also ensures that compromised assets cannot easily beacon out to malicious Command and Control (C2) servers.
* **Implementation Frequency:** Firewall rulesets must be audited and maintained **monthly**. Immediate out-of-band reviews are mandatory following any major network architecture updates, infrastructure changes, or upon detecting anomalous traffic patterns via SIEM alerts.

### 2. Multifactor Authentication (MFA)
* **Why it is effective:** Given the systemic issue of shared and default passwords in this environment, MFA is the single most effective control to halt unauthorized access. MFA neutralizes the risk of compromised passwords by requiring a distinct secondary factor (something you have or something you are). If a threat actor steals or guesses the default database administrator credentials, the authentication flow will still block them at the MFA prompt, rendering static leaked credentials useless.
* **Implementation Frequency:** MFA configuration is a **one-time core implementation** enforced globally across all corporate endpoints, database gateways, and cloud applications. Continuous maintenance includes revoking inactive tokens and auditing device logs **real-time / continuously**.

### 3. Comprehensive Password Policies (NIST Aligned)
* **Why it is effective:** Aligning with modern NIST guidelines, a strong **Password Policy** enforces long passphrases and structural uniqueness while mandating that backend databases store credentials using robust cryptographic algorithms (hashing and salting). This actively prevents brute-force scripting utilities from guessing employee accounts and stops the dangerous practice of account sharing by implementing individual accountability.
* **Implementation Frequency:** The underlying policy criteria should be reviewed and updated **quarterly (every 3 months)** to adapt to evolving threat models, while automated system-level checks validate credential compliance during every account creation or update phase.
