# Mercia Flooring

> Mercia Flooring Group: school flooring sales operation targeting schools in 30-mile radius, seasonal pipeline Jan--July.
> Last updated: 2026-04-29

## Overview
- **Company:** Mercia Flooring Group (Mercia Floors)
- **Shortname:** Mercia Flooring
- **Product(s):** [[mark]]
- **Status:** Active -- blocked on Entra/Manus app approval (Solaas IT)
- **Revenue:** £250 invoiced, £200/month projected

## Key Contacts
- Peter Clarke -- Director -- info@merciafloors.co.uk
- Jack Galbraith -- IT Apprentice, Solaas IT -- Jack.Galbraith@solaas.it
- Martin Neale -- Solaas IT (escalation contact) -- Martin.neale@solaas.it

## Current Status
Setup invoiced (INV-002, £250). School lists for all 4 target postcode areas built and ready. **Blocker has shifted:** the original app-password issue is unresolved, but the more immediate block is that Manus (publisher: Butterfly Effect PTE. LTD., verified by Microsoft) needs to be approved as an enterprise app in Entra. Jack at Solaas approved Zapier (21 Apr) but that was only a test -- the actual tool needed is Manus.

Andy has asked Jack to change Entra settings to "Allow user consent for apps from verified publishers" (Identity > Applications > Enterprise applications > Consent and permissions > User consent settings). This would let Pete self-approve verified apps without needing admin approval each time. Martin Neale (senior at Solaas) cc'd as escalation. Andy described this as "quite urgent" -- behind schedule on Pete's email campaigns.

**23 April:** Jack replied saying he'd applied the Entra consent setting ("Enterprise apps -> Consent and permissions"). Andy replied asking if Jack also approved the specific Manus app (Butterfly Effect PTE. LTD.).

**24 April:** Pete emailed (05:23) -- still getting "Need admin approval" when trying to connect 3rd party apps. Jack's consent setting fix didn't resolve it.

**5+ days silence from Solaas** after Pete's 24 Apr report. Karen flagged on 29 Apr: "Mercia / Solaas -- 5 days silent after Pete reported still failing." Cord drafted a follow-up chase to Jack/Martin specifically about Manus, cc'ing Pete -- left as Gmail draft for Andy to send.

**29 April (19:16):** Andy sent a second chase to Jack, cc'ing Martin and Pete: "Pete confirmed on Friday he's still hitting the 'need admin approval' message when connecting third-party apps to his Outlook, so the Entra setting hasn't taken effect yet." Entra/Manus still unresolved.

**29 April (14:02):** Pete emailed Andy with postcode priorities for w/c 4th May: CV1-CV35, CV47 starred as priorities. Andy acknowledged. This suggests Mercia outreach is proceeding (Pete actively sending targeting data) even while the Manus integration remains blocked -- likely Andy will send emails directly on Pete's behalf until the Entra issue resolves.

**Still blocked on Manus integration. But outreach proceeding via workaround.** Gmail send-as or manual sending by Andy appears to be the interim path. Seasonal pipeline runs Jan--July; every week of delay on automation eats into the window, but leads are flowing.

**Outlook / Entra app-password gotcha (caught 15 Apr):** Jack at Solaas IT attempted to generate an app password on Pete's behalf by logging in as himself. `mysignins.microsoft.com/security-info` only shows sign-in methods for whoever is currently authenticated -- so Jack saw his own account. Pete must generate the app password himself while logged in as Pete. Worth flagging on any future Entra/Microsoft 365 account set-up: "account holder must generate, not IT".

**Active Skills:**
- mercia-flooring-school-list-builder
- mercia-flooring-email-drafter

## Interaction Log
| Date | Summary |
|------|---------|
| 2026-04-29 | Andy chased Solaas again (19:16) -- Pete still hitting admin approval. Pete sent w/c 4 May postcode priorities (CV1-CV35, CV47). Outreach proceeding via workaround despite Manus blocker. |
| 2026-04-24 | Pete emailed (05:23) -- still getting "Need admin approval" when trying to connect 3rd party apps. Jack's consent setting fix didn't resolve it. 5+ days silence from Solaas follows. Karen flagged 29 Apr. Cord drafted follow-up chase to Jack/Martin re Manus, cc'ing Pete (Gmail draft for Andy to send). Still blocked; go-live further delayed. |
| 2026-04-23 | Jack replied saying he applied the Entra consent setting ("Enterprise apps -> Consent and permissions"). Andy replied asking if Jack also approved the specific Manus app (Butterfly Effect PTE. LTD.). |
| 2026-04-21 | Jack approved Zapier in Entra admin centre (was just a test). Andy clarified: need Manus (Butterfly Effect PTE. LTD.) approved, not Zapier. Also asked Jack to enable "Allow user consent for apps from verified publishers" in Entra settings. Martin Neale cc'd as escalation. Pete also tried connecting his email to ChatGPT -- also blocked. Andy: "This is quite urgent now as we're behind schedule." |
| 2026-04-16 | Solaas IT reportedly implemented Outlook/Entra OAuth fix today; Andy to verify 17 April. Delay pushed back Pete's whole week -- need to learn his calendar for next week. If verified, first school batch can launch same day. |
| 2026-04-14 | Outlook/Entra OAuth still outstanding with Solaas IT. 15 April go-live slipped. Gmail send-as workaround being considered to unblock first batch. |
| 2026-04-10 | Andy emailed Jack (Solaas IT) requesting IMAP + app passwords. Update email drafted/sent to Peter. School lists ready for all 4 areas. Easter break provides cover. |
| 2026-04-08 | Setup invoiced; work begun on school list and email automation |

## Links
- [[mark]] -- product (Mark-Lite automation)
- [[mercia-flooring-school-list-builder]] -- enrich school contact data
- [[mercia-flooring-email-drafter]] -- run outreach email campaigns

## Sources
- raw/ttai/claude.md
- raw/ttai/TTAI_Project_Context.md
- Gmail thread: "Admin Approval" (Jack.Galbraith@solaas.it, 2026-04-21)
- Gmail thread: "Outlook app password steps" (2026-04-15 to 2026-04-16)
