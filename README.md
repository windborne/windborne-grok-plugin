# Weather by WindBorne for Grok Build

Ask Grok Build about the weather and get WindBorne's forecast back as
interactive weather apps: cards the MCP server returns alongside each
answer, rendered by the client and containing only forecast data.

[WindBorne Systems](https://windbornesystems.com) designs, builds, and
operates Atlas, a global constellation of long-duration autonomous weather
balloons that collect in-situ observations from the parts of the atmosphere
no other network reaches, and trains WeatherMesh, its AI forecast models,
on them. This plugin connects Grok Build to WindBorne's hosted MCP server,
which serves that forecast for any location or region, and ships one skill
that teaches the agent when and how to use it.

## Installation

In Grok Build, open `/plugin`, search for **WindBorne**, and install the
plugin.

The first time a tool runs, Grok Build opens WindBorne's authorization page
in your browser. Approve the connection and the tool call completes. Grok
Build stores the resulting token locally and refreshes it without asking
again.

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
PKCE. The `clientId` in `.mcp.json` is a public identifier, not a secret;
no API key or secret is needed or stored in this repository. Tokens are
held by Grok Build in its own credential store on your machine.

The plugin has no hooks, commands, local processes, or telemetry; the MCP
connection above is all it does.

## Support

Open an issue on this repository.

## Resources

- [WindBorne Systems](https://windbornesystems.com)
- [Weather Forecasts](https://windbornesystems.com/weather/)

## License

MIT. See [LICENSE](LICENSE).
