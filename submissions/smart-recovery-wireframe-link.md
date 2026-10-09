# Smart-Recovery Portal — Prototype & Wireframe Traceability

**Deliverable:** Clickable HTML/CSS Interactive Prototype  
**Local File Link:** [smart-recovery-prototype.html](./smart-recovery-prototype.html) (`/Users/heathershepherd/Coursework-Technical-Business-Analyst-Week-2/submissions/smart-recovery-prototype.html`)  
**Scope Alignment:** [Phase 1 Scope Statement](./phase-1-scope-statement.md)  
**Backlog Mapping:** [Jira Backlog](./Jira-backlog.csv)  
**Process Alignment:** [To-Be Process Map](./to-be-process-map.bpmn) & [Process Diagram](./to-be-process-map.png)  
**Requirements Source:** [Prototype Notes](./prototype_notes.md)  

---

## 1. Prototype Overview

The **Smart-Recovery Customer Portal** prototype is a zero-dependency, fully interactive, responsive HTML5/CSS3/JavaScript web application simulating the customer self-service journey. It embodies the Phase 1 target: capturing the **38% straightforward delinquent accounts** to generate **£2.40M in annual total value** (£2.37M net revenue uplift and £30.8k operational savings) with an 823% 12-month ROI.

### Key Interactive Features
- **Working Authentication & Lockout Safeguard (KAN-4):** Simulates 6-digit OTP verification with a live 3-attempt decrement counter. Exceeding 3 attempts triggers `AUTH_LOCKOUT` and routes to the collections team for credential reset.
- **Dynamic Balance & Charge Breakdown (KAN-5):** Transparent presentation of £485.50 cleared overdue balance with itemized principal, late fee, and interest breakdown.
- **Rules-Based Intent Routing (KAN-7):** 5 distinct pathways cleanly distinguishing routine self-service from specialist cases.
- **Digital Promise-to-Pay Calendar (KAN-20):** Interactive settlement date selector enforcing the strict 1–30 calendar day policy cap, automated 48-hour reminder calculation, and collection pause.
- **Installment Plan Affordability Calculator (KAN-6):** Structured 3, 6, 9, and 12-month repayment schedules validating the £15.00/month policy minimum floor with tokenized Direct Debit mandate capture.
- **Multi-State Routed-to-Representative Handoff (KAN-7, KAN-11, KAN-14):** Empathetic exception screen dynamically adapting to Vulnerability (30-day statutory Breathing Space + StepChange/National Debtline/Citizens Advice links), Balance Disputes (14-day hold), Auth Lockouts, and Mid-Journey Timeouts, with interactive Day & Time Window specialist callback scheduling.
- **Internal Specialist Case Review Drawer (KAN-15):** Toggleable internal staff view showing journey audit trails and case context, guaranteeing that customers never have to repeat sensitive circumstances.
- **Global Inactivity Timeout Overlay (KAN-14):** Accessible modal with 2-minute countdown timer testing UK GDPR session termination and `ABANDONED_IN_FLIGHT` 48-hour contact suppression.
- **Integrated BA Traceability Header:** Real-time top banner on each screen detailing the Screen ID, Jira Story ID, BPMN process step, acceptance criteria, and active business rules.

---

## 2. Screen Inventory & Traceability Matrix

| Screen ID | Screen Name | Journey Step | Jira Story / Task | BPMN Process Activity | Key Business Rules & Scope Boundaries |
|:---|:---|:---|:---|:---|:---|
| **SCR-01** | Landing / Entry Page | Entry | **KAN-4, KAN-9** | *Access Portal* (Customer Lane) | Brand trust, FCA credentials, zero financial data displayed prior to authentication. |
| **SCR-02** | Identity Verification | Access | **KAN-4** (Highest) | *Request account verification* → *Provide details* → *Are details valid?* | 6-digit cryptographic OTP; 3-attempt lockout threshold; `AUTH_LOCKOUT` flag routes to representative. |
| **SCR-03** | Account Summary Dashboard | Review | **KAN-5** (High), **KAN-16** | *Display Account Summary & Eligible Actions* | Overdue balance (£485.50), itemized breakdown; prominent vulnerability escape banner. |
| **SCR-04** | Choose Next Action | Decision | **KAN-5, KAN-7** (Highest) | *What does the customer want to do?* (Gateway) | Triage engine: Straightforward (38%) self-service vs. specialist routing for disputes/hardship. |
| **SCR-05** | Promise-to-Pay Setup | Commitment | **KAN-20** (High), **KAN-17** | *Collect digital promise to pay* → *Add payment schedule* | Interactive date selector strictly capped at 1–30 days; 48-hour prior reminder; 24h batch sync (**KAN-12**). |
| **SCR-06/07**| Eligible Payment Plan | Selection | **KAN-6** (High), **KAN-17** | *Display eligible payment plans* → *Select Payment Plan* | Standardized 3, 6, 9, 12-month tiers; £15/mo minimum payment floor; Direct Debit tokenization. |
| **SCR-08** | Confirmation & Next Steps | Complete | **KAN-8, KAN-12, KAN-20, KAN-6** | *End initial interaction* → *Reconciliation & Sync* | Instant timestamped digital receipt; automated SMS/Email dispatch; 24h core sync stops outreach. |
| **SCR-09** | Routed to Representative | Exception | **KAN-7, KAN-11, KAN-14, KAN-15** | *Refer to Representative* → *Queue Safeguarding* | 30-day Breathing Space pause (**KAN-11**); 14-day dispute pause; debt charities; Specialist Screen (**KAN-15**). |
| **Overlay**| Inactivity Timeout Modal | Security | **KAN-14** (High), **KAN-18** | *Session Timeout Check* (Sub-process) | 13-min idle trigger; 2-min countdown; `ABANDONED_IN_FLIGHT` flag with 48h contact suppression. |

---

## 3. Exception Paths Demonstrated in the Prototype

1. **Authentication Lockout (`AUTH_LOCKOUT`):**
   - *Trigger:* 3 consecutive incorrect OTP entries on Screen 2.
   - *Outcome:* Session locked, `AUTH_LOCKOUT` logged to Portal Metadata, customer routed to Screen 7 with priority phone number `0800 458 9120` and SOP credential reset instructions from the collections team.
2. **Customer Hardship & Statutory Breathing Space (KAN-11):**
   - *Trigger:* Customer clicks "Experiencing Financial Difficulty" on Screen 3 or "Cannot Afford Options" on Screen 4.
   - *Outcome:* Instant 30-day statutory collection pause, case routed to the collections team's vulnerable customer queue, referral links to StepChange, National Debtline, and Citizens Advice.
3. **Formal Balance Dispute (KAN-7):**
   - *Trigger:* Customer clicks "I Disagree with this Balance" on Screen 3 or 4.
   - *Outcome:* Dispute reference issued (`DISP-38104`), 14-day collection pause applied, case assigned to the collections team's dispute investigation specialists.
4. **Bespoke Terms / Below £15 Floor (KAN-6):**
   - *Trigger:* Customer clicks "Request Custom Terms / Specialist Review" on Screen 5B.
   - *Outcome:* Prevents unviable online plan creation; routes to senior collections specialist for manual affordability assessment.
5. **In-Flight Inactivity Timeout (KAN-14):**
   - *Trigger:* 2-minute countdown expires mid-transaction.
   - *Outcome:* Safely closes session, tags account with `ABANDONED_IN_FLIGHT`, applies 48-hour contact suppression, and routes follow-up task to frontline triage.

---

## 4. How to Launch and Review the Prototype

1. Open `/Users/heathershepherd/Coursework-Technical-Business-Analyst-Week-2/submissions/smart-recovery-prototype.html` directly in any web browser (Chrome, Safari, Edge, Firefox).
2. Alternatively, use the top toolbar navigation pills to jump between screens or click through the natural customer journey.
3. Use the **"⏱️ Trigger Timeout (KAN-14)"** button in the top bar to inspect the session timeout safeguard at any stage.
4. Use the **"📋 Toggle BA Spec"** button to show/hide the technical business analysis annotations.
5. On Screen 7, click **"🔍 Staff View (KAN-15)"** to inspect the customer journey context available to collections specialists.
