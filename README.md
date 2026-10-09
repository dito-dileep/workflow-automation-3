# BPMN Process Models

<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=26&duration=3200&pause=900&color=0F766E&center=true&vCenter=true&repeat=true&width=760&height=75&lines=Two+BPMN+2.0+Process+Models;Happy+Paths+%2B+Exception+Handling" alt="BPMN process models" />

![BPMN 2.0](https://img.shields.io/badge/BPMN-2.0-0F766E?style=for-the-badge)
![Models](https://img.shields.io/badge/Models-2-0E7490?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Process+Exceptions-7C3AED?style=for-the-badge)

</div>

This repository contains two BPMN 2.0 models. Each model includes the normal process route and the main operational exceptions around it.

## Included models

| Assignment | Scenario | BPMN file | Failure register |
|:--:|:--|:--|:--|
| 1 | Student Project Approval and Allocation | [Open BPMN](assignment-1-student-project-approval.bpmn) | [Open register](ASSIGNMENT_1_FAILURE_PATH_REGISTER.md) |
| 3 | Loan Origination and Approval | [Open BPMN](loan-origination-approval.bpmn) | [Open register](FAILURE_PATH_REGISTER.md) |

---

## Assignment 1 - Student Project Approval and Allocation

<p align="center">
  <img src="images/student-project-approval-overview.svg" alt="Student project approval and allocation overview" width="100%" />
</p>

### Process scope

The process starts when a student team submits a proposal and ends when an allocated guide accepts the team, or when the proposal is closed because it is invalid, rejected, duplicated, or late.

### Happy path

```text
Submit proposal -> validate form and team -> screen proposal -> duplicate check
-> committee review -> match available guide -> guide accepts -> record and notify
```

### Participants

| Participant | Role |
|:--|:--|
| Student / Team | Submits and revises the proposal |
| Project Coordinator | Screens proposals and resolves allocation exceptions |
| Review Committee / HoD | Evaluates proposal quality and feasibility |
| Faculty Guide | Accepts or declines the allocation request |
| Project Management System | Validates data, checks similarity, allocates, and notifies |

### Exception handling

The model covers incomplete proposals, invalid team rules, duplicate topics, late-submission review, committee revision or rejection, review-SLA escalation, guide unavailability, no guide response, and notification failure. Details are in the [Assignment 1 Failure Path Register](ASSIGNMENT_1_FAILURE_PATH_REGISTER.md).

### BPMN techniques

- User tasks for student, coordinator, committee, and guide actions
- Business-rule tasks for validation and guide-workload matching
- Exclusive gateways for validation, committee, and allocation decisions
- Boundary timers for submission, review, and guide-response deadlines
- Error boundary event and manual fallback for notification recovery

---

## Assignment 3 - Loan Origination and Approval

<p align="center">
  <img src="images/loan-origination-overview.svg" alt="Loan origination and approval overview" width="100%" />
</p>

### Process scope

The process starts when an applicant submits a loan application with supporting documents. It ends with disbursement, rejection, withdrawal, lapse, offer expiry, or a held-funds exception.

### Happy path

```text
Submit application -> check documents -> KYC, credit, and income checks in parallel
-> risk scoring -> underwriter review -> offer -> acceptance -> e-sign
-> disbursement -> account creation and notification
```

### Participants

| Participant | Role |
|:--|:--|
| Applicant | Submits documents, accepts the offer, and signs the agreement |
| Loan Officer | Handles manual checks and document/KYC exceptions |
| Underwriter / Credit Committee | Reviews manual, high-value, and borderline cases |
| Fraud and Compliance | Handles escalated fraud or AML concerns |
| Operations / Disbursement | Releases funds and resolves payment exceptions |
| Credit Bureau | Provides external credit-score information |
| Core Banking System | Validates, scores, generates offers, and creates accounts |

### Exception handling

The model covers document correction, KYC mismatch, bureau-service failure, low score, affordability revision, authority escalation, collateral concerns, offer expiry, withdrawal, signature retry, and disbursement recovery. See the full [Loan Failure Path Register](FAILURE_PATH_REGISTER.md).

### BPMN techniques

- Parallel gateway for independent KYC, bureau, and income checks
- Business-rule tasks for document completeness and risk eligibility
- Exclusive gateways for approval, counter-offer, and rejection routes
- Timer boundary events for document and offer deadlines
- Error boundary events for bureau and payment failures
- Compensation-oriented withdrawal and recovery controls

---

## Repository structure

```text
BPMN_Exercise_3/
|- assignment-1-student-project-approval.bpmn
|- ASSIGNMENT_1_FAILURE_PATH_REGISTER.md
|- loan-origination-approval.bpmn
|- FAILURE_PATH_REGISTER.md
|- images/
|  |- student-project-approval-overview.svg
|  `- loan-origination-overview.svg
`- README.md
```

## Viewing the models

Open either `.bpmn` file with Camunda Modeler or another BPMN 2.0-compatible editor. The source files include diagram-layout information as well as the BPMN process definitions.
