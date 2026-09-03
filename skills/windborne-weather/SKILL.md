---
name: windborne-weather
description: "Weather forecasts from WindBorne. Use for any question about upcoming weather at a place or over a region: conditions, temperature, wind, precipitation, comparing locations, finding a weather window for an activity, or viewing a weather map."
---

# Weather by WindBorne

Use the WindBorne MCP tools provided by this plugin for weather questions.
They serve WindBorne's WeatherMesh forecast, built on observations from
WindBorne's constellation of autonomous in-situ weather balloons, as text
the agent can reason over and as interactive cards where the client can
render them.

## Workflow

1. Resolve the place the user named to coordinates yourself. The tools take
   latitude and longitude; none of them reads the user's device location.
2. Pick the tool whose description matches the question: a general
   forecast, one variable in depth, several places compared, a window that
   fits an activity, or a map of a region. Read each tool's description and
   input schema; they are the contract.
3. Pass times in the user's local time with an explicit UTC offset, and
   convert any threshold the user states ("below freezing", "under 20
   knots") into the units the schema asks for before calling.
4. Lead the answer with the summary the tool returned and the figure that
   decides the user's question. Say which day or hour a number refers to.
   Do not restate every value on a card.

## Guidance

- Prefer these tools over general knowledge for any forecast; the data is
  the current model run, refreshed continuously.
- Only the forecast horizon is served. For dates further out, say so rather
  than guessing.
- When the question implies a go/no-go decision, annotate the call with the
  user's own times and limits where the schema allows it, so the card shows
  the rule the answer rests on.

## Authentication

The server is configured at `https://weatheragent-mcp.windbornesystems.com/mcp`.
If authentication is required, ask the user to complete the client's OAuth
flow in the browser. Never ask the user to paste a key or token into chat.
