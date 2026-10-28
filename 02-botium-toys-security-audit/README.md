# Botium Toys — Internal Security Audit

A simulated internal IT security audit of **Botium Toys**, a fictional small U.S. toy company with a physical store, a warehouse and a growing online store that serves customers worldwide, including the E.U.

> Completed as a portfolio activity in the Google Cybersecurity Professional Certificate (Course 2: *Play It Safe: Manage Security Risks*). The company and its data are fictional. I reviewed my answers against the course exemplar afterwards, and the mistakes I made are documented below.

---

## Scenario

The IT manager asked for an internal audit because the business is growing fast and the security program has not kept up. The company accepts and stores credit card payments, processes data of E.U. customers, and runs some legacy systems. Management wants to know which security controls are missing and where the company falls short of compliance requirements.

## Scope and goals

| | |
|---|---|
| **Scope** | The whole security program: employee equipment and devices, the internal network, systems and software (accounting, e-commerce, database, inventory), data storage and retention, legacy systems, and the physical location (offices, storefront, warehouse). |
| **Goals** | Review current assets, check which controls are in place, assess compliance with PCI DSS, GDPR and SOC 1/SOC 2, and recommend what to implement first to improve the company's security posture. |
| **Framework** | NIST Cybersecurity Framework (CSF), starting with the **Identify** function |

## Method

1. Reviewed the scope, goals and risk assessment report provided by the IT manager.
2. Listed the assets the IT department manages.
3. Checked 14 administrative, technical and physical controls and marked whether each one is in place.
4. Checked 12 best practices across PCI DSS, GDPR and SOC 1/SOC 2.
5. Compared my answers with the course exemplar and recorded every mistake.
6. Wrote prioritized recommendations for stakeholders.

Full checklist: [controls-compliance-checklist.md](controls-compliance-checklist.md)

## Risk summary

| Item | Rating |
|---|---|
| Overall risk score | **8 / 10 (high)** |
| Potential impact of losing an asset | Medium (the IT department doesn't know which assets are at risk) |
| Likelihood of asset loss or regulatory fines | High |

**Main reason:** assets are not managed or classified properly, several key controls are missing, and the company does not fully follow PCI DSS, GDPR or SOC best practices.

## Key findings

**Controls in place (5 of 14):** firewall, antivirus, locks, CCTV, fire detection and prevention

**Missing or not good enough (9 of 14):**

| Area | Gap |
|---|---|
| Access | Every employee can see internal data, including cardholder data and customer PII/SPII. There is no least privilege and no separation of duties. |
| Data protection | Credit card and customer data are not encrypted. |
| Detection | No intrusion detection system (IDS). |
| Recovery | No backups of critical data and no disaster recovery plan. |
| Passwords | The password policy is weak and there is no central password management system. |
| Legacy systems | They are monitored, but not on a regular schedule, and there is no clear intervention procedure. |

**Compliance:** 4 of 12 best practices are met. Most of the gaps come from the same two problems: open access to data and missing encryption.

## Self-review: 24/26 correct

After finishing the checklist I compared it with the course exemplar. Controls assessment: **14/14 correct**. Compliance checklist: **10/12 correct**.

| Best practice | My answer | Correct answer | What I missed | Lesson |
|---|---|---|---|---|
| **PCI DSS:** Credit card information is stored, accepted, processed and transmitted internally, in a secure environment. | ❌ Yes | ✅ No | The card data does stay internal, but it is **not encrypted** and **every employee** can access it. That environment is not secure. | Data being handled in-house doesn't mean it is handled securely. Check every condition in the statement. |
| **SOC 1/SOC 2:** Data is available to individuals authorized to access it. | ❌ Yes | ✅ No | Data is available to **all** employees, not only to the people whose jobs require it. | Availability is only half of this statement. The key word is **authorized**, so it also needs access control (least privilege). |

**Takeaway:** In both cases I answered "Yes" because one part of the statement was true. An audit item passes only if the whole statement is true.

## Recommendations

See [recommendations.md](recommendations.md) for the full list. In short:

- **High priority:** least privilege and separation of duties, encryption of card and customer data, an IDS, backups and a disaster recovery plan
- **Medium priority:** a stronger password policy and a password management system, a regular maintenance schedule for legacy systems, and classifying assets

## Skills demonstrated

- Planning and carrying out an internal security audit (scope, risk assessment, controls assessment, compliance check)
- Applying the **NIST CSF** (Identify function: asset inventory and classification)
- Sorting controls into **administrative, technical and physical** categories and **preventive, detective, corrective and deterrent** types
- Checking compliance with **PCI DSS, GDPR and SOC 1/SOC 2**
- Prioritizing risk and writing recommendations for stakeholders
- Reviewing my own work critically and documenting mistakes
