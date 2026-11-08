# How to connect Appointy to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your Appointy account.** We found no official Appointy app in the ChatGPT or Claude directories, and the third-party Zapier MCP integration lists one action: Create Customer. Cotlet.dev connects your own signed-in Appointy account to any AI agent, so you can ask in plain words and the AI books, reschedules and reminds clients for you.

## What you can ask

> Book Maria Lopez for a 60-minute consultation with Dr. Patel on Thursday at 10 am and send her the confirmation.

> What does next Monday look like per staff member? List any gaps longer than 45 minutes.

> Move all of Tom's Friday afternoon appointments to Saturday morning and notify each client.

> Cancel the 3 pm group class on Wednesday and tell the 8 people booked into it.

> Send a reminder to everyone booked for tomorrow who hasn't confirmed yet.

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

This repo is a real MCP server. It speaks MCP over stdio, lists its Appointy tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"appointy":{"command":"uvx","args":["appointy-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t appointy-mcp .
docker run -i --rm -e COTLET_API_KEY appointy-mcp
```

Tools: `appointy_guide`, `appointy_status`, `appointy_open`, `appointy_read`, `appointy_click`, `appointy_type`, `appointy_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install appointy-mcp        # or run it once: uvx appointy-mcp connect
appointy-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 appointy_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 appointy_agent.py status    # is Appointy ready in your Cotlet.dev account
python3 appointy_agent.py guide     # Appointy screens and sign-in link
python3 appointy_agent.py read      # open Appointy, read the page, close the browser
python3 appointy_agent.py tools     # list Cotlet.dev tools
python3 appointy_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Appointy users

**Does Appointy have an API or developer documentation?**

Appointy lists private API access only on its Enterprise plan; its Zapier app can only create customers. Cotlet.dev works in your own signed-in Appointy account on any plan, so your AI agent can book, approve, reschedule and cancel appointments.

**How do I connect Appointy to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to Appointy once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no Appointy API key.

**Is there a way to use Claude with Appointy?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own Appointy account.

**Is there an Appointy MCP server?**

Appointy has no official MCP server and no official app in ChatGPT or Claude (checked November 2026). Cotlet.dev is a hosted Appointy MCP server that works in your own account, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [Appointy on Cotlet.dev](https://cotlet.dev/integrations/appointy-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=appointy&utm_content=find)
- [PyPI package appointy-mcp](https://pypi.org/project/appointy-mcp/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-appointy-to-ai-agents-guide)

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
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Teachable MCP](https://github.com/cotlet-connect/teachable-mcp)
- [Vagaro MCP](https://github.com/cotlet-connect/vagaro-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Zoopla MCP](https://github.com/cotlet-connect/zoopla-mcp)
- [Dribbble MCP](https://github.com/cotlet-connect/dribbble-mcp)
- [Hostelworld MCP](https://github.com/cotlet-connect/hostelworld-mcp)
- [Mashvisor MCP](https://github.com/cotlet-connect/mashvisor-mcp)
- [Rent Manager MCP](https://github.com/cotlet-connect/rent-manager-mcp)
- [ThriveCart MCP](https://github.com/cotlet-connect/thrivecart-mcp)
- [Fresha MCP](https://github.com/cotlet-connect/fresha-mcp)
- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [BookingKoala MCP](https://github.com/cotlet-connect/bookingkoala-mcp)
- [Milanote MCP](https://github.com/cotlet-connect/milanote-mcp)
- [Partiful MCP](https://github.com/cotlet-connect/partiful-mcp)
- [Contractor Foreman MCP](https://github.com/cotlet-connect/contractor-foreman-mcp)
- [Pixieset MCP](https://github.com/cotlet-connect/pixieset-mcp)
- [GlossGenius MCP](https://github.com/cotlet-connect/glossgenius-mcp)
- [ZenMaid MCP](https://github.com/cotlet-connect/zenmaid-mcp)
- [AroFlo MCP](https://github.com/cotlet-connect/aroflo-mcp)
- [Simpro MCP](https://github.com/cotlet-connect/simpro-mcp)
- [Workiz MCP](https://github.com/cotlet-connect/workiz-mcp)
- [Kickserv MCP](https://github.com/cotlet-connect/kickserv-mcp)
- [Service Autopilot MCP](https://github.com/cotlet-connect/service-autopilot-mcp)
- [Boulevard MCP](https://github.com/cotlet-connect/boulevard-mcp)
- [Mindbody MCP](https://github.com/cotlet-connect/mindbody-mcp)
- [Meevo MCP](https://github.com/cotlet-connect/meevo-mcp)
- [DaySmart MCP](https://github.com/cotlet-connect/daysmart-mcp)
- [Acuity Scheduling MCP](https://github.com/cotlet-connect/acuity-scheduling-mcp)
- [Jane App MCP](https://github.com/cotlet-connect/jane-app-mcp)
- [FieldEdge MCP](https://github.com/cotlet-connect/fieldedge-mcp)
- [Phorest MCP](https://github.com/cotlet-connect/phorest-mcp)
- [DINGG MCP](https://github.com/cotlet-connect/dingg-mcp)
- [Invoice Simple MCP](https://github.com/cotlet-connect/invoice-simple-mcp)
- [PhotoShelter MCP](https://github.com/cotlet-connect/photoshelter-mcp)
- [RazorSync MCP](https://github.com/cotlet-connect/razorsync-mcp)
- [ShootProof MCP](https://github.com/cotlet-connect/shootproof-mcp)
- [Invoice2go MCP](https://github.com/cotlet-connect/invoice2go-mcp)
- [Contractor+ MCP](https://github.com/cotlet-connect/contractor-plus-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/appointy-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=appointy

Start free: https://cotlet.dev/signup?app=appointy&utm_source=github&utm_medium=readme&utm_campaign=appointy
