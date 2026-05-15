# Incident Response Playbook — NIST SP 800-61 (CSF 2.0)

**Framework Reference:** NIST Special Publication 800-61 rev. 2 —
*Computer Security Incident Handling Guide.* Revised to reflect
**Cybersecurity Framework 2.0** (2024).

This playbook implements the four-phase NIST incident-handling lifecycle.
It is suitable for organizations operating under **federal compliance
regimes** (FISMA, FedRAMP), **healthcare** (HIPAA), or any context where
NIST alignment is the dominant requirement.

---

## 1. Preparation

### Establish Clear Roles and Responsibilities
Define specific cybersecurity roles:
- **Risk Manager** — owns the risk register and risk-acceptance decisions
- **Compliance Officer** — owns regulatory notification and audit-trail integrity
- **Incident Response Coordinator** — owns lifecycle execution from detection through closure
- **Technical responders** — endpoint, network, identity, application specialists
- **Communications lead** — internal and external messaging

Assign clear responsibilities for each role, ensuring coverage of all
cybersecurity aspects with no gaps and no overlapping authority that
could produce conflicting actions during a live incident.

### Expand and Integrate Toolsets
- Deploy advanced asset-management tools to automatically inventory
  and track all IT resources. An incident response is only as fast as
  the responder's ability to identify what is affected.
- Integrate risk-assessment software to proactively identify potential
  vulnerabilities before they become incident vectors.

### Enhance Communication Plans
- Create a comprehensive contact list for all key stakeholders and
  response teams. Maintain both primary and secondary contact methods
  for each party (in-band and out-of-band).
- Develop protocols for both internal and external communications
  during and after an incident, including pre-approved message
  templates for common scenarios.

### Comprehensive Training and Simulations
- Schedule regular training sessions on cybersecurity best practices
  for all employees.
- Conduct simulated attack scenarios (tabletop exercises, purple-team
  engagements, full-scale red-team simulations) to test and refine the
  incident-response process under realistic conditions.

---

## 2. Detection and Analysis

### Broaden Alert Mechanisms
- Utilize a combination of **signature-based** and **behavior-based**
  detection systems. Signatures catch known threats; behavior detects
  novel ones.
- Incorporate threat-intelligence feeds (commercial, government,
  industry-sharing) to stay updated on emerging threats and adversary
  tradecraft.

### Detailed Incident Analysis Procedures
- Utilize forensic tools to gather data and analyze the cause of the
  incident. Include endpoint, network, identity, and application
  telemetry in the analysis scope.
- Correlate incident data with external threat information to
  understand attack vectors, attribute the activity where possible,
  and anticipate likely follow-on actions.

### Standardize Incident Documentation
- Implement a template or software for recording all details of the
  incident consistently. Inconsistent documentation produces gaps that
  surface during legal review or post-incident audit.
- Ensure all team members are trained on how to document incidents
  accurately and thoroughly, including the chain-of-custody
  requirements for evidentiary artifacts.

---

## 3. Containment, Eradication, and Recovery

### Develop a Multi-Tier Containment Strategy
- **Immediate containment** — isolate affected systems quickly to halt
  active damage. Trade off forensic preservation against ongoing harm;
  for active ransomware or exfiltration, speed wins.
- **Secondary, long-term containment** — apply controls that prevent
  recurrence and further spread while permitting investigation and
  remediation work to continue.

### Eradication and System Restoration
- Detail the steps for thoroughly removing threats and restoring
  systems to operation. Eradication is not complete until the
  exploited vulnerability has been patched or compensating controls
  applied.
- Validate the integrity of data and systems before reconnecting
  them to the network. Returning a compromised system to production
  is the most common second-incident vector.

### Ongoing Validation and Feedback
- Regularly update recovery protocols based on new insights and
  feedback from recent incidents.
- Establish benchmarks for recovery time and effectiveness, adjusting
  strategies as needed. Track **MTTR** (Mean Time to Recovery) as a
  program-level metric.

---

## 4. Post-Incident Activity

### Structured "Lessons Learned" Sessions
- Hold debriefings with all involved parties after an incident to
  discuss what went well and what didn't. Conduct sessions under
  **blameless** protocol — the goal is system improvement, not
  individual accountability.
- Document insights and action items to improve future response
  efforts. Assign owners and due dates to each action item; an
  unowned improvement is an improvement that won't happen.

### Secure Evidence Retention and Comprehensive Reporting
- Define guidelines for securely storing digital forensic evidence.
  Retention period should be the longer of organizational policy,
  applicable regulatory minimum, or statute of limitations for any
  related legal proceeding.
- Generate detailed reports that summarize:
  - The incident itself (what happened, when, why)
  - The response effectiveness (what worked, what didn't, why)
  - Future prevention strategies (what changes follow from this incident)

---

## CSF 2.0 Alignment

This playbook implements the **Respond (RS)** and **Recover (RC)**
functions of the NIST Cybersecurity Framework 2.0:

| CSF 2.0 Function | Coverage in this Playbook |
|---|---|
| **GOVERN (GV)** | Roles and responsibilities (§1); communication plans (§1) |
| **IDENTIFY (ID)** | Asset management (§1); risk assessment (§1) |
| **PROTECT (PR)** | Training (§1); access controls referenced throughout |
| **DETECT (DE)** | Alert mechanisms (§2); analysis procedures (§2) |
| **RESPOND (RS)** | Containment, eradication (§3); communication (§3) |
| **RECOVER (RC)** | System restoration (§3); recovery validation (§3); lessons learned (§4) |
