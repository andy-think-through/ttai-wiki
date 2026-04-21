# Classify Before Acting

> Classify every inbound message before acting on it. Prevents over-action on ambiguous input. Discovered during Mark-Lite v2 safety review.
> Last updated: 2026-04-21

## The Principle

When an employee receives a Slack message (or any inbound communication), classify it before acting:

| Classification | Action |
|---------------|--------|
| Acknowledgement ("Nice work", "Thanks") | "Noted." and stop |
| Command (explicit instruction) | Execute |
| Question | Research and answer |
| Instruction (implicit task) | Execute with confirmation |
| Draft feedback (approve/edit/reject) | Process feedback |
| Ambiguous | Ask a clarifying question, don't guess |

The critical distinction: **acknowledgements get "Noted." and stop.** Without this classification, "Nice work" would trigger the employee to try to DO something.

## Origin

Mark-Lite v2 safety review (2026-04-21). The original v1 prompt treated every Slack message as an instruction. An acknowledgement like "Nice work" could have triggered Mark-Lite to attempt an action, potentially sending an email or modifying a tracker.

## Where Else It Applies

- **All employees with Slack interaction:** Universal pattern for the dual-mode prompt (Mode 2 classification)
- **Wiki:** Already uses a simplified version (question vs new info vs correction vs instruction)
- **Future employees (Karen, Cord):** Same classification layer needed

## Relationship to Other Principles

- Operationalises [[scheduled-tasks-need-zero-intervention]] -- prevents false triggers from Slack noise
- Related to [[trust-ladder-over-binary-trust]] -- classification is one of the safety controls

## Links
- [[employee-framework]] -- Framework where this is defined
- [[wiki-agent-SKILL]] -- Existing simplified implementation

## Sources
- Mark-Lite v2 prompt development (2026-04-21), inbox ingest file
