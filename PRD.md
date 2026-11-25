# Product Requirements Document (PRD)

**Project Title:** Netpulse  
**Course:** BU-COS 209  
**Document status:** Draft — updated using the BU-209 Week 4 stakeholder-meeting and PRD guidance. Confirmed findings and unanswered questions are kept separate below.

---

## 1. Product Overview

Netpulse is a simple backend hub that collects time-stamped connectivity reports for campus locations, aggregates recent signals into a clear current status, and lets authorised support staff post official updates.

- **What the product is:** a reporting and status-visibility system for campus network conditions, not a network repair tool.
- **Who it serves:** students who need to know whether a location is usable before they start time-sensitive work, and ICT staff who need structured issue awareness.
- **Scope boundary:** software cannot repair physical network hardware or increase upstream bandwidth. Netpulse focuses on visibility, getting problems across to the right people, and accountability.

**Proposed solution:** authenticated users submit short reports for a campus location; the system aggregates recent reports into a current status; authorised ICT staff post official notices and move issues through a three-state lifecycle (Reported → Investigating → Resolved).

---

## 2. Problem Statement

### 2.1 The problem

Students across the university normally deal with slow connections and dead zones when trying to access the portal, submit assignments, or join online classes.

- **Wasted time and movement:** when the network is slow, students lose time and start moving around the vicinity looking for a usable spot.
- **Waste of money:** when students keep buying data but the connection is slow or absent, the data is never used to its fullest, putting students at a loss.

### 2.2 Who has this problem

- **Students:** need a reliable connection for classes, the portal, assignments, and sometimes games.
- **Staff:** need structured and reliable connectivity to send messages, set assignments, and hold classes.

### 2.3 Evidence from surveys and interviews

- **Total people interviewed:** 23 students.
- **Most common failed network windows:** very hot afternoons around 3pm and hostels such as Samuel Akande.
- **Disrupted work shared by interviewees:** not able to join classes or submit assignments, and submissions failing.
- **Student 1:** “the connection speed is very frustrating at times and unbearable but we adapt.”
- **Student 2:** “it didn't allow me to submit assignments sometimes and do some transfers, which was very frustrating.”
- **Staff:** “we don't like it; even the Wi-Fi isn't that reliable, but we just have to go with it.”

### 2.4 Why current solutions fall short

- **WhatsApp & group chats:** questions get buried quickly, lack verified timestamps, and rarely confirm whether a fix has happened.
- **Walking around:** signal bars do not guarantee usable throughput or low latency.
- **Repeated retries & mobile-data fallbacks:** retrying on flaky connections wastes time and can cause duplicate actions, while mobile data is costly and still struggles in dead zones.

---

## 3. Business Objectives

What the organisation/product team wants to achieve:

- Improve visibility of campus network health for students and ICT staff.
- Reduce time lost to repeated retries and unnecessary movement between locations.
- Replace scattered chat complaints with structured, time-stamped issue awareness.
- Increase confidence in portal access, assignment submission, and online classes during peak periods.
- Provide an auditable record of official status changes for accountability.

---

## 4. Target Users

- **Students (primary):** view current connectivity status summaries for campus locations and submit connectivity reports.
- **ICT/support staff (primary):** view location summaries and clustered recent reports, post official status notices, and move issues through the issue lifecycle.
- **Administrators (secondary):** manage university locations, user roles, and moderation rules, and review audit logs of official status changes.
- **Academic staff (affected group):** need reliable connectivity for classes and assignments; whether they need a separate account role is an open question (see §11).

---

## 5. Stakeholders

A stakeholder is any person or group with an interest in the product, its development, operation, or success. Different stakeholders have different expectations, so the PRD records their interests explicitly.

| Stakeholder | Interest in Netpulse | Involvement |
| --- | --- | --- |
| Students | Reliable connection for classes, portal, assignments and reporting problems | Report conditions and view status summaries |
| Academic staff | Reliable connectivity to send messages, set assignments and hold classes | Affected group; interviewed in discovery |
| ICT support staff | Structured issue awareness and ability to publish authoritative updates | Primary operational users |
| Administrators | Location/role governance, moderation rules and auditability | Manage configuration and review logs |
| Course/product owner (BU-COS 209) | Product scope, requirements and deliverables | Approves the PRD and MVP scope |

**Important (Week 4 lesson):** distinguish confirmed decisions from unanswered questions. Never document an assumption as an approved business requirement.

---

## 6. User Stories

Format: *As a [type of user], I want [an action or feature], so that [the benefit I receive].*

| ID | User story |
| --- | --- |
| US-01 | As a student, I want to submit a time-stamped connectivity report for a campus location so that ICT can see current conditions. |
| US-02 | As a student, I want to check a location's status summary so that I can decide whether to start a class/assignment or move elsewhere. |
| US-03 | As an ICT staff member, I want to see clustered recent reports for a location so that I can understand the problem before responding. |
| US-04 | As an ICT staff member, I want to move a location issue from Reported to Investigating to Resolved so that students see an accurate lifecycle. |
| US-05 | As an ICT staff member, I want to post an official status notice so that students receive an authoritative update. |
| US-06 | As an ICT staff member, I want to remove invalid or test reports so that status summaries remain trustworthy. |
| US-07 | As an administrator, I want to manage locations and roles so that reporting stays organised and access is controlled. |
| US-08 | As an administrator, I want to review audit logs of official status changes so that accountability is maintained. |
| US-09 | As a student on a flaky connection, I want a retried submission to be recognised as a duplicate so that no duplicate reports are created. |

---

## 7. Functional Requirements

Functional requirements describe **what the system must do**.

| ID | Requirement | Priority |
| --- | --- | --- |
| FR-01 | Authenticated users can register/log in and are assigned a role: Student, ICT_Staff or Admin. | Must |
| FR-02 | Students can submit a connectivity report for a campus location by selecting **Location**, **Connection Type** (Campus Wi-Fi, Mobile Data, Other) and **Status** (Good, Slow/Lagging, Outage/No connection — label to confirm). | Must |
| FR-03 | A report may include an optional short note. | Must |
| FR-04 | Users can view a location status summary: aggregated status, number of recent reports, latest update time, and whether data is fresh or stale. | Must |
| FR-05 | Reports outside the agreed freshness window are excluded from live status and marked stale rather than treated as current conditions. | Must |
| FR-06 | Duplicate submissions carrying the same **Client Request ID** are ignored instead of creating multiple identical reports. | Must |
| FR-07 | ICT staff can view clustered recent reports for a location. | Must |
| FR-08 | ICT staff can move a location issue through **Reported → Investigating → Resolved** and attach an official note. | Must |
| FR-09 | Only authorised ICT/admin users can publish official updates or change issue state; each change records who made it and when. | Must |
| FR-10 | ICT/admin users can remove invalid or test reports. | Should |
| FR-11 | Administrators can manage university locations, user roles and moderation rules. | Should |
| FR-12 | Administrators can review audit logs of official status changes. | Should |
| FR-13 | The system stores status logs with Location ID, actor, previous state, new state, official note and timestamp. | Must |

---

## 8. Non-Functional Requirements

Non-functional requirements describe **how well the system operates** and the constraints it must satisfy. Targets should be measurable wherever possible.

| Category | Requirement / target |
| --- | --- |
| Performance | 95% of location status lookups return within 2 seconds under the agreed normal load. |
| Security | Passwords must never be stored in plain text; role-based access must be enforced on every protected action. |
| Availability | The platform must meet an agreed uptime target (target to confirm with stakeholders). |
| Scalability | The system must accommodate growth in students, locations and report volume (targets to confirm). |
| Reliability | Failed or retried submissions must not create duplicate reports; idempotency is enforced via Client Request ID. |
| Privacy | Student personal information must follow agreed access permissions; public status summaries should avoid exposing personal data. |
| Auditability | Every official status change is logged with actor, timestamp, previous state and new state. |
| Usability | Status summaries must be readable on common phones and low-bandwidth connections. |

**Remember:** functional = what the system does; non-functional = how well it does it. A feature can work functionally but still fail a performance or reliability requirement.

---

## 9. Scope and Priorities

### 9.1 Minimum Viable Product (first release)

The MVP is the smallest version that delivers enough value to validate the approach — not an unfinished product.

- Student registration and authentication with roles.
- Quick connectivity reporting with time-stamped location, connection type, status and optional note.
- Location status lookup with recent-report count, latest update and fresh/stale indication.
- Clear three-state issue lifecycle: Reported → Investigating → Resolved.
- Authorised official status notices.
- Basic enforcement of role, state, staleness and duplicate-submission rules.

### 9.2 MoSCoW prioritisation

The objective is to build the right product first, not the biggest product first.

| Priority | Items | Reason |
| --- | --- | --- |
| **Must Have** | Registration/login and roles; connectivity reporting; location status lookup; three-state issue lifecycle; freshness/staleness rule; idempotent duplicate handling; role/state enforcement with status logs | Essential for the first release to be trustworthy and usable |
| **Should Have** | Clustered recent-report view for ICT; removal of invalid/test reports; admin management of locations, roles and moderation rules; audit-log review screen | Important for operations and governance but not blocking launch |
| **Could Have** | Historical trend charts per location; notifications when an issue is resolved; bulk import of campus locations; export of reports for analysis | Additional value if time and resources permit |
| **Won't Have (this release)** | Repairing physical network hardware or increasing upstream bandwidth; AI-based predictive outage detection; in-app payments, delivery or marketplace features | Explicitly out of scope for this release |

---

## 10. Acceptance Criteria

Acceptance criteria define the conditions that must be satisfied before a feature is considered complete.

### AC-01 — Submit a connectivity report (US-01, FR-02, FR-03, FR-06)

- The user must be authenticated.
- A location must be selected from the managed location list.
- Connection Type must be one of the allowed values.
- Status must be provided and valid; the optional note must respect the agreed length limit.
- Invalid submissions are rejected with a clear error message.
- A valid report is stored with a timestamp and its Client Request ID.
- A repeated submission with the same Client Request ID succeeds without creating a second report.

### AC-02 — View location status (US-02, FR-04, FR-05)

- The response includes aggregated status, recent report count, latest update time and a fresh/stale flag.
- Reports older than the freshness window are excluded from live status.
- A location with no recent reports shows “No recent data” rather than an outdated “Good” status.

### AC-03 — Move issue state (US-04, FR-08, FR-09, FR-13)

- Only ICT_Staff or Admin users can change issue state.
- Only the transitions Reported → Investigating → Resolved are available in the first release.
- Each transition records actor, timestamp, previous state, new state and optional official note.
- Students viewing the location see the updated state.

### AC-04 — Post official status notice (US-05, FR-09)

- Only authorised ICT/admin users can post a notice.
- The notice includes text and a timestamp and appears on the location status view.

### AC-05 — Remove invalid report (US-06, FR-10)

- Only ICT/admin users can remove a report.
- The removal is recorded so status summaries and audit history remain explainable.

---

## 11. Assumptions and Open Questions

### Assumptions (not yet approved requirements)

- Reports are submitted by authenticated users; anonymous reporting is not planned for the first release.
- Existing university accounts can be reused for authentication (to confirm).
- Status values are Good, Slow/Lagging and Outage/No connection (final labels to confirm).
- Web-based access is sufficient for the first release (to confirm).
- The freshness window and uptime target will be agreed with stakeholders before implementation.

### Open questions (require stakeholder confirmation)

- How will student and staff identity be verified?
- What exactly counts as a “recent” report — what is the freshness window?
- What uptime and concurrency targets are agreed?
- Should academic staff have a separate account role, or use the same access as students?
- Who owns escalation after an issue is marked Investigating?
- Are official notices only shown on lookup, or also pushed to users?
- Can an issue be reopened after it is marked Resolved?
- How are invalid or test reports identified, and who approves their removal?

---

## 12. Backend Logic & Data Design (Language-Agnostic)

### 12.1 Data we store

- **Users:** User ID, Account Identifier, Full Name, Role (Student, ICT_Staff, Admin), Account Status.
- **Locations:** Location ID, Name, Zone/Building Type, Current Aggregated Status, Issue State (Reported, Investigating, Resolved), Last Updated Timestamp.
- **Connectivity Reports:** Report ID, User ID, Location ID, Connection Type, Usability, Optional Note, Client Request ID, Timestamp.
- **Status Logs:** Log ID, Location ID, Updated By, Previous State, New State, Official Note, Timestamp.

### 12.2 Key rules the backend enforces

- **Freshness / staleness rule:** only reports within the agreed freshness window count toward live status; older reports are marked stale rather than treated as active conditions.
- **Idempotent submissions:** if a user's connection drops and the same report is retried with the same Client Request ID, the duplicate is ignored instead of creating multiple identical entries.
- **Role and state enforcement:** only authorised ICT/support or admin users can publish official status updates or move an issue to Investigating or Resolved, recording who made the change and when.

---

## 13. Benefits and Success Metrics

### Benefits

- Clearer, time-stamped visibility into which campus spots are working before students move or start time-sensitive tasks.
- Faster, more structured issue awareness for ICT staff instead of scattered chat complaints.
- Lightweight, reliable status checks and safe retries suited to unstable campus connections.

### Success metrics (targets to be confirmed)

- Number of registered students and active locations covered.
- Number of active reports and active reporters per week.
- Percentage of issues moved to Resolved within the agreed response time.
- Reduction in duplicate or abandoned submissions.
- Number of invalid/test reports removed and audit logs reviewed.
- Student feedback on whether status summaries match their lived experience.

---

