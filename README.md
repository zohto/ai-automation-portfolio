# Brandon Robinson — AI Systems & Automation

**Founder, [BREALLE](https://brealle.com) · Reliable Support Systems for Trades & Home Services**

I have 17 years of operations experience and build automation systems for the places where time quietly disappears: chasing late payments, following up on quotes, and the weekly admin that turns into a weeknight problem.

BREALLE builds reliable support systems for trades and home-service owners — plumbers, HVAC, electricians, restoration — so the repetitive work runs on schedule instead of depending on the owner being available.

→ **[brealle.com](https://brealle.com)**  
The Time Audit — a free 20-minute call to find where the week actually goes. No pitch.

---

## Production Systems

### Applicant Pipeline — Applicant Intake & Tracking System
*Status: Delivered to a client and run in production. Engagement no longer active.*

End-to-end applicant intake automation built for a client engagement. Handles inbound applicant data, deduplication and normalization, deterministic keyword-based reply classification, structured pipeline tracking, reply routing, and failure alerting. Built and operated under a formal Tier 3 workflow standard (external communications, low reversibility, WGS governance applied).

**Stack:** n8n · Google Sheets · Gmail · Webhook triggers · Postgres · Caddy · Hetzner VPS

[→ Read case study](case-studies/applicant-intake-automation-case-study.md)

---

### BREALLE Lead Generator — Outbound Lead Sourcing & Enrichment Pipeline
*Status: Built and run in production under Tier 2 governance; the outbound programme it fed was concluded in August 2026.*

Outbound sourcing pipeline targeting email-native trades and home-service businesses across a New England primary geography. Mixed discovery and enrichment layer chosen on measured yield rather than vendor preference; NeverBounce verification before any lead reached the outreach pool. Schema-locked Google Sheets handoff with credit-budget management against a metered monthly discovery allowance. Fed the BREALLE outreach engine.

**Stack:** n8n · Apify · Apollo · NeverBounce · Google Sheets · Postgres · Caddy · Tier 2 governance

[→ Read case study](case-studies/brealle-lead-generator.md)

---

## Project Work

### AI Request Routing Automation
An AI-powered workflow that classifies and routes internal business requests automatically — replacing manual triage with structured, auditable routing logic.

- LLM classification with confidence validation
- Priority and department extraction
- Human review fallback for low-confidence cases
- Decision logging for operational visibility

**Stack:** n8n · OpenAI · Google Sheets
[→ View files](request-routing-automation/)

---

### AI-Powered Customer Support Workflow
Analyzes incoming support requests and routes them intelligently using AI classification.

- Automated triage and routing
- Reduced manual handling
- Faster response times

[→ View files](ai-customer-support-workflow/)

---

### Automated Feedback Analysis
Processes customer feedback and extracts structured operational insights automatically.

- Sentiment analysis
- Topic extraction and categorization
- Structured insight output for operations teams

[→ View files](automated-feedback-analysis/)

---

### Weather-Based Operational Automation
Uses weather conditions to trigger operational responses — staffing adjustments, scheduling, demand forecasting.

- Condition-based trigger logic using live weather API data
- Outputs structured operational recommendations for scheduling and staffing

[→ View files](weather-automation/)

---

## Case Study

### Applicant Intake & Re-Engagement at Production Scale — Regional Home-Appliance Distributor
End-to-end automation system delivered for a regional home-appliance distributor managing high-volume applicant flow for field sales and technician roles. Three-chain n8n pipeline (intake/qualification, outreach, reply handling) with daily-cap enforcement, halt-on-error circuit breakers, dedup audit logging, and Tier 3 governance — running on a hardened production VPS.

[→ Read case study](case-studies/applicant-intake-automation-case-study.md)

---

### Outbound Lead Sourcing & Enrichment at Production Scale — BREALLE Lead Generator
Five-workflow n8n sourcing pipeline (discovery + enrichment + NeverBounce verification + shared event/error logging) totaling 87 nodes, verified against the running instance 2026-08-04. Cost-aware design managed against a metered monthly discovery allowance, with pre-outreach deliverability verification and a schema-locked Google Sheets handoff to the outreach engine. Tier 2 governance; the outbound programme it fed was concluded in August 2026.

[→ Read case study](case-studies/brealle-lead-generator.md)

---

### Sales Workflow Automation — Regional Distributor
Diagnostic analysis and automation architecture for a small regional distributor operating with manual lead intake and phone-based scheduling. Documents the gap analysis, system design, and automation architecture for structured lead capture, AI-assisted classification, CRM integration, and follow-up automation.

[→ Read case study](case-studies/sales-workflow-automation.md)

---

### Revenue Recovery from Untapped Applicants — Regional Home Services Company
One-page diagnostic of a home services company sitting on roughly 20,000 unprocessed Indeed applicants. Documents the conversion failure between applicant volume and recruiter throughput, and outlines the structured intake, qualification, and routing system that closes the gap — turning a hiring backlog into recoverable revenue capacity.

[→ Read case study](case-studies/home_service_business_case_study_1_page.md)

---

## Resume

[→ Download Resume](resume/brandon-robinson-ai-automation-engineer.pdf)

---

*Certified: AI & ML — TripleTen*
*Available in English and Spanish*
*Contact: brandon@brealle.com*
