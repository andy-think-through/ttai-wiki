# Wiki Agent -- Routines Job Spec

> Wiki's autonomous employee configuration for Claude Code Routines. Dual-mode: scheduled scan (every other day) + API follow-up (Slack replies).
> Last updated: 2026-04-16

## Platform

**Claude Code Routines** (migrated from Cowork scheduled tasks on 2026-04-15).

- **Schedule trigger:** Every other day
- **API trigger:** Slack replies via [[ttai-slack-bridge]]
- **Reporting:** Slack #ttai-employees
- **Memory:** GitHub repo (andy-think-through/ttai-wiki) -- all state persists in the repo, not in conversation memory
- **Connectors:** Slack, Google Drive, Gmail (connector-first, no Computer Use)

## Dual-Mode Pattern

```
IF input text present:
  → Follow-up mode (respond to Andy's message)
ELSE:
  → Scheduled run (full scan loop)
```

This is the universal pattern shared by all TTAI employees. See [[employee-framework]].

## Scheduled Run Loop

1. Read index.md, log.md for current state
2. Check inbox/ for new ingest files
3. Read Slack #ttai-employees for Fred, Mark-Lite, and Andy messages
4. Check Google Drive for updates
5. Update wiki pages (process ingests, propagate changes, maintain cross-refs)
6. Exploration pass (cross-domain patterns, risks, opportunities)
7. Post report to Slack #ttai-employees

## Follow-Up Mode

Read Andy's message. Could be a question, new information, correction, or instruction. Respond in Slack. Update wiki if needed. Skip the full scan loop.

## Migration Notes (from Cowork)

| Aspect | Cowork (old) | Routines (current) |
|--------|-------------|-------------------|
| Information gathering | Computer Use scanning Claude.ai conversations | Slack connector + inbox folder + Google Drive |
| State persistence | Local filesystem | GitHub repo |
| Reporting | Email to Andy | Slack #ttai-employees |
| Runtime | 15-30 min | 5-15 min |
| Failure modes | Browser timeouts, sandbox restrictions | Ephemeral branches (solved by pushing to main) |

## Links

- [[employee-framework]] -- Universal employee operating model
- [[ttai-slack-bridge]] -- Bridge infrastructure routing Slack to API
- [[claude-code-routines]] -- Platform documentation
- [[connectors-beat-computer-use]] -- Principle discovered during migration
- [[repos-are-employee-memory]] -- Principle discovered during migration

## Sources

- Wiki Agent migration session (2026-04-15)
- Slack #ttai-employees deployment messages
