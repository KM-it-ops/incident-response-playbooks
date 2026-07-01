# Incident Response Playbook — NIST SP 800-61r3 (CSF 2.0 Community Profile)

**Framework Reference:** NIST Special Publication 800-61 Revision 3 (April 2025) —
*Incident Response Recommendations and Considerations for Cybersecurity Risk Management: A CSF 2.0 Community Profile.* Supersedes SP 800-61 Rev. 2 (2012).

**Last reviewed:** 2026-07-01

**Scope:** Personal reference library / portfolio artifact. Describes how incident response integrates into enterprise cybersecurity risk management — not a claim of prior employment at any specific institution.

This playbook maps incident-handling practice to the **six CSF 2.0 Functions** (Govern, Identify, Protect, Detect, Respond, Recover). SP 800-61r3 deliberately retires the rigid four-phase lifecycle in favor of continuous, risk-management-embedded IR. Preparation spans GV/ID/PR; active IR spans DE/RS/RC; improvement loops through **ID.IM**.

---

## How SP 800-61r3 Differs from Rev. 2

| Rev. 2 (2012) | Rev. 3 (2025) |
|---|---|
| Four-phase lifecycle: Preparation → Detection & Analysis → Containment/Eradication/Recovery → Post-Incident | Six CSF 2.0 Functions with continuous improvement via ID.IM |
| IR treated as discrete event bounded by days surrounding an incident | IR embedded in ongoing cybersecurity risk management |
| Static procedural detail in one publication | Outcome-driven guidance; implementation detail via CPRT, online resources, org-specific runbooks |
| No explicit Govern function | **Govern (GV)** is first-class — policy, roles, oversight, supply chain |

Use NIST's [Incident Response project page](https://csrc.nist.gov/projects/incident-response) and the [CSF 2.0 Reference Tool (CPRT)](https://csrc.nist.gov/projects/cprt) alongside this playbook for subcategory-level implementation examples.

---

## GOVERN (GV) — Establish Strategy, Roles, and Oversight

IR does not start at alert time. Governance outcomes define who decides, under what policy, with what risk tolerance, and how performance is measured.

### Finalize and exercise an **incident response plan** aligned to organizational context and regulatory obligations. Define **roles, responsibilities, and authorities** with no gaps and no conflicting authority during live events:

| Role | Primary IR Accountability |
|---|---|
| **Risk Manager** | Risk register, acceptance decisions, escalation thresholds |
| **Compliance / Legal** | Regulatory notification, audit-trail integrity, disclosure timing |
| **IR Coordinator / SOC Lead** | Lifecycle execution from triage through closure |
| **Technical responders** | Endpoint, network, identity, cloud, email specialists |
| **Communications lead** | Internal and external messaging, stakeholder coordination |

### GV.OC — Organizational Context
- Map mission-critical services, customer dependencies, and stakeholder expectations (GV.OC-04, GV.OC-05).
- Maintain a living register of **legal, regulatory, and contractual obligations** — FISMA, FedRAMP, HIPAA, GLBA, SEC disclosure, state breach laws, sector guidance (GV.OC-03).
- Document third-party dependencies (M365, SaaS, MSPs) and their IR contact paths.

### GV.RM — Risk Management Strategy
- Define **risk appetite and tolerance** for downtime, data exposure, and brand abuse (GV.RM-02).
- Standardize incident **severity/priority taxonomy** tied to business impact (GV.RM-06).
- Include cybersecurity risk outcomes in enterprise risk management processes (GV.RM-03).
- Establish lines of communication for cyber risks, including from suppliers and third parties (GV.RM-05).

### GV.RR — Roles, Responsibilities, and Authorities
- Publish RACI for IR; enforce through HR and access provisioning (GV.RR-02, GV.RR-04).
- Allocate resources commensurate with 24×7 coverage requirements where applicable (GV.RR-03).

### GV.PO — Policy
- Establish IR policy referencing CSF 2.0 outcomes; review on threat/tech/mission change (GV.PO-01, GV.PO-02).
- Policy covers evidence handling, communication, escalation, and third-party coordination.

### GV.OV — Oversight
- Review IR metrics, tabletop results, and post-incident findings at defined cadence (GV.OV-01, GV.OV-03).
- Adjust strategy when recurring incident classes (e.g., phishing campaigns) indicate control gaps.

### GV.SC — Cybersecurity Supply Chain Risk Management
- Include critical suppliers in **incident planning, response, and recovery** activities (GV.SC-08).
- Assess vendor IR SLAs, breach-notification clauses, and access to logs/APIs before acquisition (GV.SC-06, GV.SC-07).
- Monitor third-party compromise indicators (SolarWinds-class, OAuth app abuse, MFA bypass via IdP partners).

---

## IDENTIFY (ID) — Understand Assets, Risk, and Improvement

### ID.AM — Asset Management
- Maintain authoritative inventories of hardware, software, cloud tenants, SaaS apps, and data flows (ID.AM-01–05, ID.AM-07–08; note CSF 2.0 has no ID.AM-06).
- Prioritize assets by classification and mission impact — IR speed depends on knowing what is affected (ID.AM-05).
- Inventory **brand assets**: domains, subdomains, executive names, mobile apps, social handles used in impersonation.

### ID.RA — Risk Assessment
- Ingest threat intelligence from ISACs, commercial feeds, and government sources (ID.RA-02).
- Record phishing TTPs, brand-abuse patterns, and credential-harvest kit fingerprints (ID.RA-03).
- Tie vulnerabilities to likely incident scenarios; prioritize remediation by exploitability × impact (ID.RA-04, ID.RA-05).

### ID.IM — Improvement (Continuous)
- Feed lessons learned from incidents, tabletops, and purple-team exercises back into all functions (ID.IM-01, ID.IM-02).
- Maintain and improve IR plans, runbooks, and SOAR playbooks from operational execution (ID.IM-03, ID.IM-04).
- SP 800-61r3 treats **ID.IM as the improvement spine** — not a one-time "post-incident" phase.

---

## PROTECT (PR) — Safeguards That Reduce Incidents and Enable Response

### PR.AA — Identity, Authentication, Access
- Enforce MFA, conditional access, privileged access management; segment admin paths (PR.AA-03, PR.AA-05).
- Pre-stage break-glass accounts and emergency access procedures for IR (documented, monitored, time-bound).

### PR.AT — Awareness and Training
- General phishing awareness for all personnel (PR.AT-01).
- Role-specific training for SOC analysts, help desk, and brand-protection staff (PR.AT-02).

### PR.DS — Data Security
- Protect logs, case artifacts, and forensic images at rest and in transit (PR.DS-01, PR.DS-02).
- Define retention for IR evidence aligned to legal hold and regulatory minimums (organizational policy; backup integrity for recovery maps to PR.DS-11).

### PR.PS — Platform Security
- Harden email gateways, proxies, and endpoint agents; ensure log generation for monitoring (PR.PS-04).
- Baseline M365/Entra configurations; prevent unauthorized OAuth consent and forwarding rules.

### PR.IR — Technology Infrastructure Resilience
- Implement resilience mechanisms so monitoring and IR telemetry survive partial compromise (PR.IR-03).
- Capacity-plan SOC tooling for surge events — campaign spikes, widespread phishing reports (PR.IR-04).

---

## DETECT (DE) — Find and Analyze Adverse Events

### DE.CM — Continuous Monitoring
- Monitor networks, personnel activity, and computing environments for compromise indicators (DE.CM-01, DE.CM-03, DE.CM-09).
- Monitor third-party/SaaS provider activity where brand-abuse kits land on external hosts (DE.CM-06).
- Track external brand surfaces (look-alike domains, certificate transparency, social impersonation) via threat intel and brand-monitoring feeds — correlate into DE.AE analysis (DE.AE-07).
- **SIEM correlation concepts (lab/portfolio):** join email telemetry (headers, URLs, attachments), proxy logs, DNS queries, Entra sign-in anomalies, and user report timestamps into a single campaign object.

### DE.AE — Adverse Event Analysis
- Correlate multi-source signals before declaring an incident (DE.AE-03).
- Integrate threat intelligence and historical campaign data (DE.AE-07).
- Apply defined **incident criteria** — when to open a case vs. close as benign (DE.AE-08).
- Estimate scope and impact early; refine as investigation proceeds (DE.AE-04).

---

## RESPOND (RS) — Manage, Analyze, Communicate, Mitigate

Active response maps to four RS categories. In Threat Disruptions contexts, many events are **external-facing brand abuse** rather than internal compromise — containment emphasizes takedown and user protection, not always disk imaging.

### RS.MA — Incident Management
- Execute the IR plan in coordination with legal, comms, and third parties (RS.MA-01).
- **Triage and validate** user reports, automated alerts, and ISAC notifications (RS.MA-02).
- Categorize and prioritize by customer impact, active credential harvesting, and regulatory exposure (RS.MA-03).
- **Escalate** to enterprise SOC/IR when internal indicators exist — not just external brand abuse (RS.MA-04).
- Apply criteria to transition from response to recovery (RS.MA-05).

### RS.AN — Incident Analysis
- Establish timeline: first seen, delivery vector, click-through, credential submission, lateral movement if any (RS.AN-03).
- Preserve integrity of investigative records and chain of custody (RS.AN-06, RS.AN-07).
- Validate magnitude — count of targeted users, successful clicks, exfil volume (RS.AN-08).

### RS.CO — Reporting and Communication
- Notify internal stakeholders ( fraud, legal, comms, executive crisis team) per severity matrix (RS.CO-02).
- Share indicators with FS-ISAC, sector partners, and takedown vendors under NDAs and sharing agreements (RS.CO-03).

### RS.MI — Incident Mitigation
- **Contain:** block URLs/domains at proxy, remove malicious mail from inboxes, disable compromised accounts, revoke sessions (RS.MI-01).
- **Eradicate:** remove persistence (forwarding rules, OAuth apps, malware), patch exploited vulns (RS.MI-02).
- **Takedown:** initiate registrar/hosting/abuse workflows for brand-abuse infrastructure; track provider ticket IDs.

---

## RECOVER (RC) — Restore Operations and Communicate Recovery

### RC.RP — Recovery Plan Execution
- Execute recovery procedures once RS.MA-05 criteria are met (RC.RP-01).
- Prioritize restoration of critical services; verify backup integrity before restore (RC.RP-02, RC.RP-03).
- Confirm normal operating status and document closure (RC.RP-05, RC.RP-06).

### RC.CO — Recovery Communication
- Communicate restoration status to affected customers, regulators (where required), and internal leadership.
- Publish internal "all clear" with any required user actions (password reset, MFA re-enrollment).

Post-recovery, route all findings into **ID.IM** — update detection rules, awareness content, DMARC policy, and runbooks.

---

## CSF 2.0 Alignment Table

| CSF Function | Category ID | Category Name | Playbook Coverage |
|---|---|---|---|
| **Govern** | GV.OC | Organizational Context | Regulatory mapping, mission dependencies, third-party IR contacts |
| | GV.RM | Risk Management Strategy | Severity taxonomy, risk appetite, prioritization method |
| | GV.RR | Roles, Responsibilities, and Authorities | RACI, 24×7 staffing model, escalation authorities |
| | GV.PO | Policy | IR policy, evidence handling, communication standards |
| | GV.OV | Oversight | Metric review, tabletop cadence, strategy adjustment |
| | GV.SC | Cybersecurity Supply Chain Risk Management | Vendor IR clauses, third-party monitoring, supplier incident coordination |
| **Identify** | ID.AM | Asset Management | IT + brand asset inventory, data-flow maps |
| | ID.RA | Risk Assessment | Threat intel ingestion, phishing TTP catalog, scenario-based risk |
| | ID.IM | Improvement | Lessons learned, runbook/SOAR updates, plan maintenance |
| **Protect** | PR.AA | Identity Management, Authentication, and Access Control | MFA, conditional access, break-glass |
| | PR.AT | Awareness and Training | Phishing reporting culture, analyst specialization |
| | PR.DS | Data Security | Log and evidence protection, retention |
| | PR.PS | Platform Security | Email/proxy/endpoint hardening, M365 baselines |
| | PR.IR | Technology Infrastructure Resilience | Monitoring redundancy, surge capacity |
| **Detect** | DE.CM | Continuous Monitoring | SIEM, email telemetry, third-party monitoring |
| | DE.AE | Adverse Event Analysis | Multi-source correlation, incident declaration criteria |
| **Respond** | RS.MA | Incident Management | Triage, categorization, escalation, plan execution |
| | RS.AN | Incident Analysis | Timeline, forensics, scope validation |
| | RS.CO | Incident Response Reporting and Communication | Stakeholder notification, ISAC sharing |
| | RS.MI | Incident Mitigation | Containment, eradication, takedown |
| **Recover** | RC.RP | Incident Recovery Plan Execution | Service restoration, backup verification, closure |
| | RC.CO | Incident Recovery Communication | Customer/regulatory recovery messaging |

---

## Modernization Notes (2025–2026)

### SOAR and Runbook Automation
- Encode repeatable workflows (phishing triage, mailbox purge, URL block, account disable) as **SOAR playbooks** with human approval gates for high-impact actions.
- Automate enrichment: WHOIS, passive DNS, sandbox detonation, reputation lookups, user click attribution.
- Keep automation **idempotent and logged** — every automated action produces an auditable ticket entry.

### Cloud and M365 Incident Handling
- Treat **Entra ID, Exchange Online, SharePoint, Teams, and OAuth consent grants** as first-class IR surfaces.
- Standard runbook steps: revoke refresh tokens, reset creds, remove malicious inbox rules, audit `ApplicationPermissionGrant`, review `UnifiedAuditLog`.
- Cloud forensics differs from disk imaging — prioritize API-based evidence collection before attacker cleanup.

### Supply Chain (GV.SC)
- Monitor SaaS integrations and OAuth apps with the same rigor as on-prem software.
- Pre-contract IR requirements: breach notification SLA, forensic cooperation, log export APIs.
- Tabletop scenarios include **vendor compromise** and fraudulent vendor invoice phishing.

---

## Financial Sector IR Annex

Sector-specific overlays for banks and financial services institutions. Adapt to your org's regulatory footprint.

### FFIEC Cybersecurity Assessment Tool (CAT)
- Map IR capabilities to CAT maturity domains: **Cyber Risk Management and Oversight**, **Threat Intelligence and Collaboration**, **Cybersecurity Controls**, **External Dependency Management**, **Cyber Incident Management and Resilience**.
- **Note:** FFIEC retired the CAT on **August 31, 2025**; examiners now point institutions to NIST CSF 2.0 and sector performance goals. CAT remains useful vocabulary for financial-sector IR interviews.
- Maintain evidence of IR testing (tabletops, technical exercises) for examiner-style inquiry.
- Document alignment between **inherent risk profile** and **cybersecurity maturity** for incident-response components — CAT's two-part structure, not "declared vs. inherent."

### FS-ISAC and Sector Sharing
- Participate in FS-ISAC (or relevant ISAC) for phishing indicators, campaign attribution, and sector-specific TTPs.
- Normalize sharing format (STIX/TAXII where supported); respect TLP markings.
- Inbound ISAC intel feeds detection rules; outbound org indicators help peer institutions.

### GLBA Safeguards Rule
- Incident response supports the **Safeguards Rule** information security program — detect, respond to, and recover from events affecting customer information.
- Document how IR connects to the designated qualified individual's oversight and annual risk assessment.

### SEC Cyber Disclosure (2023 Final Rules)
- Material cybersecurity incidents require **Form 8-K disclosure** (typically four business days after materiality determination).
- Maintain IR → Legal → Disclosure Committee workflow with documented materiality assessment criteria.
- Annual 10-K disclosure of cybersecurity risk management and governance processes.

### Bank 24×7 SOC Tiering
- **Tier 1:** Alert triage, user report intake, initial enrichment, playbook execution within defined SLAs.
- **Tier 2:** Deep analysis, campaign correlation, containment decisions, takedown initiation.
- **Tier 3 / IR Lead:** Cross-domain incidents, regulatory notification, executive briefing, purple-team feedback.
- **Threat Disruptions / brand-abuse teams** often operate as specialized Tier 1–2 with escalation paths to enterprise IR when internal compromise is confirmed.

---

## Threat Disruptions Operations Annex

Operational workflow for **external-facing threat disruption** — phishing, brand impersonation, fraudulent domains, and social-engineering campaigns targeting customers and employees. Framed as a reference model for large-institution TD programs.

### Workflow: Intake → Triage → Containment → Takedown → Closure

```
[Intake]          [Triage]           [Containment]        [Takedown]         [Closure]
User report  ──►  Validate IOC  ──►  Block URL/mail  ──►  Abuse ticket  ──►  Metrics + ID.IM
ISAC feed         Campaign link       Purge inboxes        Registrar/host     Recurrence check
Brand monitor     Severity score      Reset creds          Social platform
Automated alert   Internal vs ext     DMARC review         Law enforcement (if warranted)
```

#### 1. Intake
- Channels: abuse@ mailbox, internal phish-report button, FS-ISAC, brand-monitoring SaaS, automated URL detonation alerts.
- Auto-create case ticket with timestamp, reporter, raw artifact (EML, URL, screenshot).

#### 2. Triage
- Parse email headers: `Authentication-Results`, `Received`, `Return-Path`, `Reply-To`.
- Evaluate **DMARC / DKIM / SPF** alignment — fail/pass informs spoof vs. look-alike classification.
- Correlate URL/domain against prior campaigns; assign severity (credential harvest active > benign spam).
- Decision: **TD-handled** (external brand abuse, no internal compromise) vs. **escalate to enterprise SOC/IR**.

#### TD vs. Enterprise SOC/IR Escalation Criteria

| Signal | Typical Owner |
|---|---|
| External look-alike domain; no internal mail delivery | Threat Disruptions |
| Phishing delivered to employee mailboxes; no confirmed click/compromise | TD + Email Security (contain) |
| Confirmed credential submission on internal account | **Escalate enterprise IR** |
| Endpoint malware, lateral movement, data exfil indicators | **Escalate enterprise IR** |
| Active fraud against customers (vishing/smishing using brand) | TD + Fraud + Comms; IR if backend access |
| Supply-chain partner compromise affecting org | **Escalate enterprise IR** + GV.SC contacts |

#### 3. Containment
- Block malicious URLs/domains at secure web gateway and DNS filtering.
- Search-and-destroy malicious messages across tenant mailboxes (M365 `Search-Mailbox` / compliance search patterns).
- Force password reset + session revoke for confirmed clickers.
- Publish internal advisory if wide-target campaign.

#### 4. Takedown
- Open abuse tickets with registrar, hosting provider, CDN, and platform (LinkedIn, Meta, etc.).
- Track **time-to-takedown** per provider; escalate via legal for non-responsive hosts.
- Document evidence package: screenshots, WHOIS, phishing kit hash, victim count estimate.

#### 5. Closure
- Verify URL/domain unreachable; confirm mail purge complete.
- Update detection rules (YARA, SIEM, email gateway).
- Record metrics; schedule recurrence check at 7/30 days.

### Email Authentication (DMARC / DKIM / SPF)
- **SPF:** authorize sending IPs; failures alone are weak signal (forwarding breaks SPF).
- **DKIM:** cryptographic domain signing; verify signature validity and domain alignment.
- **DMARC:** policy (`none` → `quarantine` → `reject`) + alignment checks; aggregate reports (`rua`) feed brand-abuse detection.
- TD teams use auth results to classify **exact-domain spoof** vs. **cousin/look-alike domain** — different takedown and comms paths.

### Brand-Abuse URL Disruption
- Monitor certificate transparency and newly registered domains (NRD) for brand strings.
- Sinkhole or block at resolver/proxy; initiate takedown for active credential harvest pages.
- Coordinate with fraud team when pages collect PII or payment data.

### SIEM / Email Correlation Concepts (Lab & Portfolio)
- **Index strategy:** separate sourcetypes for mail gateway, proxy, DNS, Entra sign-in, user-report API.
- **Campaign object:** common `url_domain`, `subject_hash`, `sender_fingerprint`, `first_seen` across events.
- **Join patterns:** user report timestamp → proxy log for same user → Entra sign-in from anomalous geo within window.
- **Useful searches:** spike in `reportphishing` submissions; new domain in URLs with >N recipients in 1 hour; DMARC fail + internal delivery.

---

## Threat Disruptions Metrics

| Metric | Definition | Why It Matters |
|---|---|---|
| **Time-to-takedown (TTT)** | Intake timestamp → confirmed unreachable or suspended by host | Direct customer-protection KPI; examiner and leadership visibility |
| **Phishing report-to-mitigation** | User report → URL blocked + mail purged from tenant | Measures internal protection speed |
| **Campaign recurrence** | Same TTP/domain family reappears within 7/30 days post-closure | Indicates incomplete eradication or detector gap |
| **False-positive rate** | Benign reports / total reports | Tuning signal for automation and user training |
| **Escalation rate** | TD cases escalated to enterprise IR / total cases | Boundary health between TD and IR teams |
| **MTTD / MTTR** | Mean time to detect / recover (program-level) | CSF 2.0 oversight and board reporting |

---

## Interview Talking Points (Threat Disruptions / Financial-Sector IR)

*Portfolio + aviation background: cite frameworks and lab work; never imply prior bank SOC or Wells Fargo employment.*

- **Frame IR as CSF 2.0 risk management, not a ticket queue:** SP 800-61r3 embeds incident response across Govern through Recover; Threat Disruptions-style work sits primarily in DE/RS for external brand abuse but must know when to escalate into full RS.AN/RS.MI for internal compromise — that boundary judgment is what the target role tests for.
- **Walk the phishing lifecycle with authentication context:** Intake from user reports and sector ISACs → triage using DMARC/DKIM/SPF and header forensics → contain via gateway block and mailbox purge → takedown with registrar/hosting → close with SIEM correlation (lab concepts) proving campaign scope and recurrence checks.
- **Speak financial-sector fluency without overclaiming:** Reference FFIEC CAT incident-management domains, FS-ISAC sharing norms, GLBA Safeguards alignment, and SEC materiality workflow as frameworks studied in this playbook — parallel to aviation: regulated environment, documented escalation, identity validation, not insider bank tenure.
- **Aviation → TD bridge (honest):** Eight years in federally regulated aviation security maps to procedural IR discipline, access control, and time-sensitive escalation — not to production Splunk or enterprise takedown queues. Portfolio projects demonstrate SIEM-style correlation and triage readiness.
- **Automation with guardrails:** SOAR playbooks for enrichment and repetitive containment; human approval for account disables, mass purge, and external comms. Idempotent actions, full audit trail — aligns with bank operational risk expectations.
- **Metrics that matter to leadership:** Time-to-takedown protects customers; report-to-mitigation protects employees; campaign recurrence exposes control drift. Tie improvements back to ID.IM so each incident makes the next one faster.

---

## References

- NIST SP 800-61 Rev. 3 (April 2025): [CSRC publication page](https://csrc.nist.gov/pubs/sp/800/61/r3/final)
- NIST CSF 2.0 (NIST CSWP 29, February 2024): [CSRC publication page](https://csrc.nist.gov/pubs/cswp/29/the-nist-cybersecurity-framework-csf-20/final)
- NIST Incident Response Project: [csrc.nist.gov/projects/incident-response](https://csrc.nist.gov/projects/incident-response)
- FFIEC Cybersecurity Assessment Tool: [ffiec.gov/cyberassessmenttool.htm](https://www.ffiec.gov/cyberassessmenttool.htm)
