---
type: concept
title: "MCP in AI Agents"
description: "How Model Context Protocol connects Claude Code to agent-building tools: configuring MCP servers, the 1-minute sales agent, tool permissions, and API/web-chat alternatives."
tags: [mcp, agents, tool-use, claude]
sources: [raw/claude-mcp-ai-sales-agents.md]
timestamp: 2026-08-17T17:00:00Z
---

# MCP in AI Agents

The sales-agent video is a real-world demo of Model Context Protocol (MCP): the whole product is delivered as an MCP server that an existing AI client can talk to. Sean opens Claude Code and simply asks, "Can I create a sales representative agent for my business? Yes, sir. Let's go." [00:00]. Setup is a config edit, not code: go to profile, then settings and developers, where MCP servers like Notion API and AutoManous are listed; you click edit config, copy the snippet from the MCP server's development repo, "and then open this clock underscore desktop config JSON, and then just paste that in" [00:53]. That JSON wiring turns the agent-creation platform into a set of tools Claude Code can invoke.

With MCP connected, plain conversation becomes tool orchestration. When Sean asks Claude Code to create an agent, "it's asking me for three things: company name, website URL, and my email. This is because my clock code has been set up with the MCP server from AutoManous" [01:02]. Given calendly.com and an email, the backend services scrape the website "to understand how do you take in inquiries from your customers, and how what kind of things or solutions are you providing" [01:36]. The whole goal is that "there's no leakage from customer inquiries when you're not in your office" [01:50], and the agent is created "within 1 minute" [01:58].

Tool use is permission-gated, which is the key agent-safety mechanic in the demo. When Sean wants to add his own booking link, the client "is using this MCP tool called app knowledge. All I need to do is just say allow" [03:22]. After approval, the knowledge base is updated and the agent can answer "Can I schedule a Calendly booking with you?" with a working link [03:35]. The agent starts out on the platform's servers and must be claimed via an email link ("claim your agent") before you own it; the same MCP-created agent is then deployable, editable, and testable on WhatsApp [04:00].

Verification is a security gate tied to identity: "in the training page, you can click on the sandbox mode, and then putting your website URL to confirm if your emails match with it. If it does, then it's going to verify it. If it does not, then your agent will remain unverified for security reasons" [04:49]. The video stresses the same point earlier when testing on WhatsApp: "if you're an employee or a CEO from Calendly, you'll be able to claim it using that email link with your own email domain so that there's no security issues. This must be verified by you" [02:44].

MCP is not the only integration path. For developers building SaaS or agency products, there is an API: create a key in settings under API access (a test key that "will expire in 3 days" [06:43]), then a curl call creates the company and the agent appears "directly in your agent hub because you're using the API keys. You don't even have to claim it" [07:13]. There is also an AI-agent web chat that generates an embeddable widget for a website [07:26]. The pitch closes with the MCP server on GitHub and "100 free credits, meaning 100 free AI generated responses for your clients" [08:23].

## Part of / Related

- [AI Sales Agents](/concepts/ai-sales-agents.md)
- [Automanus](/entities/automanus.md)
- [Anthropic](/entities/anthropic.md)
- [AI Agent Harness](/concepts/ai-agent-harness.md)

## Sources

- [claude-mcp-ai-sales-agents](/sources/claude-mcp-ai-sales-agents.md)
