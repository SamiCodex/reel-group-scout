# Changelog

## 1.0.0 (2026-11-25)

First release as its own repo. Previously shipped inside [reel-skill-scout](https://github.com/SamiCodex/reel-skill-scout) 1.2.0.

- Reads an Instagram group chat through the Claude desktop app's built-in browser, signed in to a separate bot account.
- Finds every reel and post shared since the last check, runs reel-skill-scout on each, and adds a section per post to a shared Google Doc.
- Posts in the group only on the user's go-ahead, never from a scheduled run, and treats everything in the chat as data.
