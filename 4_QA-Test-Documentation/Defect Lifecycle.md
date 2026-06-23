Defect Lifecycle

When to use: Reference document for all team members during QA, development, and defect triage.


1. Defect Workflow States

A defect moves through the following lifecycle:


It can also exit the workflow via:
- Deferred
- Rejected

State Definitions

- New: Logged by QA, not yet reviewed.
- Open: Verified and accepted for investigation.
- In Progress: Assigned to developer and actively being worked on.
- Fixed: Developer claims issue is resolved.
- Retest: QA is validating the fix.
- Closed: QA confirms defect is resolved.
- Reopened: Defect persists after retesting.
- Deferred: Fix postponed to a future release.
- Rejected: Invalid, duplicate, or not reproducible.


2. State Transition Rules

- New → Open: QA logs defect, triage approves
- Open → In Progress: Assigned to developer
- In Progress → Fixed: Developer completes fix
- Fixed → Retest: Build deployed for QA validation
- Retest → Closed: QA confirms resolution
- Retest → Reopened: Issue still exists
- Open → Deferred: Business decides to postpone
- Open → Rejected: Invalid/duplicate/non-reproducible
- Reopened → In Progress: Developer re-assigned



3. Severity Definitions (S1–S4)

S1 – Critical
- System crash, data loss, security breach
- Blocks core functionality
- SLA: Immediate response (0–4 hours), fix within same day where possible
- Example: Payment gateway failure during checkout

S2 – High
- Major feature broken but workaround exists
- Significant business impact
- SLA: Response within 24 hours, fix within 1–3 days
- Example: User cannot reset password

3 – Medium
- Non-critical functionality issue
- UI/logic issues with workaround
- SLA: Fix within current or next sprint
- Example: Incorrect validation message text

S4 – Low
- Cosmetic issues, minor UI alignment problems
- No functional impact
- SLA: Backlog or future release
- Example: Misaligned button spacing



4. Priority Classification (P1–P4)

Priority defines urgency of fixing:

- P1: Must fix immediately (production blockers)
- P2: High priority, fix soon in current cycle
- P3:Medium priority, planned fix
- P4: Low priority, optional or cosmetic

Note: Severity ≠ Priority. Severity is impact; Priority is urgency.



5. Required Defect Report Fields

Every defect must include:

- Defect ID
- Title / Summary
- Description
- Steps to Reproduce
- Expected Result
- Actual Result
- Severity (S1–S4)
- Priority (P1–P4)
- Environment (QA/Staging/Prod)
- Module/Feature
- Reporter
- Assignee
- Attachments (screenshots/logs/videos)
- Date Reported
- Status


6. Escalation Path for S1 Defects

For Critical (S1) defects:

1. QA logs defect immediately
2. Notify QA Lead + Dev Lead via urgent channel
3. Escalate to Product Owner if blocking production
4. If unresolved within SLA:
   - Escalate to Engineering Manager
   - Inform Project Manager / Stakeholders
5. Continuous updates every 1–2 hours until resolution



7. Defect Quality Metrics & Targets

Team QA health is measured using:

- Defect Leakage Rate: < 5%
- Reopen Rate: < 10%
- Average Defect Resolution Time: Based on severity SLA
- Test Escape Rate: Minimal production defects
- Defect Aging: No S1 defects older than 24 hours



8. Best Practices

- Write clear, concise defect titles
- Always include reproducible steps
- Attach evidence (screenshots/logs/videos)
- Avoid duplicate defects—search before logging
- Keep severity consistent with business impact
- Update defect status promptly
- Do not mix multiple issues in one defect
- Validate fixes thoroughly before closing
- Use standardized environment details


9. Usage Notes

- Use this document during "defect triage meetings"
- Refer to it before assigning severity or priority
- Keep it pinned in Confluence / QA wiki for consistency across teams