# Weather by WindBorne for Grok Build, Cursor, and Grok Bot

Ask Grok Build, Cursor, or Grok Bot about the weather and get WindBorne's
forecast back as interactive weather apps: cards the MCP server returns
alongside each answer, rendered by the client and containing only forecast
data.

[WindBorne Systems](https://windbornesystems.com) designs, builds, and
operates Atlas, a global constellation of long-duration autonomous weather
balloons that collect in-situ observations from the parts of the atmosphere
no other network reaches, and trains WeatherMesh, its AI forecast models,
on them. This plugin connects each of those hosts to WindBorne's hosted MCP
server, which serves that forecast for any location or region, and ships
one skill that teaches the agent when and how to use it.

## Installation

### Grok Build

In Grok Build, open `/plugin`, search for **WindBorne**, and install the
plugin.

The first time a tool runs, Grok Build opens WindBorne's authorization page
in your browser. Approve the connection and the tool call completes. Grok
Build stores the resulting token locally and refreshes it without asking
again.

### Cursor

Install **Weather by WindBorne** from the Cursor Marketplace, either from
its listing on cursor.com or from **Customize → Plugins** inside Cursor.

The first time a tool runs, Cursor opens WindBorne's authorization page in
your browser. Approve the connection and the tool call completes.

### Grok Bot

Grok Bot has no plugin catalog of its own; it installs plugins from the
Cursor Marketplace. A Teams admin allows the plugin under
**Teams Marketplace → Integrations**, after which it is available to the
team. The same authorization page appears the first time a tool runs.

## What you can ask

- The forecast for a place, from today out to the current forecast horizon
- One variable in depth: wind, temperature, precipitation, pressure, cloud cover
- Several places compared side by side
- When an activity fits the weather, judged against your own limits
- An animated weather map over a region

The exact tool set is served by the MCP server and may grow; the agent
reads each tool's description and schema at connection time.

## Example prompts

```text
What's the weather in Lisbon this weekend?
```

```text
Plot the wind at Crissy Field on Saturday. I sail if it stays under 20 knots.
```

```text
Compare Denver and Salt Lake City for a hike next Tuesday.
```

```text
Show me precipitation and pressure over the North Atlantic.
```

## Authentication and security

The plugin talks to exactly two WindBorne endpoints:

- `https://weather-mcp.windbornesystems.com/mcp`, the MCP server.
- `https://app.windbornesystems.com`, the OAuth 2.1 authorization server
  the MCP server points to.

Authorization uses the standard MCP OAuth flow with a public client and
PKCE. Each host reads its own server configuration: Grok Build reads
`.mcp.json` (`oauth.clientId`) and Cursor reads `mcp.json`
(`auth.CLIENT_ID`). Both values are public client identifiers, not
secrets; no API key or secret is needed or stored in this repository.
Tokens are held by the client: on your machine for Grok Build and Cursor
desktop, on Cursor's side for Cursor web and Grok Bot.

The plugin has no hooks, commands, local processes, or telemetry; the MCP
connection above is all it does.

## Support

Open an issue on this repository.

## Resources

- [WindBorne Systems](https://windbornesystems.com)
- [Weather Forecasts](https://windbornesystems.com/weather/)

## License

MIT. See [LICENSE](LICENSE).
