# Phase 1 Scope

## In scope

### Core Customer Journeys
- **Identity and account verification (OP-01 - KAN-4):** Lightweight, secure OTP authentication (SMS/email) confirming customer identity with a 3-attempt lockout threshold before displaying sensitive financial account details.
- **Account summary and eligible actions (OP-01 - KAN-5):** Dashboard displaying transparent, cleared overdue balance figures, an itemized breakdown of charges, and distinct self-service action pathways.
- **Digital promise-to-pay capture (OP-03 - KAN-20):** Interactive calendar selector allowing customers to commit to a single future payment date (e.g. next payday, capped at 30 days) with an instant timestamped digital receipt and automated confirmation.
- **Eligible payment-plan selection (OP-04 - KAN-6):** Pre-calculated installment schedules (3 to 12 months) with integrated tokenized Direct Debit or card mandate setup.
- **Rules-based contact triage (OP-05 - KAN-7):** Upfront evaluation separating straightforward accounts from complex or vulnerable cases, guiding the former into self-service while routing complex/vulnerable accounts to specialists.
- **Customer hardship & vulnerability intake (KAN-11):** Self-service disclosure screen that immediately freezes automated collections and outreach for 30 days and routes to Gareth's vulnerable customer queue.

### Technical, Governance & Regulatory Enablers
- **Session safeguarding & inactivity timeout (KAN-14):** 13-minute inactivity warning modal with 2-minute countdown under UK GDPR principles, invalidating idle sessions and conditionally routing abandoned mid-transaction journeys.
- **Dual-store audit trail logging (KAN-8):** Tamper-evident, synchronous event logging to `Portal Metadata` and `Portal interaction history` with a 6-year retention schedule to satisfy statutory and FCA Consumer Duty requirements.
- **Specialist handoff summary screen (KAN-15):** Context screen for referred, disputed, or timed-out accounts displaying referral reasons and prior portal steps so customers never have to repeat sensitive circumstances.
- **Daily ledger reconciliation (KAN-10):** Automated daily batch reconciliation comparing portal transaction records against legacy collections ledgers to guarantee ledger integrity.
- **24-hour core database synchronization (KAN-12):** Automated sync pipeline committing confirmed online promises and payment schedules to legacy collections databases within 24 hours to suppress conflicting collections contact.
- **Management portal performance reporting (KAN-13):** Daily reporting on sessions, verifications, plan conversions, drop-offs, and referral reasons to validate the £2.40M ROI business case.

## Out of scope

- **Detailed clickstream history sync (OP-06):** Granular, click-by-click customer navigation tracking on staff screens is deferred to Phase 2. Phase 1 provides the handoff summary only.
- **Automated hardship and vulnerability assessment:** Decisions regarding financial distress, health issues, or bereavement remain strictly human-led. The system identifies self-declared distress and halts automation, but does not attempt algorithmic hardship resolution.
- **Bespoke repayment negotiations & balance write-offs:** Terms outside the standard 3–12 month schedules or debt forgiveness route directly to senior specialists.
- **Legal escalation and litigation workflows:** Accounts subject to active litigation or formal recovery remain with the legal recovery team.
- **Full legacy core-platform replacement:** Phase 1 integrates via APIs and scheduled batch feeds rather than replacing core databases.
- **Online dispute document uploads:** Customers raising balance disputes speak directly with specialist staff; document upload portals remain out of scope for Phase 1.

## Assumptions

### Data & Technical Feasibility
1. **Legacy data accessibility:** Customer balances, contact details, and payment histories can be queried and updated via existing APIs or batch pipelines within 24 hours.
2. **`vulnerability_category` attribute availability:** Assumes core/CRM databases support or can be mapped to structured vulnerability tags (`HEALTH`, `BEREAVEMENT`, `HARDSHIP`, `BREATHING_SPACE`). If unpopulated, the triage engine falls back to `risk_flag = 'Y'`.
3. **`dispute_status` attribute availability:** Assumes backend databases identify active formal disputes via `dispute_status = 'OPEN_FORMAL'` (or an equivalent status flag).
4. **Standardized eligibility policies:** Minimum payment thresholds and a 12-month maximum plan duration are approved by Risk and Compliance without bespoke policy variations.

### Policy & Operational Rules (To Validate with Daniel & Gareth)
5. **14-day dispute collection pause:** Assumes automated collections are paused for 14 calendar days upon customer balance dispute notification, pending investigation. *(Policy validation required with Daniel).*
6. **30-day Breathing Space:** Assumes self-reported financial vulnerability triggers a 30-day statutory collection freeze in line with debt respite regulations. *(Policy validation required with Daniel).*
7. **6-year audit trail retention:** Assumes audit logs in `Portal interaction history` must be retained for 6 years in compliance with standard financial limitation periods. *(Policy validation required with Daniel).*
8. **Defensible portfolio parameters:** The 38% straightforward case ratio holds, supporting projected recovery uplifts (2.5% promise, 4% plan) and the £2.40M annual benefit.
9. **Staff availability & queue capacity:** Gareth's team has sufficient specialist capacity to receive referred and vulnerable cases without SLA degradation.

## Dependencies and constraints

- **System updates:** Confirmed online commitments must sync to legacy databases within 24 hours (KAN-12) to prevent conflicting collections outreach.
- **Compliance sign-offs:** Daniel (Compliance) must approve customer-facing disclaimers, CCA terms, verification wording, and hardship pause rules.
- **Specialist queue routing:** Gareth (Operations) must confirm routing thresholds and intake capacity for specialist queues.
- **Unconfirmed stakeholder sign-offs (owner TBC):** Technical and financial integrations require sign-off from the Finance Operations Lead (owner TBC) and Core Banking / IT Ops Lead (owner TBC).

## Why this scope is credible

This scope is credible because it focuses on the top four priorities identified in Week 1: OP-04 (Payment Plans), OP-03 (Promise to Pay), OP-01 (Balance View), and OP-05 (Smart Case Sorting), treating them as an interconnected operating system rather than disconnected features. Together, they create a seamless journey: the system automatically filters incoming cases (OP-05), gives customers clear visibility of what they owe (OP-01), and provides two straightforward digital settlement options (OP-03 and OP-04). By targeting the 38% of accounts that are straightforward, Phase 1 delivers £2.40M in annual total value (£2.37M in net revenue uplift and £30.8k in operational cost savings) against an upfront build cost of £260,000. This yields an 823% 12-month ROI, unlocks over 2,400 staff hours per year, and achieves full capital payback in just 1.3 months. Even under conservative stress testing (30% lower recovery uplift and 20% lower time savings), the plan remains resilient, generating £1.33M in net benefit with payback inside 2.7 months.

From a delivery and change perspective, the plan minimises execution risk by cleanly separating routine automation from specialist human discretion. By relying on pre-agreed business rules and proven self-service workflows, rather than attempting a complex, high-risk overhaul of legacy core systems, Phase 1 should be achievable on a reasonable time scale. Crucially, it directly resolves the core concerns identified in our ADKAR change assessment: frontline teams get immediate proof of workload relief by removing over 1,000 hours of manual status checks and queue confusion from Day 1, while Compliance and Legal gain an airtight, non-negotiable safety off-ramp ensuring vulnerable customers are always protected and routed to trained specialists.


| Deliverable            | Target Milestone   | Hard Deadline      | Estimated Effort | Risks & Considerations                                                       |
|------------------------|--------------------|--------------------|------------------|------------------------------------------------------------------------------|
| To-Be Process          | Tuesday, 1:45 PM   | Tuesday, 4:00 PM   | 2–3 hours        | Maintain strict scope boundaries; prevent unnecessary process complexity.    |
| Jira Backlog           | Wednesday, 1:45 PM | Wednesday, 5:00 PM | 3–4 hours        | Unfamiliar with Jira; factor in learning time for the new tool.              |
| Rapid Portal Prototype | Thursday, 1:45 PM  | Thursday, 5:00 PM  | 3–4 hours        | Broad task scope and unfamiliar tooling; AI outputs require manual review.   |
| Executive Briefing     | Friday, 11:30 AM   | Friday, 12:30 PM   | 2 hours          | Strict delivery cutoff; requires synthesis of all prior sprint deliverables. |
