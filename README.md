# Lab 1 - Requirements Engineering & UML Use-Case Modelling

**Problem Statement #32: Personal Subscription & Recurring Expense Auditor**
Role: Requirements Engineer

## Contents

- `Lab1_Subscription_Auditor_Requirements.docx` - the full submission, containing:
  1. Requirements Table (5 FRs, 2 NFRs)
  2. UML Use-Case Diagram (rendered image)
  3. Use-Case Flow Specification (UC3 - Analyze Transactions for Recurring Billing Patterns)
  4. Appendix A - PlantUML source for the diagram

## App Summary

A micro-app that aggregates recurring bank charges, alerts users ahead of subscription renewal dates, calculates monthly and annualized burn rates, and provides one-click cancellation guides.

**Actors:** Individual User, Finance Auditor

## Use-Case Model at a Glance

| Use Case | Triggered by | Relationship |
|---|---|---|
| UC1 — Import Transaction Log (CSV/OFX) | Individual User | includes UC2 |
| UC2 — Securely Parse & Encrypt Imported Data | (via UC1) | included by UC1 |
| UC3 — Analyze Transactions for Recurring Billing Patterns | Individual User | includes UC4, UC5 |
| UC4 — Calculate Monthly Burn Rate | Individual User / (via UC3) | included by UC3 |
| UC5 — Send Renewal Alert | (via UC3) | included by UC3; extended by UC6 |
| UC6 — View Cancellation Guide | Individual User | extends UC5 |
| UC7 — Export Recurring Expense Report | Finance Auditor | — |
| UC8 — Configure Alert Preferences | Individual User | — |

`<<include>>` is used only for mandatory sub-behavior (always executed as part of the base use case). `<<extend>>` is used only for optional, condition-triggered behavior. UC1 is a precondition of UC3, not an include, since UC3 assumes the import already happened rather than invoking it.

## Requirements Traceability

| Req ID | Covered by |
|---|---|
| FR-001 (pattern detection) | UC3 |
| FR-002 (renewal alerts) | UC5, UC8 |
| FR-003 (burn rate) | UC4 |
| FR-004 (cancellation guide) | UC6 |
| FR-005 (auditor export) | UC7 |
| NFR-001 (secure parsing) | UC2 |
| NFR-002 (performance & uptime) | applies system-wide, not tied to one use case |

## Regenerating the Diagram

The PlantUML source in Appendix A can be pasted into any PlantUML renderer (e.g., plantuml.com/plantuml, a local PlantUML jar, or a VS Code extension) to reproduce or edit the diagram independently of the Word document.

## Key Thresholds Used Throughout

- Recurrence detection: ≥3 same-merchant charges, interval consistency ±3 days, amount consistency ±5%
- Minimum transaction history required for analysis: 60 days
- Default renewal alert lead time: 3 days (user-configurable)
- Performance target: ≤5 seconds to analyze a 12-month / 5,000-transaction history
- Uptime target: ≥99.5% monthly availability
