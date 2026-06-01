# BREALLE
## AI Systems & Automation

---

# **Case Study: Applicant Intake & Re-Engagement at Production Scale**
### *Regional Home-Appliance Distributor · Tier 3 Production System*

---

## **The Situation**

A regional home-appliance distributor was losing hiring opportunities every day — not because applicants weren't applying, but because the team couldn't keep up with them.

Applicant data sat unreviewed in spreadsheets. Follow-up depended on whoever had time to send a text. Nobody had a clear picture of who had been contacted, who had replied, or who had already moved on. The pipeline wasn't moving because the manual layer between "applicant applies" and "applicant gets contacted" was the bottleneck.

Every day of delay was a candidate lost to a competitor or to silence.

---

## **The Real Problem**

This wasn't a hiring volume problem. The applicants were there.

The business was losing candidates between intake and first contact — a gap that no amount of job posting spend could fix. The pipeline needed to move on its own, without depending on manual bandwidth that was already maxed out.

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

> Most hiring pipelines don't fail because of bad candidates. They fail because the gap between application and first contact is too slow, too manual, and too dependent on someone remembering to follow up.
>
> BREALLE builds the system that closes that gap — so the pipeline runs whether or not someone is working the queue that day.

---

## **About BREALLE**

BREALLE designs and operates production automation systems for businesses where revenue depends on inbound capture, intake, follow-up, and tracking.

- **Lead Loss Snapshot** — identifies where opportunities are leaking
- **Lead Recovery Setup** — builds the system that closes the gap
- **Managed Lead Recovery** — keeps it running

Ready to find where your pipeline is leaking? Start with a **Lead Loss Snapshot**.

[brealle.com](https://brealle.com) · [brandon@brealle.com](mailto:brandon@brealle.com)

---

**Brandon Robinson**
Founder, BREALLE
