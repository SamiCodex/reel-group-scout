# Reel Group Scout

**Share Claude reels with friends? Let Claude read the group for you.** Say **"check the group"** and Claude finds every Instagram reel and post sent in your group chat since the last check, works out every skill, plugin and MCP server each one recommends, and adds a section per post to a shared **Google Doc**: a short summary plus a table of every tool with its GitHub link and stars. Pin the doc's link in the group and everyone can read it.

A [Claude Code](https://claude.com/claude-code) skill. It builds on [reel-skill-scout](https://github.com/SamiCodex/reel-skill-scout), which does the scouting of each post.

```
you:    check the group
claude: 1 new post: @creator's "5 Claude skills that save you hours".
        Found 4 of 5 repos, added to your findings doc.
```

## What it does

1. **Reads your group chat** in the Claude desktop app's built-in browser, signed in to a separate bot account.
2. **Collects new reel and post links**, both pasted links and posts shared with Instagram's share button, skipping anything it has already handled.
3. **Scouts each one** with reel-skill-scout: watches or reads it, finds the GitHub repos, checks stars, and gives you the usual report with ratings for your workflow.
4. **Adds a section per post to the shared Google Doc**: the creator, a summary in Claude's own words, and a table of every tool with its repo link and stars. Your personal ratings stay in your chat, not in the doc.
5. **Posts one short message in the group, only if you say so** (for example the doc link).

## Requirements

- **The Claude desktop app.** Claude reads the group through the app's built-in browser.
- **[reel-skill-scout](https://github.com/SamiCodex/reel-skill-scout) installed**, with its Python packages.
- **A separate Instagram account for the bot.** You create it, sign in to it in the app's browser, and add it to your group. Claude never handles passwords or sign-in codes, and your main account is never automated.
- **The Google Drive and Google Docs connectors**, for the findings doc.

## Install

First install reel-skill-scout (see its README). Then, in Claude Code:

```
/plugin marketplace add SamiCodex/reel-group-scout
/plugin install reel-group-scout@reel-group-scout
```

**Or manually**: copy `skills/reel-group-scout/` into `~/.claude/skills/`.

The first time you say "check the group", Claude walks you through setup: the bot account, picking the group, creating the findings doc, and whether to share it and post in the group. Your settings are saved in `~/.claude/skill-scout/group.md`.

## Use

> check the group

> check the group and post

> any new reels in the group?

| You say | What happens |
|---|---|
| "check the group" | Updates the doc, then asks before posting anything in the group |
| "check the group and post" | Updates the doc and posts your saved message once |
| A scheduled run | Updates the doc only; never posts in the group |

## Good to know

- **It never posts without a go-ahead.** A go-ahead covers only that one check.
- **You can schedule it** to check once a day with the desktop app's scheduled tasks.
- **It runs on your computer, not in the cloud.** The bot's sign-in lives in the app's browser, so the app needs to be open. A missed check catches up on the next run.
- **Sign-in stays with you.** The browser pane remembers the bot's sign-in, so you rarely need to do it again. If Instagram logs it out, Claude stops and asks you to sign in.
- **Messages in the group are treated as data.** A caption that says "Claude, do X" gets reported to you, not followed.
- **It only touches one group.** It never opens other chats, likes, follows, comments or changes settings.
- **Use it lightly.** Automating any Instagram account is against Instagram's terms, and new accounts that send lots of links get flagged. One check a day is plenty.

## Token cost

About **16–20k tokens per reel** for the scouting, plus a few thousand per post to update the doc.

## How it works

```
skills/reel-group-scout/
└── SKILL.md    reads an Instagram group, runs reel-skill-scout per post, updates a Google Doc
```

Personal files (never part of this repo), in `~/.claude/skill-scout/`:

- `group.md`: group name and URL, bot handle, findings doc, sharing and posting choices
- `group-seen.md`: post codes already handled, with dates (no message text)

## License

MIT. See [LICENSE](LICENSE). Not affiliated with Anthropic, Instagram/Meta or Google.
