# TTAI Slack Bridge

> Node.js Slack Bolt app that routes Andy's Slack replies to the correct employee routine API endpoint. Deployed on Railway free tier.
> Last updated: 2026-04-16

## What It Does

The bridge listens for Andy's messages in #ttai-employees and fires the correct employee's Routine API endpoint with the message as the `text` field. This enables two-way interaction: employees post reports to Slack, Andy replies, the reply triggers a follow-up run.

## Architecture

```
Andy replies in #ttai-employees
  -> Bridge identifies target employee (name prefix or thread context)
  -> Bridge fires Routine /fire endpoint with message as text field
  -> Employee routine runs in follow-up mode
  -> Employee posts response back to #ttai-employees
```

## Technical Details

- **Framework:** Slack Bolt (Node.js)
- **Connection:** Socket Mode (no public URL required)
- **Hosting:** Railway free tier (auto-deploys from GitHub on push)
- **Repo:** Separate GitHub repo (not the wiki repo)
- **Config:** Employee API endpoints and tokens stored as Railway env vars

## Current Employees Routed

| Employee | Routine Trigger | Status |
|----------|----------------|--------|
| Wiki | API endpoint configured | Active |
| Mark-Lite | Not yet configured | Pending migration |
| Fred | Not yet configured | Pending migration |

## Adding a New Employee

1. Create the employee's Routine (schedule + API triggers)
2. Get the Routine's API endpoint URL and token
3. Add endpoint + token to Railway env vars
4. Update bridge code to recognise the new employee's name prefix
5. Deploy (auto-deploys on push to the bridge repo)

## Links

- [[employee-framework]] -- Universal employee operating model
- [[claude-code-routines]] -- Platform documentation
- [[wiki-agent-SKILL]] -- First employee using this bridge

## Sources

- Wiki Agent migration session (2026-04-15)
