# Controls and Compliance Checklist — Botium Toys

**Question:** Does Botium Toys currently have this control in place, or follow this best practice?

Rows marked ❌ are the ones I got wrong on my first attempt. The answer in the table is the corrected one, and my original answer is shown in the note. See the [self-review in the README](README.md#self-review-2426-correct) for details.

---

## Controls assessment (14/14 correct)

| Control | Category | Type | In place? | Reason |
|---|---|---|---|---|
| Least privilege | Administrative | Preventive | **No** | Every employee can access customer data, including cardholder data and PII/SPII. |
| Disaster recovery plans | Administrative | Corrective | **No** | There is no plan, so business continuity is at risk after an incident. |
| Password policies | Administrative | Preventive | **No** | A policy exists but its requirements are below current minimums, which makes accounts easier to compromise. |
| Separation of duties | Administrative | Preventive | **No** | Not implemented. This raises the risk of fraud and insider misuse of critical data. |
| Firewall | Technical | Preventive | **Yes** | Blocks traffic based on a properly defined set of security rules. |
| Intrusion detection system (IDS) | Technical | Detective | **No** | Not installed, so possible intrusions could go unnoticed. |
| Backups | Technical | Corrective | **No** | Critical data is not backed up, so it can't be restored after a breach or failure. |
| Antivirus software | Technical | Corrective | **Yes** | Installed and monitored regularly by the IT department. |
| Manual monitoring, maintenance and intervention for legacy systems | Technical | Preventive | **No** | Legacy systems are monitored, but not on a regular schedule, and intervention steps are unclear. |
| Encryption | Technical | Preventive | **No** | Not used, so sensitive customer and card data is not kept confidential. |
| Password management system | Technical | Preventive | **No** | There is no central system to enforce the policy. Password resets also slow down employees and IT. |
| Locks (offices, storefront, warehouse) | Physical | Preventive | **Yes** | The physical location has enough locks. |
| CCTV surveillance | Physical | Preventive / Detective | **Yes** | Installed, up to date and working. |
| Fire detection and prevention | Physical | Detective / Preventive | **Yes** | Fire alarm and sprinkler systems are working. |

> In the course's control categories document, encryption is listed as *deterrent*, IDS/IPS as *detective* and antivirus as *corrective*. I used the more common labels above: encryption is preventive, an IDS is detective (an IPS would also be preventive), and antivirus is both detective and corrective.

---

## Compliance checklist (10/12 correct)

### PCI DSS (3/4 correct)

| Best practice | Follows it? | Reason |
|---|---|---|
| Only authorized users have access to customers' credit card information. | **No** | Every employee can access internal data, including card data. |
| ❌ Credit card information is stored, accepted, processed and transmitted internally, in a secure environment. | **No** *(my answer: Yes)* | The data is unencrypted and open to every employee, so the environment is not secure. |
| Implement data encryption procedures to better secure credit card transaction touchpoints and data. | **No** | Encryption is not used. |
| Adopt secure password management policies. | **No** | The password policy is weak and there is no password management system. |

### GDPR (4/4 correct)

| Best practice | Follows it? | Reason |
|---|---|---|
| E.U. customers' data is kept private/secured. | **No** | The data is not encrypted and every employee can access it. |
| There is a plan to notify E.U. customers within 72 hours if their data is compromised. | **Yes** | The IT department has a 72-hour breach notification plan. |
| Ensure data is properly classified and inventoried. | **No** | Assets are listed but not classified. |
| Enforce privacy policies, procedures and processes to properly document and maintain data. | **Yes** | Privacy policies have been developed and are enforced among IT staff and other employees. |

### SOC 1 / SOC 2 (3/4 correct)

| Best practice | Follows it? | Reason |
|---|---|---|
| User access policies are established. | **No** | No least privilege and no separation of duties. Every employee can access internal data. |
| Sensitive data (PII/SPII) is confidential/private. | **No** | PII/SPII is not encrypted. |
| Data integrity ensures the data is consistent, complete, accurate and has been validated. | **Yes** | The IT department has controls in place for data integrity. |
| ❌ Data is available to individuals authorized to access it. | **No** *(my answer: Yes)* | Data is available, but to everyone. Access has to be limited to the people who need it for their jobs. |
