# InventList MCP

Model Context Protocol server for InventList.
**Agent-readable execution memory + the indie builder workspace.**

- **Live endpoint:** https://inventlist.com/mcp
- **Public manifest** (no auth): https://inventlist.com/api/v1/tools.json
- **Human onboarding guide:** https://inventlist.com/how-tos/mcp
- **All 26 tools, agent-facing reference:** https://inventlist.com/tools/cli/skills

## What is this?

Most MCP servers expose one thing — a database, a doc store, a search
index. InventList exposes a **founder's whole workspace**: 26 tools across
Nodepad (execution memory), Ships, Roadmaps, Stories, Collections, Sites,
and Teams. One install, one auth token, one workspace.

The wedge is **Nodepad** — agent-readable execution memory no other PKM
tool offers. Every pad exposes a `context.json` describing your active
role, which node was open, and what got captured but never filed. Your
next agent session reads it and resumes exactly where the last one
stopped.

## Install

### Claude Code

```bash
claude mcp add inventlist --transport http https://inventlist.com/mcp \
  --header "Authorization: Bearer YOUR_API_KEY"
```

### Claude Desktop

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "inventlist": {
      "transport": "http",
      "url": "https://inventlist.com/mcp",
      "headers": { "Authorization": "Bearer YOUR_API_KEY" }
    }
  }
}
```

### Cursor

Settings → MCP → **Add server**:

```
Name:   inventlist
URL:    https://inventlist.com/mcp
Header: Authorization = Bearer YOUR_API_KEY
```

Generate `YOUR_API_KEY` at
[inventlist.com/settings#developer](https://inventlist.com/settings#developer).

## Example prompts

- *"Resume my InventList nodepad `side-project` — what was I working on?"*
- *"Capture this thought into my `work-notes` pad: ..."*
- *"Toggle task 3 done on my roadmap for inventlist.com"*
- *"Draft a ship for my product `localvault` about the v1.2 release"*

## The 26 tools

| Family | Count | Purpose |
| --- | --- | --- |
| Nodepad | 6 | List pads, read per-pad context, read/write nodes & stickies |
| Roadmaps | 5 | List/read/create/update roadmaps, toggle tasks |
| Profile + portfolio | 8 | Your sites, ships, series, stories, teams, roundups, notifications |
| Ships, Stories, Collections | 4 | Draft ships (always status=draft), get stories, curate collections |
| Discovery + social | 3 | Search sites, list asks, list X accounts |

Full machine-readable list: https://inventlist.com/api/v1/tools.json

## Why this repo exists

The InventList web app is closed source. This repo is a thin public
companion whose only job is to host:

1. `smithery.yaml` — for [Smithery](https://smithery.ai)'s registry
   crawler
2. This README — for humans landing here from GitHub search

The contract is the surface:

- `tools.json` is generated live from the registry — see
  https://inventlist.com/api/v1/tools.json
- Every MCP tool is mirrored 1:1 by a REST endpoint under `/api/v1/*`
- Editing one declaration updates both surfaces — there's no separate
  manifest to maintain

## Sister tools

- [LocalVault](https://github.com/inventlist/localvault) — zero-infra
  secrets manager with its own MCP server (open source)
- [Rails Markup](https://github.com/inventlist/rails-markup) —
  point-and-click annotation tool for AI agents (open source)
- [InventList CLI](https://github.com/inventlist/cli-releases) — manage
  sites, ships, series, and collections from the terminal

## License

MIT — for the manifest in this repo.

The InventList web app, including the MCP server implementation, is
closed source. The contract above is the public surface.

## Contact

[@nauman](https://inventlist.com/@nauman) on InventList ·
nauman@intellecta.co
