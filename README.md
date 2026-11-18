# Incident Response Playbook Library

Cross-framework incident-response playbooks designed for organizations
operating under multiple compliance regimes simultaneously. Both
playbooks cover the full IR lifecycle and are intentionally aligned so
the same operational patterns apply across regulated industries —
**finance, healthcare, and federal contractors** in particular.

## Why dual-framework

Most organizations operate under more than one compliance standard.
A financial services firm processing healthcare data may be subject
to **GLBA**, **HIPAA**, **PCI-DSS**, **SOX**, and state breach-notification
law simultaneously. Building one playbook against one framework and
hoping it covers the rest is how compliance gaps become incident
post-mortems.

This library publishes two complete playbooks — one mapped to **ISO/IEC
27035:2023**, one to **NIST SP 800-61 rev. 2** (revised to reflect
**CSF 2.0**) — and aligns them at the phase level so an organization can
operate from either framework's authoritative source without rewriting
the operational procedure.

The ISO playbook includes a **NIST CSF 2.0 crosswalk** (GV/ID/PR/DE/RS/RC),
a **Financial Services IR Annex** (FFIEC-aligned classification, GLBA/OCC
notification inputs, exam-ready evidence retention), and a **SOC operations
section** covering alert validation through IR handoff.

## Contents

| File | Framework | Authoritative Reference |
|---|---|---|
| [`iso-27035-playbook.md`](iso-27035-playbook.md) | ISO/IEC 27035:2023 | *Information security incident management* (supersedes 27035:2016) |
| [`nist-800-61-playbook.md`](nist-800-61-playbook.md) | NIST SP 800-61 rev. 2 + CSF 2.0 | *Computer Security Incident Handling Guide*, revised to reflect Cybersecurity Framework 2.0 |
| [`sources/`](sources/) | Original Word documents | For download / archival |

## Phase alignment

Both playbooks cover the same operational lifecycle under slightly
different phase nomenclature:

| ISO/IEC 27035:2023 phase | NIST SP 800-61 phase | CSF 2.0 (primary) |
|---|---|---|
| Plan and Prepare | Preparation | GV, PR |
| Detection and Reporting | Detection and Analysis | DE |
| Assessment and Decision | Detection and Analysis (continued) | DE, RS |
| Responses (Containment, Eradication, Recovery) | Containment, Eradication, and Recovery | RS |
| Lessons Learned and Improvement | Post-Incident Activity | GV, RC |
| Documentation and Evidence | Post-Incident Activity (continued) | RS, RC |

The phase mapping is what makes dual-framework operation tractable:
once a team is fluent in one playbook, the second is a relabeling
exercise, not a relearning one. See the full crosswalk table in
[`iso-27035-playbook.md`](iso-27035-playbook.md).

## How to use

1. **Pick the framework your dominant compliance regime cites.** If audited
   primarily against ISO 27001:2022, start with the ISO playbook.
2. **Walk the lifecycle once during a tabletop exercise** before relying
   on it in a live incident.
3. **Customize the role assignments** (Risk Manager, Compliance Officer,
   IR Coordinator, SOC tiers) to your org chart — the playbooks specify the
   functions; you specify the people.
4. **Review quarterly.** Frameworks evolve (27035:2023 superseded 2016;
   CSF 2.0 replaced CSF 1.1 in 2024); your playbook should evolve with them.

---

**License:** MIT — see [LICENSE](LICENSE).

**Author:** Mahmoud Al Kurdi · [LinkedIn](https://www.linkedin.com/in/mahmoud-al-kurdi-it/) · [Portfolio](https://km-it-ops.github.io) · [GitHub](https://github.com/KM-it-ops)
