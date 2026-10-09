# Failure Path Register

This register is the operational companion to `loan-origination-approval.bpmn`. It records the trigger, control, owner and exit for every identified failure path.

| ID | Stage | Trigger | Control / resolution | Owner | Exit |
|:--:|:--|:--|:--|:--|:--|
| L1 | Document check | Missing, unreadable or expired evidence | Return a targeted missing-items list; allow correction for 7 days | Applicant / Loan Officer | Continue or **Application lapsed** |
| L2 | KYC | Data mismatch with authoritative records | Manual verification; retain a reason code if unresolved | Loan Officer | Continue or **Rejected** |
| L3 | Fraud & AML | Forgery, sanctions or AML hit | Compliance investigation, internal report and termination when confirmed | Fraud & Compliance | **Rejected — compliance** |
| L4 | Bureau check | Timeout, outage or malformed response | Three timed retries; manual assessment or timed parking fallback | Loan Officer | Continue or parked case |
| L5 | Risk score | Score below the selected product policy | Reject with reasons, or issue counter-offer for lower amount / security | Underwriter | **Rejected** or revised scoring |
| L6 | Income / DTI | Income fails affordability policy | One revised amount / term cycle before final decision | Underwriter | Continue or **Rejected** |
| L7 | Authority | Amount exceeds authority or score is borderline | Senior committee review and SLA reminder | Credit Committee | Continue or **Rejected** |
| L8 | Collateral | Low valuation or title issue | Revalue, lower LTV, re-underwrite; reject unclear ownership | Underwriter | Continue or **Rejected** |
| L9 | Offer | No acceptance within 15 days | Expire offer; notify applicant and close outstanding offer record | Core Banking System | **Offer expired** |
| L10 | Withdrawal | Applicant cancellation at any active stage | Release holds and compensate completed charge / reservation work | Operations | **Withdrawn** |
| L11 | Signature | E-signature mismatch or no signature | Remind and resend; stop after two unsuccessful attempts | Applicant / Loan Officer | Continue or **Offer cancelled** |
| L12 | Disbursement | Invalid account or payment-gateway error | Verify account, retry, then hold funds and contact applicant; reverse account creation when needed | Operations | Continue or **Funds held** |

## Control principles

- **No silent failure:** every terminal branch has a labelled end state and notification action.
- **No infinite rework:** document, bureau, affordability and signature loops are time- or count-bounded.
- **No hidden side effects:** withdrawal and disbursement-repair paths explicitly compensate reservations, charges or account creation.
- **Auditability:** rejection paths retain a reason code rather than ending with an unexplained decline.
