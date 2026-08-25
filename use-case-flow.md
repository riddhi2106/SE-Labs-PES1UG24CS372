# Use-Case Flow Specification
## Submit Elective Bids

**System:** Academic Elective Bidding & Allocation System  
**Problem Statement #05 | Campus & Academic Operations**

| Field | Value |
|-------|-------|
| **Use Case ID** | UC-001 |
| **Use Case Name** | Submit Elective Bids |
| **Primary Actor** | Student |
| **Related Requirements** | FR-001, FR-002, FR-003 |
| **Included Use Cases** | Authenticate User, Validate Prerequisites |
| **Extending Use Case** | Acknowledge Timetable Conflict Warning |

---

## Brief Description

The student ranks elective course preferences, distributes 100 bidding credits across them, and submits the bid during an open bidding window. The system validates prerequisites and checks for timetable collisions before saving the submission.

---

## Preconditions

1. The student is registered for the current academic semester.
2. The elective bidding window is open (configured by the Academic Registrar).
3. The student has not already submitted a final bid for this bidding period *(or is editing a draft before final submission)*.
4. The elective catalog for the semester is published in the system.

---

## Postconditions

**Success**

- The student's ranked preferences and credit allocations are persisted with a submission timestamp.
- Total allocated credits equal exactly 100.
- All selected electives have satisfied prerequisites on record.

**Failure**

- No bid data is saved; the student remains on the bidding form with error or warning messages displayed.

---

## Main Success Scenario

| Step | Actor | Action |
|------|-------|--------|
| 1 | Student | Opens the elective bidding page for the current semester. |
| 2 | System | Authenticates the student via university SSO *(«include» Authenticate User)*. |
| 3 | System | Displays the available elective catalog and an empty preference list (up to 10 slots). |
| 4 | Student | Selects electives and ranks them in order of preference (1 = highest). |
| 5 | Student | Assigns bidding credits to each ranked elective such that the total equals 100. |
| 6 | System | Validates prerequisite completion for every selected elective *(«include» Validate Prerequisites)*. |
| 7 | System | Checks selected electives for timetable collisions; none are found. |
| 8 | Student | Reviews the bid summary and clicks **Submit**. |
| 9 | System | Saves the bid, records the submission timestamp, and displays a confirmation message. |

---

## Alternate Flow

### A1 — Timetable Conflict Detected (extends Step 7)

| Step | Actor | Action |
|------|-------|--------|
| A1.1 | System | Detects overlapping time slots between two or more selected electives and displays a conflict warning with course names and clashing slots. |
| A1.2 | Student | Either (a) removes or re-ranks the conflicting elective to eliminate the overlap, or (b) acknowledges the warning and chooses to proceed despite the conflict. |
| A1.3 | System | If the student revised preferences, re-validates prerequisites (Step 6) and re-checks timetable collisions (Step 7). If the student acknowledged the warning, continues to Step 8. |

**Rejoins:** Main Success Scenario at Step 8 (if student proceeds) or Step 4/5 (if student revises preferences).

---

## Business Rules

- A student may allocate a maximum of 100 bidding credits per bidding period (FR-001).
- Negative credit values are not permitted.
- Bids cannot be submitted when the bidding window is closed.
- Electives with unmet prerequisites must be rejected before submission (FR-002).

---

## Special Requirements

- Prerequisite validation must complete within 2 seconds of submission attempt.
- Timetable conflict warnings must identify all conflicting course pairs, not just the first detected pair (FR-003).
