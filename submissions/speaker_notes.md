Slide 1:

Welcome leadership to the Smart Recovery Phase 1 proposal review.
The objective today is to outline a targeted self-service portal designed to automate routine collections, protect vulnerable accounts, and deliver rapid operational returns.
At a high level, Phase 1 targets a net value of £2.40M with an 823% ROI, achieving capital payback in just 1.3 months while saving over 2,400 frontline staff hours.
Emphasize that execution carries low risk because it focuses strictly on a targeted customer segment without core platform disruption.

Slide 2:

Core Recommendation: Implement a lightweight self-service portal for straightforward cases (38% target) to clear balances, set 1–30 day payment promises, or structure £50–£5,000 installment plans.
Built-In Safeguards: Automatically pause collections for vulnerable customers and open disputes, ensuring seamless context transfer to representatives.
Financial & Regulatory Return: Deliver £2.40M in annual net value (£2.37M net revenue uplift, £30.8k cost savings) against a £260k build cost, yielding an 823% ROI, 1.3-month payback, and immediate FCA Consumer Duty alignment.
Execution Credibility: Low risk and high focus, connecting to existing systems without costly core banking overhauls while automating routine tasks so senior staff can focus on complex hardship decisions.

Slide 3:

Customer Journeys (Retention & Trust): Focuses on the 38% straightforward cases needing self-service. Eliminates access barriers via secure OTP login (KAN-4), provides transparent balances and flexible plans (KAN-5, KAN-6) to prevent drop-off, and secures cash flow through digital promise-to-pay with 48h reminders (KAN-20).
Triage & Safeguards (Risk & Capacity): Reclaims 2,400+ annual frontline hours by automating case routing (KAN-7), protects vulnerable customers with an automated 30-day "Breathing Space" hardship freeze (KAN-11), and prevents customer repetition using specialist handoff summaries (KAN-15).
Integration & Governance (Regulatory & Data Integrity): Fulfills mandatory 6-year statutory audit requirements through dual-store tamper-evident logging (KAN-8), halts uncoordinated outreach via 24h sync pipelines (KAN-12) and daily batch reconciliations (KAN-10), and enables active tracking with volumetric management reporting (KAN-13).

Slide 4:

Customer Friction ("Slow, Repetitive, Confusing"):
50.37% of accounts endure uncoordinated outreach (up to 7 separate attempts).
Duplicate status checks account for 28.9% of activities spread across 4 separate silos.
Handover friction persists across 58 representatives working in 4 distinct platforms without synced history.
Collections Reps ("Fragmented & Exhausting"):
43.37% of agent effort is consumed by manual administrative logging.
58 representatives rely on concurrent offline spreadsheets, creating severe version conflicts.
1,423 escalations create bottlenecks that drain over 200 senior staff hours.
Team Leaders ("Unclear and Unreliable"):
£3.05M sits in overdue balances without live management visibility.
1,458 manual reconciliation tasks consume over 218 staff hours.
Regulatory exposure includes 519 vulnerable accounts lacking tailored handling, alongside 1,007 promise accounts split across conflicting status codes.

Slide 5:

Break down the financial return and operational savings by initiative.
Priority 1 is the Eligible Payment Plan selection feature, delivering £1.46M in revenue uplift (£1.39M net benefit) and saving 8 minutes per case.
Priority 2 is the Digital Promise to Pay capture, yielding £874,920 in net benefit and saving 11 minutes per case.
Highlight foundational enablers, Self-Serve Balance View (404 hrs saved) and Rules-Based Routing (650 hrs saved), which combined deliver £2.37M in annual revenue uplift and full capital payback in under 2 months.

Slide 6:

Eligibility Rule: Emphasize that strict eligibility rules apply: only straightforward cases (the target 38%) are allowed to use the self-service portal.
Core Journeys (In Scope): Covers secure OTP verification (KAN-4), balance dashboards (KAN-5), promise-to-pay calendars (KAN-20), 3–12 month installment plans (KAN-6), automated contact triage (KAN-7), and 30-day hardship intake freezes (KAN-11).
Technical Enablers (In Scope): Includes 13-minute session timeouts (KAN-14), 6-year tamper-evident audit logging (KAN-8), context-aware handoff summary screens (KAN-15), daily ledger reconciliations (KAN-10), 24-hour legacy sync pipelines (KAN-12), and daily ROI performance reporting (KAN-13).
Boundaries & Out of Scope: Explicitly excludes detailed clickstream history sync (OP-06), automated hardship/vulnerability negotiations, legal escalations and dispute uploads, full legacy core-platform replacements, and online dispute document uploads.
Key Assumptions & Credibility: Relies on 24-hour API responsiveness, approved Risk/Compliance policies, and the 38% straightforward case ratio to deliver £2.40M annual value (£2.37M net revenue, £30.8k savings) against a £260k build cost with an 823% ROI and 1.3-month payback.

Slide 7:

Customer Journeys (Retention & Trust): Targets the 38% straightforward cases for self-service by eliminating access barriers via secure OTP login (KAN-4), providing transparent balances and flexible plans (KAN-5, KAN-6), and securing cash flow through digital promise-to-pay with 48h reminders (KAN-20).
Triage & Safeguards (Risk & Capacity): Reclaims 2,400+ annual frontline hours via automated case routing (KAN-7), protects vulnerable customers with a 30-day "Breathing Space" hardship freeze (KAN-11), and prevents customer repetition using specialist handoff summaries (KAN-15).
Integration & Governance (Regulatory & Data Integrity): Fulfills mandatory 6-year statutory audits via dual-store tamper-evident logging (KAN-8), halts uncoordinated outreach using 24h sync pipelines (KAN-12) and daily batch reconciliations (KAN-10), and enables active tracking with volumetric management reporting (KAN-13).

Slide 8:

Overview: Walk through the 9-screen interactive prototype, showing the flow from authentication and triage to self-service resolution or specialist exception routing.
Entry & Triage (SCR-01 to SCR-04): Enforces secure pre-authentication (KAN-4, KAN-9) with 3-attempt OTP lockout (SCR-02), routing straightforward cases (38% target) to self-service while deflecting complex queries.
Self-Service & Ineligibility Rules (SCR-03 to SCR-07): Supports balance summaries, 30-day payment promises (KAN-20), and 3–12 month payment plans (KAN-6). Strict ineligibility criteria—such as balances outside £50–£5,000, sub-£15 monthly floors, active disputes, or write-off requests—automatically pause self-service and trigger exception routing.
Exception Handoff & Support (SCR-09): Ineligible or distressed cases instantly route to Screen 7 (bespoke-plan) with a unique case reference, queueing them for manual affordability review, priority telephony (0800 458 9120), debt advice directories, and Staff View context transfer (KAN-15) to prevent customer repetition.
Governance & Security (SCR-08 & KAN-14): Confirms agreement registration with immutable 6-year FCA dual-store audit logging (KAN-8), 24-hour legacy database synchronization (KAN-12), and 13-minute session timeout protections with 48-hour contact suppression.

Slide 9:

Address potential implementation risks and their corresponding safeguards.
For legacy sync delays or downtime, automated staging queues and immediate collection pause triggers prevent duplicate outreach.
For regulatory and data privacy risks, immutable dual-store logging ensures 6-year FCA compliance while pre-auth shields and 13-minute timeouts protect customer data.
For adoption risks, context-aware specialist handoff drawers ensure reps see full history without forcing customers to repeat details.

Slide 10:

Summarize the core message: a 9-screen interactive prototype is fully specified and mapped to the Jira backlog.
Reiterate the single recommendation: approve Phase 1 to move forward with converting the existing prototype into a fully usable live solution.
Remind stakeholders of the financial and operational return: £2.40M annual value, 823% projected ROI, under 2-month payback, and full regulatory compliance.

