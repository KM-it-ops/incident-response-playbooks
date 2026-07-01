# Incident Response Playbook — ISO/IEC 27035

**Last reviewed:** 2026-07-01

**Framework Reference:** ISO/IEC 27035-1:2023 — *Information security incident
management* Part 1 (supersedes ISO/IEC 27035-1:2016; series also includes
Parts 2–3 for plan/prepare and response operations guidance)

This playbook implements the five-phase incident-management lifecycle
specified by **ISO/IEC 27035-1:2023** (Part 1 — principles and process;
supersedes ISO/IEC 27035-1:2016). Documentation and evidence handling is
**cross-cutting** per ISO 27035-1 Section 4.7 — not a sixth phase. It is
suitable for organizations operating
under **ISO/IEC 27001:2022** information-security management systems or any
regulated context where ISO alignment is required (international
operations, EU-aligned regulatory regimes, ISO-certified supply chains).

**Scope note:** This is a reference playbook from the author's IR library —
not a production runbook from a specific employer. Adapt role names,
escalation paths, and regulatory triggers to your org chart and counsel.

---

## NIST CSF 2.0 Crosswalk

Use this table when auditors, partners, or internal stakeholders ask how
ISO 27035 phases map to **NIST Cybersecurity Framework 2.0** functions.
Both frameworks describe the same work; the labels differ.

| ISO/IEC 27035-1:2023 Phase | Primary CSF 2.0 Function | Secondary CSF 2.0 Functions | Operational focus |
|---|---|---|---|
| **1. Plan and Prepare** | **GV** Govern | ID, PR | Policy, roles, tooling, training, playbooks, third-party IR contacts |
| **2. Detect and Report** | **DE** Detect | PR | SIEM/EDR alerts, user reports, threat-intel hits, anomaly detection |
| **3. Assess and Decide** | **DE** Detect | RS, GV | Triage, severity scoring, scope confirmation, response authorization |
| **4. Respond** | **RS** Respond | RC, PR | Containment, eradication, recovery, stakeholder communication |
| **5. Learn Lessons** | **ID** Identify (ID.IM) | GV | Blameless review, control gaps, detection tuning, policy updates |
| **Documentation & evidence** *(cross-cutting, §4.7)* | **RS** Respond | GV, RC | Case records, chain of custody, regulatory packages — maintained in every phase |

**Quick read for panel questions:** Prepare = GV+PR. Detect/Assess = DE
bleeding into RS. Respond = RS (+ RC for restoration). Learn lessons =
ID.IM under GV oversight. Document throughout — not a separate close-out phase.

---

## Severity Matrix (P1–P4)

Assign severity at **Assess and Decide** (Phase 3). Re-score when scope
changes — a P3 that turns out to involve customer PII becomes P1 fast.

| Level | Label | Criteria (any one triggers) | Initial response target | Escalation |
|---|---|---|---|---|
| **P1** | Critical | Active data exfiltration; ransomware affecting production; widespread outage; confirmed compromise of privileged identity; regulatory notification likely | IR lead + Legal/Compliance within **15 min**; exec bridge optional | Full IR team, external counsel, regulator path per annex |
| **P2** | High | Confirmed malicious activity on critical system; limited exfiltration suspected; BEC with wire-transfer attempt; DDoS affecting customer-facing service | IR coordinator within **30 min**; tier-2 SOC engaged | IR lead, business owner, Legal if customer/regulator impact |
| **P3** | Medium | Contained malware on non-critical host; phishing click without credential compromise; policy violation with audit trail | Tier-2 SOC / IR analyst within **2 hr** | Document; escalate if scope expands |
| **P4** | Low | Blocked attack; false positive after validation; informational intel match with no internal footprint | SOC closure with ticket notes | Weekly trend review only |

Severity drives **RACI activation depth**, not just urgency. A P4 closed
wrong poisons MTTD metrics; a P1 under-scored burns containment time.

---

## RACI — Core IR Functions

Customize names to your org. Functions stay stable across frameworks.

| Activity | IR Lead | SOC Tier-1 | SOC Tier-2 / Threat | Legal / Compliance | Business Owner | Comms |
|---|---|---|---|---|---|---|
| Alert validation | I | **R** | C | — | — | — |
| Severity assignment | **A** | C | **R** | C | I | — |
| Containment authorization | **A** | I | **R** | C | C | — |
| Evidence collection | **A** | I | **R** | C | — | — |
| External notification | C | — | I | **A/R** | I | C |
| Customer/regulator comms | C | — | — | **A** | C | **R** |
| Post-incident review | **R/A** | C | C | C | C | I |
| Playbook / control updates | **A** | C | C | C | I | — |

**R** = Responsible · **A** = Accountable · **C** = Consulted · **I** = Informed

Handoff rule: SOC owns **validation and correlation** until severity ≥ P2 or
containment is required — then IR Lead owns the case record regardless of
who executes the technical action.

---

## Containment vs. Preservation Decision Tree

Wrong choice here loses court-admissible evidence or lets an adversary
keep moving. Decide in Phase 3; revisit after every major action.

### Ransomware

```
Alert: encryption or ransom note observed
├─ Active encryption spreading? → CONTAIN NOW (isolate VLAN, disable account)
│   └─ Snapshot volatile data if < 5 min; do not wait for full imaging
├─ Single host, encryption complete, no lateral movement? → PRESERVE
│   └─ Network isolate + memory capture + disk image before reboot
└─ Backup integrity unknown? → CONTAIN + preserve; do not mass-restore
    until scope confirmed
```

### Business Email Compromise (BEC)

```
Suspected BEC / wire fraud
├─ Transfer not yet sent? → CONTAIN (hold payment, lock mailbox rules,
│   reset creds, preserve headers + mailbox audit log)
├─ Transfer sent? → PRESERVE + escalate Legal immediately; do not delete
│   mailboxes or rules until counsel signs off
└─ Attacker still in mailbox? → Short-term contain (session kill, rule block)
    while preserving O365/GWS audit exports
```

### Insider Threat

```
Privileged user anomaly (data staging, off-hours bulk access)
├─ Active exfil in progress? → CONTAIN (disable session, block egress)
│   └─ HR/Legal parallel track — do not tip off via visible lockout
│       without workforce policy alignment
├─ Historical access only? → PRESERVE (enable enhanced logging, preserve
│   DLP hits, defer account action until scope mapped)
└─ Termination scenario? → Follow workforce playbook; preserve before
    access removal when policy allows
```

### DDoS

```
Availability attack on customer-facing property
├─ Attack ongoing? → CONTAIN via edge mitigation (scrubbing, rate limits,
│   geo block) — preservation is secondary to uptime
├─ Attack subsided? → PRESERVE (flow logs, WAF hits, PCAP samples if
│   captured) for attribution and trend analysis
└─ Combined with breach indicators? → Treat as P1/P2; do not assume
    DDoS is distraction-only without assessment
```

**Default bias:** If you cannot decide in **10 minutes**, short-term contain
and preserve what you can in parallel. Explain the tradeoff in the case
timeline.

---

## SOC Operations — Alert to IR Handoff

This section bridges **Detect and Report** (Phase 2) and **Assess and
Decide** (Phase 3). It reflects common SOC operating patterns — adapt to
your org; this is playbook design, not a claim of production SOC tenure.

### Workflow: Validation → Correlation → Hypothesis → Escalation

1. **Alert validation (Tier-1)**
   - Confirm the alert is tied to a real entity (host, user, IP), not a
     parser error or stale asset inventory.
   - Check suppression rules and change windows — was this a known deploy?
   - Outcome: *True Positive*, *Benign True Positive*, or *False Positive*
     with documented reason code.

2. **Correlation (Tier-1 → Tier-2)**
   - Pivot on user, host, process hash, destination IP, JA3, cloud session ID.
   - Pull **7–30 day** lookback for same indicators (adjust to retention policy).
   - Enrich with threat intel (commercial, ISAC, internal disruption feeds).

3. **Hypothesis (Tier-2 / Threat Intel)**
   - State the working hypothesis in one sentence: *"Likely credential theft
     via phishing leading to mailbox rule creation."*
   - List disconfirming evidence needed before closure.
   - Map to MITRE ATT&CK tactics if your tooling supports it — optional but
     useful for handoff consistency.

4. **Escalation**
   - **Stay in SOC:** P4, closed BTP, blocked single-stage malware with no
     lateral movement.
   - **Tier-2 owns:** P3 with clear scope, no containment beyond host isolate.
   - **IR handoff (P2+):** Active adversary, data at risk, regulatory trigger,
     or executive/customer impact. Open IR case; SOC stays on comms bridge.

### Tier Handoff Checklist (SOC → IR)

When escalating, the SOC ticket must include:

- UTC timeline of first alert → validation → correlation
- Affected assets (hostname, IP, user UPN, cloud resource ID)
- Severity recommendation with rationale
- Actions already taken (isolate Y/N, cred reset Y/N)
- Evidence pointers (SIEM search IDs, EDR investigation links)
- Open hypothesis and what is still unknown

IR should not re-triage from scratch. If the checklist is incomplete, send
it back — fixing handoff quality is cheaper than duplicate work mid-incident.

### Threat Intel ↔ SOC ↔ IR Coordination

| Touchpoint | Threat Intel / Disruption | SOC | IR |
|---|---|---|---|
| **Proactive** | Publish disruption guidance (block lists, hunt queries, TTP briefs) | Tune detections; run hunts | Update playbooks; tabletop scenarios |
| **During incident** | Attribute TTPs; suggest containment targets | Execute blocks/isolations; monitor for re-entry | Authorize scope; own comms and legal path |
| **Post-incident** | Feed IOCs into disruption pipeline | Close loop on detection gaps | Track remediation actions to closure |

Threat intel work **feeds** the SOC; IR **consumes** outcomes when an
incident crosses severity threshold. Keep the lanes clear: disruption teams
hunt and harden; IR owns lifecycle once impact is confirmed.

---

## Financial Services IR Annex

Use this annex when the organization is subject to **GLBA**, **FFIEC**
guidance, OCC/Federal Reserve supervision, or state banking/data-breach
law. This is illustrative — **confirm notification thresholds with counsel**.

### FFIEC-Aligned Classification

FFIEC expects institutions to define **their own** severity thresholds and
escalation paths — it does not publish a universal P1–P4 or
Material/Significant taxonomy. Map internal severity to exam-friendly
language **your org defines** (illustrative mapping below):

| Internal | Illustrative exam-facing label | Typical exam question |
|---|---|---|
| P1 | **Material** — customer impact, safety/soundness, or systemic availability | "Was this reported to the board? What was MTTR?" |
| P2 | **Significant** — confined to critical system, no confirmed customer data loss | "Show containment decision and evidence chain." |
| P3 | **Moderate** — limited scope, no regulatory trigger | "How was this distinguished from noise?" |
| P4 | **Low / Event** — blocked or informational | "Trend data and control effectiveness." |

Document **why** a case stayed below material — examiners read downgrades.
For federal **notification incidents**, use the statutory definition (material
disruption/degradation of critical operations) — not this internal table alone.

### Regulatory Notification Triggers (Decision Inputs)

Escalate to Legal/Compliance when **any** apply (non-exhaustive). **Which
rule applies depends on entity type** — do not conflate them in interviews:

| Regime | Who it covers | Trigger (simplified) | Timing |
|---|---|---|---|
| **OCC / FDIC / FRB** (12 CFR Part 53 et al.) | Federally supervised **banks** | **Notification incident** — computer-security incident that materially disrupted/degraded critical operations, business lines, or customer delivery | As soon as possible, **≤ 36 hours** after determination |
| **FTC Safeguards Rule** (GLBA, 16 CFR 314) | **Non-bank** financial institutions under FTC jurisdiction (mortgage brokers, auto dealers, payday lenders, etc.) | Unauthorized acquisition of **unencrypted customer information** for **≥ 500** consumers | **≤ 30 days** after discovery, to FTC |
| **State breach law** | Varies | Customer PII exposure thresholds per state | Per statute |

Common escalation signals (any regime):

- Unauthorized access to **customer NPI** (names + SSN/account, or other
  GLBA-covered fields)
- Service disruption affecting customer transactions beyond defined RTO
- Third-party / vendor breach with potential access to your customer data
- Law-enforcement or regulator inquiry tied to the event
- Media inquiry or social signal suggesting public exposure

**Do not self-notify regulators from the SOC.** Legal owns timing, content,
and channel. Technical teams supply facts, timeline, and scope drafts.

### Legal / Compliance Escalation Path

1. IR Lead notifies Compliance **within SLA for severity** (see P1–P4 table).
2. Compliance triages: regulatory notification, law enforcement, customer
   notice, credit monitoring, SEC 8-K (if applicable — public parent entity).
3. Preserve **privilege** where counsel directs — separate technical fact
   collection from attorney work product.
4. No external statement without Comms + Legal approval.

### Evidence Retention for Regulatory Exam

| Artifact | Minimum retention guidance | Notes |
|---|---|---|
| IR case record + timeline | Per org records policy (banks often **5–7 years**; not a single FFIEC mandate) | UTC timestamps; version changes logged |
| SIEM raw logs supporting the case | Per log retention policy; **extend hold** on legal hold | Immutable storage where available |
| Chain-of-custody forms | Life of matter + per org records policy | Hash values at collection |
| Containment change tickets | Per org records policy | Tie to CAB/emergency change process |
| Post-incident action items | Until closed + per org policy | Examiners ask for closure proof |

Place legal hold **before** bulk log rotation. Rotating evidence you later
need is an exam finding, not a technical footnote.

---

## IR Metrics and Continuous Improvement

Track these at **Learn Lessons** (Phase 5). Report monthly to leadership;
review trends quarterly.

| Metric | Definition | Target (tune per org) |
|---|---|---|
| **MTTD** | Mean time from adversary action (or first observable) to confirmed detection | Trend down quarter-over-quarter |
| **MTTR** | Mean time from confirmed incident to containment (or service restoration for availability events) | P1: < 4 hr · P2: < 8 hr (starting points) |
| **Tabletop cadence** | Full-scale or functional IR exercise | **≥ 2 per year**; include Legal/Comms in one |
| **Post-incident actions** | % of remediation items closed within SLA | **≥ 90%** within 90 days |
| **Escalation quality** | % of IR handoffs passing SOC checklist on first transfer | **≥ 95%** |
| **False positive rate** | Closed alerts / total alerts (by use case) | Tune detections; do not game by over-closing |

Every P1/P2 gets a **blameless post-incident review** within 10 business days.
Action items enter the same tracker as vulnerability remediation — if they
sit in a slide deck, they did not happen.

---

## 1. Plan and Prepare

### Incident Management Policy
Develop policies that define the management of information-security
incidents, the roles involved, and the responsibilities each role
carries. The policy is the authoritative source under which every
subsequent phase operates. ISO 27035-1:2023 expects alignment with
**ISO 27001:2022** Clause 8 and Annex A controls for incident management.

### Competence and Awareness
Ensure all participants in incident management are trained on their
roles and aware of the escalation paths, communication protocols, and
authority boundaries that apply to them. Include SOC analysts, threat
hunters, and third-party MSSP staff if in scope.

### Incident Response Tools
Prepare and maintain a toolkit for incident response, including:
- **Forensic tools** for evidence collection and analysis
- **Communication channels** that remain operational during an incident
  (out-of-band where possible)
- **Documentation templates** for consistent case capture
- **Network and endpoint isolation capabilities** ready for immediate
  invocation
- **Runbooks** for top scenarios (ransomware, BEC, insider, DDoS) linked
  to the containment/preservation trees above

---

## 2. Detect and Report

### Detection Mechanisms
Implement mechanisms for the early detection of incidents:
- Intrusion Detection Systems (IDS) at the network perimeter and key
  internal segmentation points
- Log management with centralized SIEM correlation
- Anomaly detection systems (statistical and behavioral)
- Endpoint telemetry feeds from EDR platforms
- Threat-intelligence and disruption feeds mapped to detection logic

### Incident Reporting
Establish a straightforward, low-friction process for reporting
incidents. Reporting must be accessible to:
- All internal employees
- Contractors and third-party personnel with system access
- External parties (customers, partners, regulators) where the
  organization's risk profile requires it

Reporting friction is the single largest predictor of detection
latency. A clear single-pane reporting path matters more than the
sophistication of the tooling behind it.

---

## 3. Assess and Decide

### Incident Assessment
Assess incidents to determine:
- **Severity** — use P1–P4 matrix; impact on confidentiality, integrity, availability
- **Scope** — affected systems, data classifications, user populations
- **Category** — predefined taxonomy (malware, unauthorized access, data
  exfiltration, denial of service, insider, BEC, etc.)

### Response Decision
Decide on appropriate response actions based on the incident's
category and severity. Apply the **containment vs. preservation**
decision tree before executing. The decision authority must be
specified in advance; ambiguity at this step produces minutes of
delay that compound into hours of damage.

---

## 4. Respond

### Containment
Take immediate action to isolate affected systems and prevent further
spread. Containment strategies include:
- **Short-term containment** — disconnect, block, or quarantine affected
  endpoints/accounts to halt active damage
- **Long-term containment** — apply more durable controls (network
  segmentation, credential rotation) that allow continued investigation
  without ongoing risk exposure

### Eradication and Recovery
Remove the causes of the incident, repair affected systems, and return
to normal operations with minimal downtime. This phase includes:
- Malware removal and persistent-foothold elimination
- Vulnerability patching for the exploited weakness
- System restoration from validated clean backups
- Integrity validation before returning systems to production

### Communication
Keep internal and external stakeholders informed throughout the
incident-management process. Communication discipline during an
incident is as important as technical response — leadership,
legal, communications, customers, and (where required by regulation
or contract) regulators must all receive timely, accurate updates
through pre-defined channels.

---

## 5. Learn Lessons

### Post-Incident Review
Analyze the incident and the effectiveness of the response to
identify improvements. The review should be **blameless**, focused on
systemic causes rather than individual mistakes; this is the only
posture that produces honest reporting and durable improvement.

### Continuous Improvement
Update policies, procedures, and controls based on lessons learned
to strengthen future incident-response capabilities. Improvements
typically fall into four categories:
- **Detection** — coverage gaps that delayed identification
- **Response** — workflow friction that delayed action
- **Prevention** — root-cause weaknesses that should be patched
- **Governance** — policy or authority gaps that surfaced during execution

Feed metrics (MTTD, MTTR, action closure) back into ISMS management
review per ISO 27001:2022.

---

## Documentation and Evidence (Cross-Cutting)

ISO 27035-1:2023 treats documentation as a capability requirement (Section
4.7) spanning all phases — event reports, incident logs, incident reports,
and the incident register. The guidance below applies continuously, not only
after response closes.

### Documentation
Keep detailed records of the incident, its analysis, and the response
for accountability, legal proceedings, and learning purposes. Records
should capture:
- Timeline (UTC timestamps for every significant event)
- Actions taken and by whom
- Systems and data affected
- Communication log (who was notified, when, by what channel)
- Final root cause and remediation

### Evidence Handling
Ensure proper collection, handling, and storage of evidence for
potential legal action or further investigation. Maintain **chain
of custody** documentation. Store evidence in tamper-evident
locations with documented access logs. Retention duration should
follow the longer of (a) organizational policy, (b) regulatory
requirement (see Financial Services Annex), or (c) statute applicable
to any related legal proceeding.

---

## Interview Talking Points (Portfolio-Safe)

**Use these as framework fluency — cite the playbook/library, not employer
war stories.** Pair with aviation or portfolio examples where you have real
depth (ops discipline, checklists, escalation under time pressure).

- **Framework fluency:** "In my IR playbook I align work to ISO 27035-1's
  five phases and explain it to leadership through NIST CSF 2.0 —
  Govern/Detect/Respond is the language audit and risk committees use."
- **SOC-to-IR handoff:** "My escalation bar in the playbook is
  evidence-backed severity, not alert volume. P2+ means a completed handoff
  checklist — hypothesis, timeline, actions taken — so IR does not re-triage
  under fire."
- **Threat intel / disruption value:** "Upstream intel shortens MTTD when
  hunt queries and blocks feed SOC workflows before incidents mature — I
  frame that as Detect, not a separate silo."
- **Financial services judgment:** "For regulated environments I separate
  technical facts from notification decisions — Legal owns regulator timing;
  technical teams deliver scope, NPI impact assessment, and evidence on
  legal hold. Bank notification incidents (36-hour) and FTC Safeguards
  (non-bank, 500+ consumers) are different regimes."
- **Containment tradeoffs:** "For ransomware I bias to isolate fast; for BEC
  with sent wires I bias to preserve mailboxes and audit logs first. The
  decision tree is scenario-specific, not one-size-fits-all."
