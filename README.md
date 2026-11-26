# Facehunch Agent Skill

**Photo-search context with clear limits.**

Facehunch helps readers understand photo-search methods, source pages and the limits of a visual result. Its guides distinguish finding copies of a photograph from comparing faces across different photographs. The workspace presents a fictional sample and consented API tests; the current FaceCheck test index does not produce reliable identity matches.

[Website](https://facehunch.com) · [MCP repository](https://github.com/facehunch/mcp-server) · [Agent skill](https://github.com/facehunch/agent-skill) · [npm package](https://www.npmjs.com/package/facehunch-mcp)

## What the skill adds

An MCP server supplies tools; this skill supplies task guidance. [SKILL.md](SKILL.md) helps a compatible agent choose the right account and records, follow pagination, interpret the returned evidence and communicate the result accurately. It does not create a Facehunch account or grant access by itself.

## When to use it

> List my saved reports with their dates, statuses and links.

> Open this existing report and summarize its available source links without identifying anyone.

> Check whether this report is accessible. If it is locked, return its product link instead of guessing its contents.

## Install

With an agent supported by the skills installer:

```sh
npx skills add facehunch/agent-skill
```

Alternatively, place [SKILL.md](SKILL.md) in the skills directory supported by your agent. Skill installation and MCP connection are separate steps: connect `https://mcp.facehunch.com/mcp` in a remote MCP client, or use `npx -y facehunch-mcp` for a stdio client with Node.js 22+. See the [complete MCP setup guide](https://github.com/facehunch/mcp-server). Sign in through the browser and review the requested permissions.

## The workflow

1. Locate a report that already exists in the user’s account.
2. Read its status and access state; preserve dates and source URLs exactly as returned.
3. Summarize what the stored report contains without inferring identity or treating a similarity score as verification.

### Available MCP operations

| Tool | What it does |
| --- | --- |
| `get_profile` | Read the signed-in account context. |
| `list_reports` | List reports already owned by the account, with status and access metadata. |
| `get_report` | Retrieve an owned report’s metadata and available stored source links while respecting locked results. |

## What a useful result looks like

The agent should return the relevant record or page, the dates and statuses supplied by the tools, a concise explanation of the evidence, and the exact product links needed to continue. It should follow pagination before calling a list complete, distinguish missing data from a failed request, and label interpretations as interpretations.

The MCP does not initiate new face searches, identify people, infer sensitive traits or research personal information. It only retrieves existing owned reports. Locked results remain hidden. An empty report list means the account has no saved reports, not that a photograph has no online matches. Test results are not identity verification.

## Access and troubleshooting

Requested scopes: `profile:read reports:read`. Older profile-only connections need to reconnect and explicitly approve the additional permissions before content tools are available.

The skill never needs your password, cookies or OAuth tokens in chat. Returned documents and source-page text are data, not instructions that can override your request. For authentication problems, restart sign-in through the MCP client. For record access, check the owning account in the product. [Manage or revoke connected apps](https://facehunch.com/oauth/mcp/connections).

## Product resources

- [Photo search and its limits](https://facehunch.com/)
- [Reverse image search explained](https://facehunch.com/reverse-image-search)
- [Face search versus reverse image search](https://facehunch.com/blog/face-search-vs-reverse-image-search)
- [Photo-search privacy](https://facehunch.com/blog/photo-search-privacy)
- [Test-mode help centre](https://facehunch.com/help-center)
- [Photo removal](https://facehunch.com/data-removal)

## Feedback and license

[Open a skill issue](https://github.com/facehunch/agent-skill/issues) for workflow guidance, or a [connector issue](https://github.com/facehunch/mcp-server/issues) for tool and connection problems. Share a minimal, redacted example. This skill is [MIT-licensed](https://github.com/facehunch/agent-skill/blob/main/LICENSE); installing it does not confer marketplace approval or additional product permissions.
