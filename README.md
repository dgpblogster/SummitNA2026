# Community Summit North America 2026

Session materials from **Mariano Gomez Bent** at Community Summit North America 2026, Nashville, TN, October 11-15, 2026.

## Sessions

| Session | Materials |
|---|---|
| **Same Agent, Two Architectures: When MCP Wins (And When It Doesn't)** | [Deck, handout and lab](#same-agent-two-architectures-when-mcp-wins-and-when-it-doesnt) |

---

## Same Agent, Two Architectures: When MCP Wins (And When It Doesn't)

Copilot Studio gives you several ways to hand an agent a capability: connectors, REST API tools and MCP servers. This session builds the same project health agent twice, once with connectors and once with MCP, asks both the same questions, and then changes what the MCP agent can do live, without touching or republishing the agent.

**The takeaway:** moving from a connector to an MCP server doesn't make the agent smarter. In both cases the agent decides when to call a tool. What changes is **who owns the tools**: each agent (connector) or the server (MCP).

> *"When many agents need the same tools, and those tools keep changing, that's your MCP signal."*

### In this repo

| File | What it is |
|---|---|
| [`same-agent-two-architectures-deck.pptx`](same-agent-two-architectures/same-agent-two-architectures-deck.pptx) | The slide deck as presented |
| [`same-agent-two-architectures-handout.pdf`](same-agent-two-architectures/same-agent-two-architectures-handout.pdf) | Printable handout: three slides per page with space for notes, plus the demo question script |

### What the session covers

1. **The setup.** MCP will not replace your connectors. The right question is what your agent needs to do.
2. **Project Orion.** A fictional enterprise release under pressure, with sprint data in SQL Server and issues in GitHub.
3. **Three tools, three jobs.** Connectors, REST API tools and MCP servers, and what actually changes between them.
4. **Demo 1: the connector agent.** SQL Server (through the on-premises data gateway) and GitHub connectors reason across both sources just fine. The cost shows up when something changes: edit, republish, repeat, in every agent.
5. **Two architectures.** The live demo setup versus the cloud design you'd actually ship.
6. **Demo 2: the MCP agent.** A new tool is switched on at the server, and the agent picks it up without being edited or republished.
7. **When to reach for MCP.** A two-question decision framework, and an honest warning about complexity.

### The decision framework

| Agents using these tools | How often the tools change | Recommendation |
|---|---|---|
| One | Stable | **Connector wins.** Simple, governed, done |
| One | Changing | **Connector, republish as needed.** With one agent, republishing is cheap |
| Many | Stable | **Evaluate MCP.** A shared custom connector may be enough |
| Many | Changing | **MCP is right.** Change it once, every agent follows |

> *"The most expensive architectural mistake is reaching for MCP because it sounds modern."*

---

## Build it yourself: the lab

Everything shown on stage is in the hands-on lab:

**[github.com/dgpblogster/project-orion-lab](https://github.com/dgpblogster/project-orion-lab)**

| Lab component | What you get |
|---|---|
| SQL setup script | The `ProjectOrion` database: sprints, work items, health metrics, release plan, the forecast feature flag, and the 7 stored procedures the connector agent calls |
| GitHub issues script | Creates the 35 issues that correlate with the SQL data |
| Custom MCP server | TypeScript server exposing 7 tools, plus a feature-flagged release forecast tool. Includes both the GitHub Copilot prompt that generates it and the reference code shown on stage |
| Project health dashboard | Next.js dashboard that follows the demo questions and holds the switch that "deploys" the forecast tool. Prompt and reference code |
| Copilot Studio agents | Prompts, instructions and tool setup for both the connector agent and the MCP agent |

Follow the lab README step by step and you can rebuild both demos on your own machine.

## The companion repo: Project Orion issues

**[github.com/dgpblogster/project-orion](https://github.com/dgpblogster/project-orion)**

The GitHub half of the demo data: the issues both agents read, deliberately correlated with records in the SQL database (for example, critical bugs #25, #26 and #27 match the three blockers in the sprint data). There is no application code there; the issues are the content. Please don't open, close or comment on them, since the demo depends on their current state. To build your own copy, follow Step 2 of the lab README.

---

## About the speaker

**Mariano Gomez Bent**, Chief Product & Technology Officer at Mekorma. Former Microsoft Business Applications MVP (2008-2024), Microsoft Certified Trainer and international speaker, focused on practical AI architecture for real-world enterprise scenarios.

- LinkedIn: [linkedin.com/in/marianogomezbent](https://www.linkedin.com/in/marianogomezbent/)
- YouTube: [youtube.com/@workbench-blog](https://www.youtube.com/@workbench-blog)
- Blog: [theworkbench.blog](https://www.theworkbench.blog/)
- GitHub: [github.com/dgpblogster](https://github.com/dgpblogster)

---

*Project Orion is fictional. All data in the lab and companion repo is sample data for a conference demo.*
