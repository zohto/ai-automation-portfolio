# BREALLE
## AI Systems & Automation

---

# **Case Study: Applicant Intake & Re-Engagement at Production Scale**
### *Regional Home-Appliance Distributor · Tier 3 Production System*

---

## **The Situation**

A regional home-appliance distributor manages high-volume applicant flow for Entry Level Sales Representative and Appointment Setter roles across its territory.

The business had accumulated a large applicant backlog — the kind of operational pileup where every unprocessed applicant could mean a missed hire, fewer appointments set, fewer house calls, and delayed revenue opportunity.

Before the system was in place, applicant intake, qualification, and re-engagement followed a manual cycle:
- Data sat in spreadsheets waiting for review
- Follow-up depended on manual text messages and staff availability
- There was no consolidated view of who had been contacted, who had replied, or who had quietly dropped out
- Duplicates were handled by eye, not by logic
- Reply tracking required manually checking communication history

**Result:** the throughput of the hiring pipeline was bound to the manual capacity of whoever happened to be working the queue that day.

---

## **The Real Problem**

This wasn't a hiring problem. It was a **conversion failure between applicant intake and active engagement.**

Each unprocessed applicant represented a decayed opportunity. Every day of delay made a re-engagement message less effective. A missed reply meant a candidate quietly fell out of the funnel. The business couldn't process the leads it was already generating — let alone scale to handle more.

---

## **The System BREALLE Built**

**Regional Distributor Applicant Pipeline v5 PROD** — a three-chain automation that runs continuously on a hardened production VPS, processing incoming applicant records from raw intake through outreach, reply tracking, and pipeline state management.

**Status:** Live · Production · Tier 3 governance applied
**Scale:** 82 nodes across three independent scheduled chains plus a built-in error subworkflow

---

## **System Architecture**

### **Chain A — Intake & Qualification**
Pulls raw applicant rows from the intake sheet, dedupes against the master pipeline using generated keys, normalizes fields, applies decision logic, and writes both to the master pipeline and to a human-review queue. Duplicates aren't silently dropped — they're routed through a dedicated logging branch and recorded before the chain merges back to the main path.

### **Chain B — Outreach (Re-Engagement)**
Pulls approved candidates from the review queue, builds personalized re-engagement emails, enforces a daily send cap so the system never exceeds Gmail throughput limits, sends through Gmail with 3-minute pacing between messages, captures the thread ID for downstream reply matching, and logs every send.

### **Chain C — Reply Handling**
Runs on a 15-minute schedule. Pulls active threads from the pipeline, fetches new replies from Gmail by thread ID, matches each reply back to the original candidate, decides whether to respond, sends a threaded reply (also under daily cap), updates pipeline stage and review queue, and logs the chain.

### **Error Subworkflow — Failure Logging & Halt Handling**
Built-in error trigger subworkflow. Any failure in any chain routes to a structured error log entry with chain identifier, timestamp, and error context.

---

## **Operational Controls**

These are the controls that distinguish a production system from a demo:

- **Daily send cap enforcement** (Chains B and C) — the system reads its own LOGS sheet to count sends-so-far-today and skips if at cap, marking the row as queued for tomorrow rather than dropping it
- **Halt-on-error circuit breaker** — every Gmail send is wrapped in error classification logic; classified failures halt the chain and write a halt-log entry instead of cascading
- **3-minute pacing waits** between sends to respect rate limits, reduce burst behavior, and protect deliverability
- **Field Preservation Gate** — explicit candidate-payload restoration through transforming nodes, addressing the n8n pattern where Code/AI/HTTP nodes silently drop upstream fields
- **Deduplication with full audit trail** — every duplicate is logged before being merged out
- **Audit logging at every chain** — RAW intake, pipeline writes, duplicates, sends, halts, replies, and errors all land in a single LOGS sheet

---

## **Governance**

The system is governed under BREALLE's Workflow Governance Standard (WGS) v1 at **Tier 3** — BREALLE's highest-risk workflow category, used for external communications with low reversibility.

Tier 3 controls applied:
- Field Preservation Gate (required)
- Audit logging required at every external touch
- Manual approval gate (REVIEW_QUEUE) before any outbound send
- Documented rollback procedure
- Halt-on-error behavior with classified failure modes

---

## **Production Footprint**

| Layer | Implementation |
|---|---|
| Orchestration | n8n on hardened VPS |
| Reverse proxy + TLS | Caddy with managed TLS |
| State | Postgres-backed n8n instance |
| Hardening | Hardened Linux server, key-based access, firewall enforced |

---

## **What This Replaces**

- ✗ Manual checking of the applicant sheet each day
- ✗ Memory-based decisions about who to contact next
- ✗ Manual text-message follow-up without centralized state tracking
- ✗ Untracked duplicate handling
- ✗ Scattered visibility into who replied, who needed review, and who needed next-step action

## **What's Now Possible**

- ✓ Continuous, unattended applicant capture
- ✓ Consistent re-engagement cadence with cap-respecting throughput
- ✓ Complete audit trail of every action — no silent drops
- ✓ Reply matching without manual thread tracking
- ✓ Production-grade failure handling with documented halt behavior

---

## **Key Insight**

> The constraint was never applicant volume.
> 
> It was the manual layer between intake and engagement.

---

## **Positioning Statement**

> Regional Home-Appliance Distributor's hiring throughput wasn't capped by applicants.
> 
> It was capped by how fast the team could move Entry Level Sales Representative and Appointment Setter candidates through the funnel.
> 
> Replace the manual layer with a governed automation system, and applicant intake stops being a backlog problem and becomes a managed recruiting pipeline.

---

## **About BREALLE**

BREALLE designs and operates production automation systems for businesses where revenue depends on inbound capture, intake, follow-up, and tracking.

- **Lead Loss Diagnostic** — identifies where opportunities are leaking
- **Integration Sprint** — builds the system that closes the gap
- **Maintenance Retainer** — keeps it running

Ready to find where your pipeline is leaking? Start with a Lead Loss Diagnostic.

[brealle.com](https://brealle.com) · [brandon@brealle.com](mailto:brandon@brealle.com)

---

**Brandon Robinson**
Founder, BREALLE
