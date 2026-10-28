# Recommendations — Botium Toys

These recommendations are for the IT manager to share with stakeholders. They are ordered by how quickly each risk needs to be addressed.

## High priority — implement first

| Recommendation | Risk it reduces | Compliance it supports |
|---|---|---|
| **Least privilege and separation of duties:** give employees access only to the data their role needs, and split critical tasks between different people. | Insider misuse, fraud, large exposure if an account is compromised | PCI DSS, GDPR, SOC 1/SOC 2 |
| **Encryption:** encrypt credit card data and customer PII/SPII, both stored and in transit, including payment touchpoints. | Data theft and breach of confidentiality | PCI DSS, GDPR, SOC 1/SOC 2 |
| **Intrusion detection system (IDS):** monitor network traffic for signs of attack. | Intrusions going unnoticed | Supports the NIST CSF Detect function |
| **Backups and a disaster recovery plan:** back up critical data regularly and write a tested recovery plan. | Data loss and long downtime after an incident | Business continuity |

## Medium priority — implement next

| Recommendation | Risk it reduces | Compliance it supports |
|---|---|---|
| **Stronger password policy:** require at least 8 characters with letters, numbers and special characters. | Account compromise through brute force or guessing | PCI DSS |
| **Central password management system:** enforce the policy automatically and let users reset their own passwords. | Weak passwords; fewer reset tickets for IT | PCI DSS |
| **Legacy system schedule:** set a regular maintenance schedule and clear intervention steps for end-of-life systems. | Unpatched vulnerabilities in old systems | — |
| **Classify assets:** go beyond the current inventory and label assets by sensitivity and business impact. | Not knowing which assets need the most protection | GDPR, NIST CSF Identify |

## Keep in place

Firewall, antivirus, physical locks, CCTV, fire detection and prevention, the GDPR 72-hour breach notification plan, the privacy policies, and the data integrity controls.

## Expected outcome

Most of the compliance gaps come from two problems: **open access to data** and **no encryption**. Fixing the high-priority items first would close most of the gaps in PCI DSS, GDPR and SOC, and should bring the overall risk score down from 8/10.
