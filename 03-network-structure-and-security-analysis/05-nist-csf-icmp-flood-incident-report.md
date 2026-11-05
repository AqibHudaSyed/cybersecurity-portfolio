# Incident Report: ICMP Flood DoS Attack (NIST CSF)

## Summary
A company's network services suddenly stopped working because of a flood of incoming ICMP packets. The firewall had no rules, so the attacker was able to overwhelm the internal network with a denial of service (DoS) attack. I used the **NIST Cybersecurity Framework (CSF)** to document what happened and to plan how to protect, detect, respond and recover from this kind of attack in the future.

## Scenario
- **Company:** A multimedia company that offers web design, graphic design and social media marketing to small businesses.
- **Incident:** A DoS attack took the internal network down for about two hours.
- **What users saw:** Normal internal traffic could not reach any network resources.
- **Root cause:** An attacker sent a flood of ICMP pings through a firewall that was not configured.

## Skills used
| Area | Used for |
|---|---|
| NIST CSF | Structuring the report into Identify, Protect, Detect, Respond and Recover |
| Network attack analysis | Recognising an ICMP flood and its impact |
| Firewall and IDS/IPS | Choosing controls to stop and spot the attack |
| Incident reporting | Writing a clear report for the team and management |

## How the attack worked
```mermaid
flowchart LR
    A[Attacker] -- "flood of ICMP pings" --> F[Firewall<br/>no rules configured]
    F -- "all ICMP traffic let in" --> N[Internal network]
    N -- "overloaded" --> X[Network services stop<br/>for ~2 hours]
```

## ICMP flood vs ping of death
| Attack | What it is |
|---|---|
| **ICMP flood** (this incident) | A huge number of normal ping packets, sent so fast that the network cannot handle them |
| Ping of death | A single oversized or broken ping packet that crashes a system |

## Incident report (NIST CSF)

### Summary
Our organization had a sudden stop in network services because of an incoming flood of ICMP packets. This ICMP flood left the internal network unable to reach network resources. It happened because the organization's firewall was not configured to stop unwanted traffic. This left a large attack surface, and the threat actor used it to overwhelm the company's network with a denial of service (DoS) attack. The team blocked incoming ICMP traffic, stopped the non-critical services and restored the critical services.

### Identify
The security team investigated the event and found that the malicious actor had sent a flood of ICMP packets, causing an ICMP flood DoS attack. The attack happened because the company's firewall was not configured. The entire internal network was affected.

### Protect
To counter this event, the security team added a new firewall rule to limit the rate of incoming ICMP packets. Source IP address verification was also set up on the firewall to check for spoofed IP addresses on incoming traffic. An IPS was added to filter out suspicious ICMP traffic. The team will also maintain the firewall regularly, keeping its rules up to date.

### Detect
To spot malicious traffic, the team set up network monitoring software to catch abnormal traffic patterns, and an IDS that alerts the team about suspicious ICMP traffic. Network logs are analysed to find events of interest.

### Respond
The security team isolated the affected systems, restored the critical services and set up network log analysis. The team also informed management about the event. Management will inform law enforcement if needed.

### Recover
The team will recover by:
1. Blocking ICMP flood traffic at the firewall.
2. Stopping non-critical services to reduce load on the network.
3. Restoring critical systems and services first.
4. Bringing non-critical services back online once the ICMP flood stops, so the internal network can use its resources again.

## Quick view
| CSF function | Main action |
|---|---|
| Identify | ICMP flood through an unconfigured firewall; whole internal network affected |
| Protect | ICMP rate-limit rule, source IP verification, IPS, regular firewall maintenance |
| Detect | Network monitoring software, IDS alerts, log analysis |
| Respond | Isolate affected systems, restore critical services, inform management |
| Recover | Block at firewall → stop non-critical → restore critical first → bring the rest back |

## What I learned
- One missing firewall configuration can take down a whole network.
- An ICMP flood is many normal packets; a ping of death is one bad packet.
- Detect means spotting and alerting; blocking belongs to Protect.
- In recovery, critical services come back first, the rest after the attack stops.
