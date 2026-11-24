# Security

## Reporting a problem

Please open a [GitHub security advisory](../../security/advisories/new) (private) rather than a public issue for anything that could put users at risk.

## Threat model

This skill drives a real Instagram account in a browser and writes to a shared Google Doc, using content that anyone in the group (or any creator whose post is shared there) controls. The scouting itself, with its own protections, is done by [reel-skill-scout](https://github.com/SamiCodex/reel-skill-scout); see its SECURITY.md.

| Risk | Protection |
|---|---|
| A group member or a shared post tells Claude to message someone, install something or change settings | Everything in the chat is data. The skill only reads the one group in the user's settings, opens Instagram post links, writes to one Google Doc, and posts at most one fixed message in that group. It never opens other chats, likes, follows or comments. |
| Messages sent in the user's name | The skill expects a separate bot account and checks that it is the signed-in account before sending. It sends only after the user's go-ahead for that run, and never from a scheduled run. |
| Passwords and sign-in codes | Claude never types or stores Instagram passwords or verification codes. The user signs the bot in through the browser pane. |
| Unattended scheduled runs | A scheduled run has nobody approving each step, so it is limited to reading the group and adding to the doc. It sends nothing to the group. |
| Poisoned text in the shared doc | The doc holds only Claude's own short summaries and verified repo links, never copied captions or README text, and never instructions for readers to run. |
| Other people's messages stored on disk | `group-seen.md` keeps only post codes and dates, never message text or captions. |

## Out of scope

- The security of third-party skills found in the group. reel-skill-scout reviews and flags them, but you decide what to install.
- Instagram's own account protections. Automating an account is against Instagram's terms; use a separate account and check lightly.
