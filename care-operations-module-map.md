# Care Operations Platform: Module Map

This page expands the [main case study](care-operations-platform.md). It explains module boundaries and examples visible in the private project documentation and implementation. It is a technical overview, not a product manual or a claim that every optional module is enabled at every installation.

## Workforce lifecycle

| Module | What the workflow does | Important boundary |
| --- | --- | --- |
| Recruitment | Short application, scoped full-application link, manager review, interview and offer responses, references, evidence checks and staff conversion | Applicant records remain the source until conversion; no general applicant account is required for a new application. |
| Staff and onboarding | Staff profile, contracts, eligibility, portal linkage, starter tasks, documents, change requests and leaver handling | A staff member's approved profile is separate from login and attendance-device records. |
| Staff self-service | Desktop and mobile views for rota, hours, leave, training, policies and profile requests | Staff-submitted changes go through review before changing the approved staff record. |
| Training | Role requirement matrix, assignments, sessions, bookings, completion review, evidence and expiry awareness | A booking or uploaded certificate is not automatically an approved completion. |

The recruitment implementation preserves submitted evidence and manager actions. Onboarding connects approved recruitment to contract and access setup. Training requirements can be checked against a person's role and completion history, while staff-facing interfaces show due or expired items.

## Scheduling, attendance and pay

| Module | What the workflow does | Important boundary |
| --- | --- | --- |
| Rota | Weekly assignments, templates, publication, open shifts and swap handling | The assignment's unit and worked role define operational context for that shift. |
| Kiosk | Device pairing, clock events, current-on-site/fire list, agency entry and event logs | Device identity and raw punches are evidence, not an approved HR profile or final payable time. |
| Attendance approval | Match planned shifts with clock evidence; auto-approve clear cases and present exceptions for manager decisions | Rota edits, ambiguous evidence and leave conflicts must not bypass review. |
| Leave | Day-level storage with grouped request review, approve/reject/cancel/send-back actions and overlap context | Approved leave affects payroll facts; pending leave is kept separate. |
| Annual leave | Employee-specific leave year, contract-hours history, taken/future/pending balances and forecast | Accrual begins at the appropriate employment or leave-year start and follows dated hours changes. |
| Payroll preparation | Refreshable daily facts, premium and break rules, weekly overtime allocation, reports and period finalisation | The daily fact is derived from approved source records; finalised periods need a controlled reopen. |

For a shift, the implementation considers the planned interval, linked or nearby clock evidence, manager outcome, approved absence and contract in force that day. It then derives paid, weekend and bank-holiday minutes, including work across local midnight. Weekly overtime is allocated to the month where the payroll week starts. These details matter because a simple clock-out minus clock-in calculation would give the wrong answer for several common cases.

## Quality, governance and evidence

| Module | What the workflow does | Current limit |
| --- | --- | --- |
| Supervisions | Templates or free-form discussion, scheduling, recorded answers, follow-up actions, acknowledgement and sign-off | Staff-app self-acknowledgement and generated PDF are not yet built. |
| Audits | Question bank, audit setup, draft and submitted runs, scoring, findings, action plans, evidence and report/print views | PDF output is browser print; a generated PDF/email service is pending. |
| Policies | Rich-text versions, audience assignment, staff release and version-specific acknowledgement | Automatic notifications and review-due alerts are pending. |
| Document Hub | Search/index documents from staff, recruitment, audits and service certificates; staff-document review and scoped manager access | A fully generic upload/review widget across all modules is pending. |
| Scanner intake | Private-folder PDF/image intake, type/owner suggestions, strong-match auto-filing and an unclear-file queue | This application-side foundation does not run OCR. |
| Service certificates | Supplier/provider register, certificate requirements by location, protected uploads and renewal history | Reminder email job and reminder log UI are pending. |

The audit workflow keeps question answers and evidence tied to a run, creates actions from findings, and records action updates. Supervision similarly preserves meeting answers and follow-up actions, then locks a signed-off record. Policies retain old versions so a staff acknowledgement refers to the exact content released.

## Additional operational modules

- **Agency staffing:** provider and worker setup, kiosk clocking, manager approval, planned cover and approved-hours CSV for invoice matching. Rate/cost calculations are not yet part of that export.
- **Resident and room records:** room allocation, moves, discharge and daily presence, with basic on-page counts. Richer occupancy reporting is pending.
- **Communication:** a feature-flagged central inbox and message/response model for staff and applicants, with audience selection, templates and email alerts. It is disabled by default and the automatic alert trigger still needs completion.
- **Background work:** registered jobs refresh payroll facts and staff compliance, handle scanner intake and support training-expiry notices. Jobs have their own enablement and operational controls.

## What this demonstrates

The project combines operational workflow design with source-of-truth discipline, permission and scope checks, protected evidence, audit trails, scheduled processing, derived reporting and staff-facing interfaces. The engineering challenge is keeping these modules connected without letting one stage make an unreviewed decision for another.

These notes are documentation only. Private source, data, configuration and deployment details are not included.

