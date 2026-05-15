# Incident Response Playbook — ISO/IEC 27035

**Framework Reference:** ISO/IEC 27035:2016 — *Information technology —
Security techniques — Information security incident management*

This playbook implements the six-phase incident-management lifecycle
specified by ISO/IEC 27035. It is suitable for organizations operating
under **ISO/IEC 27001** information-security management systems or any
regulated context where ISO alignment is required (international
operations, EU-aligned regulatory regimes, ISO-certified supply chains).

---

## 1. Plan and Prepare

### Incident Management Policy
Develop policies that define the management of information-security
incidents, the roles involved, and the responsibilities each role
carries. The policy is the authoritative source under which every
subsequent phase operates.

### Competence and Awareness
Ensure all participants in incident management are trained on their
roles and aware of the escalation paths, communication protocols, and
authority boundaries that apply to them.

### Incident Response Tools
Prepare and maintain a toolkit for incident response, including:
- **Forensic tools** for evidence collection and analysis
- **Communication channels** that remain operational during an incident
  (out-of-band where possible)
- **Documentation templates** for consistent case capture
- **Network and endpoint isolation capabilities** ready for immediate
  invocation

---

## 2. Detection and Reporting

### Detection Mechanisms
Implement mechanisms for the early detection of incidents:
- Intrusion Detection Systems (IDS) at the network perimeter and key
  internal segmentation points
- Log management with centralized SIEM correlation
- Anomaly detection systems (statistical and behavioral)
- Endpoint telemetry feeds from EDR platforms

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

## 3. Assessment and Decision

### Incident Assessment
Assess incidents to determine:
- **Severity** — impact magnitude on confidentiality, integrity, availability
- **Scope** — affected systems, data classifications, user populations
- **Category** — using predefined taxonomy (malware, unauthorized
  access, data exfiltration, denial of service, insider, etc.)

### Response Decision
Decide on appropriate response actions based on the incident's
category and severity. The decision authority must be specified in
advance; ambiguity at this step produces minutes of delay that
compound into hours of damage.

---

## 4. Responses

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

## 5. Lessons Learned and Improvement

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

---

## 6. Documentation and Evidence

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
follow the longer of (a) organizational policy or (b) the statute
applicable to any related legal proceeding.
