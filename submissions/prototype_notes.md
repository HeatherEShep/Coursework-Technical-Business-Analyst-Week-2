# Smart-Recovery Prototype Specification & Screen Traceability Notes

This companion documentation details the architecture, screen-by-screen specification, business logic, and Jira user story traceability for the **Smart-Recovery Self-Service Portal** prototype (`smart-recovery-prototype.html`).

---

## 1. Screen 1: Landing / Entry Page (SCR-01)
* **Related User Story IDs:** `KAN-4`, `KAN-9`
* **Key Data Shown:**
  * Service branding & trust credentials.
  * FCA Consumer Duty regulation badges, Consumer Credit Act (CCA) 1974, and UK GDPR compliance assurances.
  * 3-step value overview (Quick Identity Check, Transparent Overview, Flexible Resolution).
  * *Zero customer financial or delinquency data is displayed.*
* **Validation / Business Rule:**
  * Pre-authentication barrier (UK GDPR Article 32 & CONC guidelines): strictly zero personal identifiable information (PII) or overdue balance data exposed before verified authentication.
* **Next Steps in Journey:**
  * Click *"Manage My Account"* -> Proceeds to **Screen 2 (Identity Verification - SCR-02)**.
  * Click *"Prefer to Speak to Someone?"* -> Routes to **Screen 7 (Specialist Support - SCR-09)**.

---

## 2. Screen 2: Identity Verification & Sign-In Assistance (SCR-02)
* **Related User Story IDs:** `KAN-4` (Highest / Must-Have), `KAN-9`
* **Key Data Shown:**
  * Pre-filled reference number (`SR-89421`) from inbound SMS/email magic link.
  * Date of Birth and Postal Code inputs.
  * Masked mobile phone delivery indicator (`07*** ***412`).
  * 6-digit OTP passcode input field and remaining attempts indicator (`3 Verification Attempts Remaining`).
* **Validation / Business Rule:**
  * Cryptographic OTP verification with a strict 3-attempt retry threshold.
  * 3 consecutive failed verification attempts automatically triggers an `AUTH_LOCKOUT` state and diverts the customer to telephony support to prevent brute-force exposure.
* **Next Steps in Journey:**
  * Valid OTP entered -> Unlocks authenticated session and advances to **Screen 3 (Account Summary - SCR-03)**.
  * 3 Verification failures -> Routes to **Screen 7 (Exception Screen - SCR-09)** under `AUTH_LOCKOUT`.

---

## 3. Screen 3: Account Summary Dashboard (SCR-03)
* **Related User Story IDs:** `KAN-5` (High), `KAN-11`, `KAN-16`
* **Key Data Shown:**
  * Customer personalized greeting (*Alex Taylor*).
  * Total cleared arrears balance (£485.50).
  * Delinquency stage (*Delinquent - 34 Days Past Due, Pre-Default Stage*).
  * Itemized transparent charge breakdown (Monthly Installment: £420.00, Late Admin Fee: £35.00, Accrued Interest: £30.50).
  * Recent communications timeline (Notice of Arrears, SMS reminder).
  * Prominent, empathetic vulnerability/hardship escape banner.
* **Validation / Business Rule:**
  * Only accessible after identity verification. Targets 12.49% balance enquiry deflection by providing transparent ledger items. Requires an immediate escape route for vulnerable circumstances.
* **Next Steps in Journey:**
  * Click *"Choose Resolution Options"* -> Advances to **Screen 4 (Choose Next Action - SCR-04)**.
  * Click *"Get Support & Pause"* -> Routes immediately to **Screen 7 (Specialist Handoff - SCR-09)** triggering a 30-day statutory breathing space hold (`KAN-11`).
  * Click *"I Disagree with this Balance"* -> Routes to **Screen 7 (Specialist Handoff - SCR-09)** lodging a formal 14-day dispute hold (`KAN-7`).

---

## 4. Screen 4: Choose Next Action / Triage & Intent Selector (SCR-04)
* **Related User Story IDs:** `KAN-5`, `KAN-7` (Rules-Based Triage), `KAN-18`
* **Key Data Shown:**
  * 5 clear, mutually exclusive resolution intent cards:
    1. *Pay Balance in Full Today (£485.50)*
    2. *Pay Later / Promise to Pay (1–30 Days)*
    3. *Spread Cost / Payment Plan (3–12 Months)*
    4. *Dispute this Balance (14-Day Hold)*
    5. *I Cannot Afford Any of These Options (Financial Hardship)*
* **Validation / Business Rule:**
  * Rules-based case sorting and triage. Automatically routes straightforward self-service accounts (38% target population) into automated digital resolution while cleanly deflecting complex, disputed, or distressed cases to human specialist queues.
* **Next Steps in Journey:**
  * Option 1 (*Pay in Full*) -> Advances to **Screen 5C (Immediate Card Settlement - SCR-04b)**.
  * Option 2 (*Promise to Pay*) -> Advances to **Screen 5A (Promise-to-Pay Setup - SCR-05)**.
  * Option 3 (*Payment Plan*) -> Advances to **Screen 5B (Installment Plan Selection - SCR-06/07)**.
  * Option 4 (*Dispute*) or Option 5 (*Hardship*) -> Routes to **Screen 7 (Specialist Exception Routing - SCR-09)**.

---

## 5. Screen 5A: Digital Promise-to-Pay Setup (SCR-05)
* **Related User Story IDs:** `KAN-20` (OP-03, High), `KAN-17`
* **Key Data Shown:**
  * Total settlement balance (£485.50).
  * Interactive settlement date picker with dynamic range boundaries.
  * Quick-select milestone pills (+7 days, +14 days, +21 days, +28 days).
  * Fulfillment reminder / payment method choices.
  * Notice of Terms (48-hour prior notification, conditions under which enforcement actions resume).
* **Validation / Business Rule:**
  * Strict policy cap: settlement promise date must be within **1 to 30 calendar days** from the current date. Rejects past dates and dates beyond 30 days.
* **Next Steps in Journey:**
  * Click *"Confirm Payment Promise"* -> Captures commitment and advances to **Screen 6 (Confirmation & Receipt - SCR-08)**.
  * Click *"View Monthly Installments"* -> Bridges to **Screen 5B (Payment Plan Selector - SCR-06/07)**.
  * Click *"Back to Options"* -> Returns to **Screen 4 (SCR-04)**.

---

## 6. Screen 5B: Eligible Payment Plan Flow (SCR-06/07)
* **Related User Story IDs:** `KAN-6` (OP-04, High), `KAN-17`
* **Key Data Shown:**
  * Total arrears (£485.50) and eligibility threshold banner (£50–£5,000 met).
  * Tiered duration cards: 3 months (£161.83/mo), 6 months (£80.92/mo), 9 months (£53.94/mo), and 12 months (£40.46/mo).
  * Repayment schedule summary, first payment collection date (1st of next month), and Direct Debit guarantee terms.
  * Custom terms escape callout (*"None of these amounts work?"*).
* **Validation / Business Rule:**
  * Arrears must fall between £50 and £5,000.
  * Monthly repayment amount must satisfy the **£15.00/month policy floor threshold**.
  * Durations longer than 12 months, balance write-offs, or sub-£15/mo arrangements are strictly ineligible for self-service and must route to human specialists.
* **Next Steps in Journey:**
  * Click *"Authorize Mandate & Finalize Plan"* -> Tokenizes mandate and advances to **Screen 6 (Confirmation & Receipt - SCR-08)**.
  * Click *"Request Custom Terms / Specialist Review"* -> Routes to **Screen 7 (Specialist Handoff - SCR-09)** under `bespoke-plan`.
  * Click *"Back to Options"* -> Returns to **Screen 4 (SCR-04)**.

---

## 7. Screen 5C: Immediate Settlement / Card Payment (SCR-04b)
* **Related User Story IDs:** `KAN-5`, `KAN-8` (Dual-Store Audit Logging)
* **Key Data Shown:**
  * Balance to clear (£485.50).
  * Debit card input form: Cardholder Name, Card Number (masked/formatted), Expiry (MM/YY), CVV.
  * Test mode indicator banner with *"Re-populate Test Data"* shortcut.
* **Validation / Business Rule:**
  * Payment details must be submitted and validated before generating a final confirmation and cleared-balance receipt. Requires valid card length (13–19 digits), valid expiry date format, and 3-4 digit CVV.
* **Next Steps in Journey:**
  * Click *"Pay £485.50 Now"* -> Authorizes payment transaction and advances to **Screen 6 (Confirmation & Receipt - SCR-08)**.
  * Click *"Back to Options"* -> Returns to **Screen 4 (SCR-04)**.

---

## 8. Screen 6: Confirmation & Next Steps (SCR-08)
* **Related User Story IDs:** `KAN-8` (Dual-Store Audit Logging), `KAN-12` (Automated 24h Nightly Sync), `KAN-20`, `KAN-6`
* **Key Data Shown:**
  * Unique Transaction Reference ID (e.g. `TX-20261008-8942`).
  * `PAUSE_COLLECTIONS_ACTIVE` status badge confirming suspension of debt recovery.
  * Itemized agreement summary (Plan/settlement type, committed amounts, due date, payment method).
  * Dispatch delivery targets (SMS & Email).
  * Core Database Sync indicator (KAN-12 staging).
  * Clear *"What happens next?"* guidance list.
* **Validation / Business Rule:**
  * Agreement registration creates an immutable dual-store audit record (`KAN-8`) and stages the schedule into the 24-hour nightly core database synchronization queue (`KAN-12`). All automated outbound debt collection calls/letters are immediately suppressed.
* **Next Steps in Journey:**
  * Click *"Download PDF Agreement Receipt"* -> Generates and downloads digital agreement receipt.
  * Click *"Return to Account Dashboard"* -> Returns to **Screen 3 (SCR-03)** in an updated state.
  * Click *"Secure Sign Out"* -> Safely terminates session and returns to **Screen 1 (SCR-01)**.

---

## 9. Screen 7: Routed to Representative / Specialist Handoff (SCR-09)
* **Related User Story IDs:** `KAN-7` (Triage & Case Routing), `KAN-11` (Vulnerability Intake & Breathing Space), `KAN-14` (Session Timeout), `KAN-15` (Specialist Review Context)
* **Key Data Shown:**
  * Unique Case Reference (e.g. `CASE: VUL-94812`, `CASE: DISP-38104`, `CASE: SEC-00129`, `CASE: TMO-55201`, `CASE: BES-77319`).
  * Dynamic status banner reflecting specific routing reason:
    * *Financial Hardship:* 30-Day Statutory Breathing Space hold activated.
    * *Balance Dispute:* 14-Day collections investigation hold.
    * *Auth Lockout:* Security lockout guidance after 3 OTP failures.
    * *Inactivity Timeout:* 48-Hour contact hold preserving in-flight intent (`ABANDONED_IN_FLIGHT`).
    * *Ineligible / Custom Plan:* Transferred to senior specialist affordability queue.
  * Direct contact options: Freephone Priority Specialist Line (`0800 458 9120`) and interactive Specialist Call-Back request form.
  * Free independent debt advice directory (StepChange, National Debtline, Citizens Advice).
  * Staff View drawer (`KAN-15`) displaying the internal triage context and session audit trail.
* **Validation / Business Rule:**
  * Non-repetition principle (FCA Consumer Duty Principle 12): captures full customer intent and journey history so the customer never has to repeat their circumstances when speaking with a specialist.
  * Applies automatic collections hold corresponding to the exception type.
* **Next Steps in Journey:**
  * Submit call-back request -> Displays confirmed scheduled call-back window and assigns priority ticket.
  * Dial phone line -> Agent retrieves pre-populated case file via reference number.
  * Click *"Return to Portal Home"* / *"Close Session"* -> Flushes credentials and returns to **Screen 1 (SCR-01)**.

---

## 10. Global Supporting Overlay: Inactivity Timeout Modal (KAN-14)
* **Related User Story IDs:** `KAN-14` (Session Timeout Detection, Summary Logging, and Queue Safeguarding)
* **Key Data Shown:**
  * Session inactivity security prompt.
  * 2-minute live countdown timer (`02:00` down to `00:00`).
  * Action choices: *"Stay Logged In"* vs. *"Save & Exit"*.
* **Validation / Business Rule:**
  * Triggers after 13 minutes of inactivity (15-minute total UK GDPR security threshold).
  * If the 2-minute countdown expires without customer input:
    * If on an active resolution screen (Screens 4, 5A, 5B, 5C), the session is flagged as `ABANDONED_IN_FLIGHT`, applies a 48-hour contact suppression hold, and routes cleanly to **Screen 7 (SCR-09)**.
    * If on unauthenticated/entry screens (Screens 1, 2), credentials are immediately purged and the browser resets to **Screen 1 (SCR-01)** to avoid queue clutter.
* **Next Steps in Journey:**
  * Click *"Stay Logged In"* -> Dismisses overlay and resets inactivity timer.
  * Click *"Save & Exit"* or Timer expires -> Invokes `executeSessionTimeout()`.
