# Lab 1: Academic Elective Bidding & Allocation System

  
**Problem Statement #05 | Campus & Academic Operations**

## Actors

- **Student**
- **Academic Registrar**

---

## Functional Requirements


| ID     | Description                                                                                                                                                                                     | Priority | Acceptance Criteria                                                                                                                                                                                                                                                                                | Rationale                                                                                                                                    |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| FR-001 | The system shall allow a student to distribute exactly 100 bidding credits across up to 10 ranked elective course preferences during an open bidding window.                                    | High     | **Pass:** Student can assign credits to each preference; total equals 100; submission is saved with timestamp. **Fail:** Submission accepted when total ≠ 100, negative credits entered, or bidding window is closed.                                                                              | Credit-based bidding is the core selection mechanism; capping at 100 ensures fair competition and predictable solver input.                  |
| FR-002 | The system shall validate that a student has completed all prerequisite courses for each elective in their preference list before accepting a bid submission.                                   | High     | **Pass:** Bid rejected with a clear error listing unmet prerequisites; bid accepted only when all prerequisites are satisfied. **Fail:** Bid accepted despite missing prerequisites or validation skipped for any course.                                                                          | Prevents ineligible enrollments and reduces manual correction work for the registrar after allocation.                                       |
| FR-003 | The system shall detect timetable collisions among a student's selected electives and warn the student before bid submission.                                                                   | Medium   | **Pass:** Overlapping electives are flagged with conflicting course names and time slots; student must acknowledge the warning or remove a conflicting preference to proceed. **Fail:** Bid submitted with undetected schedule overlap or no warning shown.                                        | Students need visibility into scheduling conflicts early; the registrar should not allocate seats that force impossible timetables.          |
| FR-004 | The system shall allow the Academic Registrar to configure and execute the elective allocation solver, which assigns seats based on bid credits, course capacity, and prerequisite eligibility. | High     | **Pass:** Registrar sets bidding window end time and course capacities, triggers allocation, and receives a completion report with seat assignments per student. **Fail:** Allocation runs without capacity constraints, ignores bid credits, or assigns seats to ineligible students.             | Centralizes the seat-allocation process so the registrar can run a fair, constraint-aware batch assignment at the end of the bidding period. |
| FR-005 | The system shall allow students to view their final elective allocation results, including assigned courses, unallocated preferences, and remaining bid credits after the allocation run.       | Medium   | **Pass:** After allocation, each student sees assigned courses with seat confirmation, courses not allocated (with reason: capacity/prerequisite/conflict), and credits refunded for unallocated preferences. **Fail:** Results unavailable, incomplete, or displayed before allocation completes. | Students need transparent outcomes to plan their semester; showing refund logic builds trust in the bidding process.                         |


---



## Non-Functional Requirements


| ID      | Type                    | Description                                                                                                                                                                   | Priority | Acceptance Criteria                                                                                                                                                                                                                                      | Rationale                                                                                                                                       |
| ------- | ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| NFR-001 | Performance             | The elective allocation solver shall process 5,000 student bids across all courses and resolve schedule conflicts in under 30 seconds on standard university server hardware. | High     | **Pass:** Benchmark test with 5,000 simulated bids completes allocation and conflict resolution in ≤ 30 s at p95 latency. **Fail:** p95 latency exceeds 30 s or solver times out under peak load.                                                        | Large departments run simultaneous bidding; slow allocation delays result publication and blocks the next academic workflow step.               |
| NFR-002 | Security & Availability | The system shall authenticate all users via university SSO, enforce role-based access (Student vs. Academic Registrar), and maintain 99.5% uptime during the bidding window.  | High     | **Pass:** Unauthenticated requests are rejected; students cannot access registrar functions; system uptime ≥ 99.5% measured over the bidding period. **Fail:** Unauthorized bid modification, role bypass, or downtime exceeding 0.5% during the window. | Bidding involves sensitive academic data and time-bound actions; security prevents fraud and availability ensures all students can participate. |


