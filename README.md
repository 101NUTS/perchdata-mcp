# Perch Data MCP

[![smithery badge](https://smithery.ai/badge/perchdata/perch-data)](https://smithery.ai/servers/perchdata/perch-data)

Listed on Smithery: [perchdata/perch-data](https://smithery.ai/servers/perchdata/perch-data) ·
also in the official MCP registry as `io.github.101NUTS/perch-data`.

Six data tools for AI agents, served as MCP tools through Apify's hosted MCP server.
There is no server to install: point your MCP client at the URL below and sign in with
your own Apify account (OAuth) or pass your Apify API token. Runs are billed to your
Apify account at each actor's pay-per-event price.

**MCP endpoint (streamable HTTP):**

```
https://mcp.apify.com/?tools=fetch-actor-details,get-actor-output,perchpermits/kalshi-weather-markets-nws,perchpermits/polymarket-weather-markets-stations,perchpermits/tennis-matches-odds-form,perchpermits/nashville-building-permits,perchpermits/kitchen-floor-plan-takeoff,perchpermits/apify-store-trends
```

Auth: OAuth on first connect, or header `Authorization: Bearer <APIFY_TOKEN>`
(token from https://console.apify.com/account/integrations).

## Tools

| Tool (Apify actor) | What it returns | Price |
|---|---|---|
| [kalshi-weather-markets-nws](https://apify.com/perchpermits/kalshi-weather-markets-nws) | Kalshi daily high/low temperature ladders (24 US cities) joined to the NWS station that settles each one: strikes, prices, observations, forecast, official climate report. | $0.02 per city-day |
| [polymarket-weather-markets-stations](https://apify.com/perchpermits/polymarket-weather-markets-stations) | Polymarket daily highest/lowest temperature ladders (50 cities) joined to the airport station the market rules settle on, with high/low recomputed as the rules read it. | $0.02 per city-day |
| [tennis-matches-odds-form](https://apify.com/perchpermits/tennis-matches-odds-form) | ATP and WTA matches for a day with opening and current odds from 15+ bookmakers, rankings, last-10 form, surface record, head-to-head. | $0.02 per match |
| [nashville-building-permits](https://apify.com/perchpermits/nashville-building-permits) | Nashville / Davidson County TN building permits with licensed contractor, owner, open sub-trade permits and inspection stage; 22 scope presets. | $0.02 per record |
| [kitchen-floor-plan-takeoff](https://apify.com/perchpermits/kitchen-floor-plan-takeoff) | Kitchen or bath floor plan (SVG), cabinet takeoff (CSV) and quote totals from one JSON room spec; validates the layout. | $0.25 per plan |
| [apify-store-trends](https://apify.com/perchpermits/apify-store-trends) | Apify Store demand by niche: users, runs, fail rate, rating, price, leader share and gap flags. | $0.001 per actor row |

Weather and tennis data come from free official or public sources; see each actor's page
for sources, input schema and verification notes.

## Client setup

**Claude Code**

```bash
claude mcp add --transport http perch-data "https://mcp.apify.com/?tools=fetch-actor-details,get-actor-output,perchpermits/kalshi-weather-markets-nws,perchpermits/polymarket-weather-markets-stations,perchpermits/tennis-matches-odds-form,perchpermits/nashville-building-permits,perchpermits/kitchen-floor-plan-takeoff,perchpermits/apify-store-trends" --header "Authorization: Bearer $APIFY_TOKEN"
```

**Cursor / VS Code / any client that reads `mcp.json`**

```json
{
  "mcpServers": {
    "perch-data": {
      "url": "https://mcp.apify.com/?tools=fetch-actor-details,get-actor-output,perchpermits/kalshi-weather-markets-nws,perchpermits/polymarket-weather-markets-stations,perchpermits/tennis-matches-odds-form,perchpermits/nashville-building-permits,perchpermits/kitchen-floor-plan-takeoff,perchpermits/apify-store-trends",
      "headers": { "Authorization": "Bearer <APIFY_TOKEN>" }
    }
  }
}
```

Leave out `headers` to use OAuth sign-in instead.

**Claude Desktop / claude.ai:** Settings > Connectors > Add custom connector, paste the
endpoint URL above, and sign in to Apify when prompted.

**Local (stdio), for clients without remote support**

```json
{
  "mcpServers": {
    "perch-data": {
      "command": "npx",
      "args": ["-y", "@apify/actors-mcp-server", "--tools", "fetch-actor-details,get-actor-output,perchpermits/kalshi-weather-markets-nws,perchpermits/polymarket-weather-markets-stations,perchpermits/tennis-matches-odds-form,perchpermits/nashville-building-permits,perchpermits/kitchen-floor-plan-takeoff,perchpermits/apify-store-trends"],
      "env": { "APIFY_TOKEN": "<APIFY_TOKEN>" }
    }
  }
}
```

Only need one tool? Keep just that actor in the `tools` list.

## About

Built and maintained by Perch Data (Apify username `perchpermits`). Actor source:
https://github.com/101NUTS/perchpermits-actors. Also available to agents on Virtuals ACP
as "Perch Data". This repository holds listing metadata only; the MCP server itself is
Apify's (https://docs.apify.com/platform/integrations/mcp).

License: MIT
