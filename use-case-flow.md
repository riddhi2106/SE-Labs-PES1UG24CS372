# Use-Case Flow Specification
## Submit Bidding Preferences

**System:** Academic Elective Bidding & Allocation System  
**Problem Statement #05 | Campus & Academic Operations**

| Field | Value |
|-------|-------|
| **Use Case ID** | UC-002 |
| **Use Case Name** | Submit Bidding Preferences |
| **Primary Actor** | Student |
| **Related Requirements** | FR-001, FR-002 |
| **Included Use Cases** | Validate Prerequisites |
| **Extending Use Case** | Modify Submitted Bid |

---

## Brief Description

The student ranks elective course preferences, distributes 100 bidding credits across them, and submits the bid during an open bidding window. The system validates prerequisites before saving the submission.

---

## Preconditions

1. The student is registered for the current academic semester.
2. The elective bidding window is open (configured by the Academic Registrar).
3. The elective catalog for the semester is published in the system.
4. The student has browsed or is aware of available electives *(optional — via Browse Elective Catalog)*.

---

## Postconditions

**Success**

- The student's ranked preferences and credit allocations are persisted with a submission timestamp.
- Total allocated credits equal exactly 100.
- All selected electives have satisfied prerequisites on record.

**Failure**

- No bid data is saved; the student remains on the bidding form with error messages displayed.

---

## Main Success Scenario

| Step | Actor | Action |
|------|-------|--------|
| 1 | Student | Opens the bidding preferences page for the current semester. |
| 2 | System | Displays the preference list (up to 10 slots) and available electives. |
| 3 | Student | Selects electives and ranks them in order of preference (1 = highest). |
| 4 | Student | Assigns bidding credits to each ranked elective such that the total equals 100. |
| 5 | System | Validates prerequisite completion for every selected elective *(«include» Validate Prerequisites)*. |
| 6 | Student | Reviews the bid summary and clicks **Submit**. |
| 7 | System | Saves the bid, records the submission timestamp, and displays a confirmation message. |

---

## Alternate Flow

### A1 — Modify Submitted Bid (extends Step 6)

| Step | Actor | Action |
|------|-------|--------|
| A1.1 | Student | After an earlier submission, opens the submitted bid while the bidding window is still open and chooses **Modify**. |
| A1.2 | System | Displays the current ranked preferences and credit allocations for editing. |
| A1.3 | Student | Re-ranks electives, changes credit allocations, or adds/removes preferences (total must remain 100). |
| A1.4 | System | Re-validates prerequisites for the updated preference list *(«include» Validate Prerequisites)*. |
| A1.5 | Student | Confirms the revised bid and clicks **Submit**. |
| A1.6 | System | Updates the stored bid with a new timestamp and displays a confirmation message. |

**Rejoins:** Postconditions (Success) on completion.

---

## Business Rules

- A student may allocate a maximum of 100 bidding credits per bidding period (FR-001).
- Negative credit values are not permitted.
- Bids cannot be submitted or modified when the bidding window is closed.
- Electives with unmet prerequisites must be rejected before submission (FR-002).

---

## Special Requirements

- Prerequisite validation must complete within 2 seconds of each submission attempt.
- Modified bids must replace the prior submission atomically — no duplicate active bids per student per period.
