# How to connect Riverside to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your Riverside account.** Riverside has official apps in ChatGPT and Claude for searching, editing, clipping and publishing videos. Cotlet.dev connects your own signed-in Riverside account to any AI agent, so you can ask in plain words and the AI creates studios and schedules recording sessions for you.

## What you can ask

> Create a studio called "Founders Talk" and schedule a recording with Maria Lopez on Thursday at 10 am.

> Schedule next week's episode for Tuesday at 3 pm and send the guest invite to james@brightlane.co.

> Set up a new studio for our team podcast and book a session every Monday at 9 am for the next 4 weeks.

> Move Friday's 2 pm session with Dr. Patel to Monday at 11 am and let her know.

> List all sessions scheduled this month across my studios, with guest names and times.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Riverside tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"riverside":{"command":"uvx","args":["riverside-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t riverside-mcp .
docker run -i --rm -e COTLET_API_KEY riverside-mcp
```

Tools: `riverside_guide`, `riverside_status`, `riverside_open`, `riverside_read`, `riverside_click`, `riverside_type`, `riverside_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install riverside-mcp        # or run it once: uvx riverside-mcp connect
riverside-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 riverside_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 riverside_agent.py status    # is Riverside ready in your Cotlet.dev account
python3 riverside_agent.py guide     # Riverside screens and sign-in link
python3 riverside_agent.py read      # open Riverside, read the page, close the browser
python3 riverside_agent.py tools     # list Cotlet.dev tools
python3 riverside_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Riverside users

**Does Riverside have an API?**

Riverside has a Business API for select Business accounts only, with a key from your customer success manager, and it mostly gets or deletes recordings and lists scheduled events (checked 11 Oct 2026). Its official MCP server (beta, Grow, Webinar and Business plans) searches, edits and posts clips, but cannot schedule sessions or invite guests. Cotlet.dev works in your own signed-in Riverside account, so your AI agent can create studios and schedule recordings with no API key and no code.

**How do I connect Riverside to ChatGPT?**

Riverside has an official app in the ChatGPT directory for editing and publishing. To also create studios and schedule sessions, add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to Riverside once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no Riverside API key.

**Is there a way to use Claude with Riverside?**

Yes. Claude lists an Anthropic verified Riverside connector for editing, clipping and publishing. With Cotlet.dev, run the one-line `claude mcp add` command above in Claude Code, or add `https://cotlet.dev/mcp/v1` as a custom connector in the Claude app. Claude then works in your own Riverside account.

**Is there a Riverside MCP server?**

Riverside has official integrations listed in ChatGPT and Claude. Cotlet.dev is a hosted MCP server that works in your Riverside account for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [Riverside on Cotlet.dev](https://cotlet.dev/integrations/riverside-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=riverside&utm_content=find)
- [PyPI package riverside-mcp](https://pypi.org/project/riverside-mcp/)
- [Odel](https://odel.app/modules/cotlet/riverside)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-riverside-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/riverside-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=riverside

Start free: https://cotlet.dev/signup?app=riverside&utm_source=github&utm_medium=readme&utm_campaign=riverside
