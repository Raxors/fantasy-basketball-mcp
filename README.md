# Personal Fantasy Basketball MCP

A local Model Context Protocol (MCP) server for personal Yahoo Fantasy Basketball analysis with an AI assistant.

## Project status

This project is in the planning stage. This repository currently contains the project description; there is no working server or installable release yet. Yahoo Fantasy Sports API access has not yet been granted to this project.

The initial scope is a personal, non-commercial tool for one user and one NBA fantasy league in which that user participates. All capabilities below are planned and depend on API approval and the data made available by Yahoo.

## Purpose

The server will let an MCP-compatible AI assistant retrieve authorized fantasy data to answer questions about a team and its league. Analysis will use the league's actual settings and scoring categories.

Example questions:

- Which statistical categories are my team's strengths and weaknesses?
- How does my roster compare with this week's opponent?
- Which available players could help address a weakness in my lineup?
- How would a proposed trade change my team's statistical profile?
- What changed in my league's standings and recent transactions?

## Planned data access

The integration will request read access to:

- The authenticated user's basketball leagues and teams.
- League settings, scoring categories, and roster requirements.
- Teams, rosters, standings, matchups, and scores.
- Player statistics, position eligibility, and league availability.
- Free agents, waiver players, and league transaction history.

Requests will be limited to data that the authenticated account is authorized to access. The initial implementation will focus on a single selected league.

## Planned architecture

```text
MCP-compatible AI client
          |
          | Local MCP connection (stdio)
          v
Local Fantasy Basketball MCP server
          |
          | HTTPS requests authorized with Yahoo OAuth 2.0
          v
Yahoo Fantasy Sports API
```

The server will expose a small set of tools for retrieving league, team, matchup, and player information. The connected AI assistant will use the returned data as context for user-requested analysis.

## Read-only scope

The planned integration will retrieve fantasy data only. Lineup changes, player additions and drops, waiver claims, and trades will be performed manually through Yahoo Fantasy.

Yahoo's current [API access application](https://sports.yahoo.com/developer/access/) states that write access is unavailable.

## Planned data handling

- Use Yahoo OAuth 2.0 for explicit account authorization.
- Keep client secrets and OAuth tokens on the user's device and outside version control.
- Exclude credentials and tokens from MCP tool results and logs.
- Retrieve data on demand, with limited caching and backoff to reduce repeated requests and respect API limits.
- Return only data needed for the requested analysis and minimize unnecessary personal information about league members.
- Keep private league data and real API responses out of the public repository.

If the connected AI client uses a cloud model, fantasy data returned by MCP tools may be sent to that provider for processing. The MCP server itself is intended to run locally.

The initial project has no public data feed, paid service, or redistribution of Yahoo data.

## Development roadmap

- [ ] Obtain Yahoo Fantasy Sports API approval and review the applicable API agreement.
- [ ] Implement OAuth authorization, token refresh, and local credential storage.
- [ ] Implement read-only tools for leagues, settings, teams, and rosters.
- [ ] Add matchups, player statistics, available players, and transaction history.
- [ ] Add caching, rate-limit handling, and credential-safe error reporting.
- [ ] Document installation and configuration after a working prototype is available.

## References and attribution

- [Yahoo Fantasy Sports Developer Portal](https://sports.yahoo.com/developer/)
- [Yahoo Fantasy Sports API Documentation](https://sports.yahoo.com/developer/docs/)
- [Yahoo OAuth 2.0 Documentation](https://developer.yahoo.com/oauth2/guide/)

Fantasy data provided by [Yahoo Fantasy](https://sports.yahoo.com/fantasy/).

This is an independent project and is not affiliated with or endorsed by Yahoo or the NBA.
