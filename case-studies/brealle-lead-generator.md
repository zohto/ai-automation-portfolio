# BREALLE
## AI Systems & Automation

---

# **Case Study: Outbound Lead Sourcing & Enrichment at Production Scale**
### *BREALLE Lead Generator · Tier 2 Production System*

---

## **The Situation**

BREALLE operates on outbound — finding small businesses that are losing revenue through broken intake, and reaching them with a credible offer.

For that motion to work, the sourcing pipeline behind it has to do three things continuously, under cost control:

- Discover candidate firms inside a configured vertical — currently trades and home services (plumbing, HVAC, electrical, restoration) across a New England primary geography
- Resolve a verified, deliverable contact email for each firm — without burning enrichment credits on dead records
- Hand the result to the outreach engine in a structured, governed shape so nothing leaks between sourcing and the next stage

Before the system existed, this was a manual cycle: search, copy, paste, check, retry, re-verify — and the unit economics didn't work for a one-person operation running against a **metered monthly discovery budget**.

---

## **The Real Problem**

This wasn't a sourcing volume problem. It was an **economics-and-trust problem** between sourcing and downstream outreach:

- Every wasted enrichment credit was money out of the operating budget
- Every undeliverable email risked the sender reputation the outreach engine depends on
- Every record sitting in an ungoverned spreadsheet was a candidate for double-sending, missed dedup, or a "Hi {first_name}" disaster

The pipeline needed to be **cost-aware, deliverability-aware, and audit-traceable from day one.**

---

## **The System BREALLE Built**

**BREALLE Lead Generator** — an n8n-orchestrated sourcing and enrichment pipeline that runs on the BREALLE production n8n instance and feeds verified, deduplicated leads into the outreach engine.

**Status:** Live · Production · Validated & Operational
**Tier:** Tier 2 governance (operational/revenue-support, BREALLE WGS v1)
**Scale:** Five coordinated workflows totaling 87 nodes, verified against the running instance 2026-08-04

The function — outbound lead sourcing and enrichment — runs continuously today. The discovery layer has been rebuilt more than once as the economics were measured: Apify-based scraping first, then Apollo-based discovery and enrichment, and today a mixed layer that uses whichever source actually yields deliverable addresses. The five workflows described below are the stable core; the wider sourcing family currently runs eight active workflows totalling 163 nodes.

---

## **System Architecture**

### **Discovery — Apollo Discovery v3**
Pulls candidate firms from Apollo using per-vertical ICP rulesets (industry, headcount band, geography). Writes structured rows into the lead pipeline sheet with sourcing metadata: who pulled, when, which vertical, which ruleset matched.

### **Enrichment — address resolution**
For each discovered firm, resolves a contact address from the strongest available source. A domain-lookup vendor was trialled as a fallback for firms that route inbound through contact forms and was **not adopted** — measured against the target profile it returned a usable address for roughly 7% of the domains tested, which did not justify the subscription. Recording that is the point: the fallback looked obviously worth buying until it was measured.

### **Verification — NeverBounce Verification Gate**
Every resolved email passes through NeverBounce verification before it lands in the active outreach pool. Records that fail the deliverability classification are routed to an exclusion path with a logged reason rather than reaching the outbound stage.

### **Dedup & Credit-Budget Logic**
Every new candidate is keyed against the existing pipeline before being appended. A gap-aware lead-cap mechanism manages the monthly discovery budget across cycles — the pipeline self-throttles as it approaches its ceiling rather than blowing through it mid-month.

### **Structured Handoff**
Verified, deduplicated leads land in a schema-locked Google Sheets pipeline with explicit field projection at every transform step. Field preservation is enforced by convention: every Code node hardcodes the field list it emits, every Sheets node uses an explicit column schema rather than dynamic mapping. Nothing drifts between transforms.

---

## **Operational Controls**

- **Credit-budget enforcement** — gap-aware lead-cap logic prevents the sourcing chain from exceeding its monthly discovery allowance; remaining budget is tracked alongside the pipeline data
- **Schema-locked column projection** — every Code node and every Sheets node hardcodes its output fields, addressing the n8n pattern where transforming nodes silently drop upstream fields
- **Audit logging at every stage** — discovery, enrichment, verification, and dedup all write to a centralized event log via EventLog Append v1, with workflow name, node, record id, step, result, and timestamp
- **Error-workflow routing** — every workflow in the family is wired to BREALLE Error Handler v1 (Tier 2 standard) so failures land in a structured error log rather than dying silently
- **Per-vertical ICP configuration** — verticals are configured externally, so onboarding a new vertical is a configuration change, not a code edit

---

## **Human-in-the-Loop Gate**

Sourcing is automated. **Outreach is not.**

The pipeline feeds verified leads to the BREALLE outreach engine, where every outbound draft is reviewed and approved by the founder before send. No outreach message goes out without explicit founder ratification. This is a deliberate Tier-3-grade control on the engine side: the sourcing pipeline can move fast because the gate at outreach is deliberately slow.

---

## **Governance**

The pipeline operates under BREALLE's Workflow Governance Standard (WGS) v1 at **Tier 2** — operational/revenue-support with internal pipeline effects.

Tier 2 controls applied:
- Workflow Record filed in the BREALLE Workflow Catalog before build
- Build Brief documenting node-level implementation
- Audit logging at every external touch
- Error-workflow routing to a shared Error Handler
- Post-deployment monitoring via daily log review

---

## **Production Footprint**

| Layer | Implementation | Nodes |
|---|---|---|
| Discovery | Apollo Discovery v3 | 20 |
| Enrichment | Apollo Enrichment v2 | 18 |
| Email verification | NeverBounce Verification Gate v1 | 25 |
| Event logging | EventLog Append v1 (shared) | 16 |
| Error routing | BREALLE Error Handler v1 (shared) | 8 |
| Orchestration | n8n on hardened production Linux server | — |
| Data layer | Schema-locked Google Sheets pipeline | — |
| Reverse proxy + TLS | Caddy with managed Let's Encrypt TLS | — |
| State | Postgres-backed n8n instance | — |
| Hardening | Key-based SSH, ufw firewall, fail2ban, unattended-upgrades | — |

---

## **What This Replaces**

- ✗ Manual prospect research and copy-paste workflow
- ✗ Unverified email lists with high bounce risk
- ✗ Credit-budget drift mid-month with no visibility
- ✗ Untracked dedup with double-touch risk
- ✗ No structured handoff to the outbound stage

## **What's Now Possible**

- ✓ Continuous, cost-aware sourcing across multiple verticals
- ✓ Pre-outreach deliverability verification — sender reputation protected
- ✓ Schema-locked handoff to the outreach engine with no field drift
- ✓ Full audit trail from discovery through verification
- ✓ Founder-gated outreach with sourcing throughput decoupled from approval pace

---

## **Key Insight**

> Outbound automation isn't a sourcing-volume problem.
>
> It's a credit-economics, deliverability, and audit-trail problem.
>
> Solve those three and the sourcing rate stops mattering.

---

## **Positioning Statement**

> Most small operators trying to run cold outbound burn their sourcing budget in two weeks, their domain reputation in three, and their attention span by the time the first reply arrives.
>
> BREALLE Lead Generator is the layer that prevents all three — cost-aware sourcing, pre-send deliverability verification, and a schema-locked handoff to the outreach engine where the founder still approves every send.

---

## **Stack**

n8n · Apify · Apollo · NeverBounce · Google Sheets · Postgres · Caddy · Hetzner-class hardened VPS · Tier 2 governance

---

## **About BREALLE**

BREALLE builds reliable support systems for trades and home-service owners — plumbers, HVAC, electricians, restoration — taking the repetitive, time-draining work off the owner's plate so the business stops depending on them being available.

Start with **The Time Audit** — a free 20-minute call to find where the week actually goes. No pitch.

[brealle.com](https://brealle.com) · [brandon@brealle.com](mailto:brandon@brealle.com)

---

**Brandon Robinson**
Founder, BREALLE
