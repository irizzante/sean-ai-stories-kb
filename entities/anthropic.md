---
type: entity
title: "Anthropic"
description: "Anthropic and Claude as they appear on the channel: Claude Code as the MCP sales-agent front-end, Claude Opus 4.8 in the Kimi K3 benchmark, and Claude as Sean's explainer and harness collaborator."
tags: [company, claude, mcp, benchmark]
sources: [raw/you-can-learn-why-kimi-k3-blew-up.md, raw/claude-mcp-ai-sales-agents.md]
timestamp: 2026-08-17T17:00:00Z
---

# Anthropic

Anthropic shows up on the channel as the maker of the AI Sean most visibly works through. The sales-agent video opens inside Claude Code, Anthropic's coding client, as the interface for the entire demo: "A clock code. Can I create a sales representative agent for my business? Yes, sir. Let's go." [00:00]. Claude's MCP support is what makes the demo possible — the AutoManous MCP server is registered under Claude's settings/developers panel and pasted into the claude_desktop_config.json file [00:35], after which "my clock code has been set up with the MCP server from AutoManous" and Claude Code itself collects the inputs and drives agent creation [01:10].

Anthropic's flagship model also appears as a benchmark competitor. Claude Opus 4.8 was one of the ten models raced in the Kimi K3 comparison, where it finished second on grades with 7.9 (behind Grok 4.5's 8.3) [17:26]. Behaviorally it stood out for restraint: during the web-search task, "Anthropic only searched once" while other models searched two or three times [15:41]. Cost is where Sean is loudest: "whoever is using Anthropic APIs, Jesus Christ, we're using so much more money than the rest of the models" [12:45], with Anthropic's token usage almost doubling Kimi's [14:38] and Opus 4.8 sitting at the expensive end alongside Fable 5 [12:31].

Claude also plays a recurring role as explainer and collaborator. When Sean needs the math behind delta attention explained, "I asked Claude for an answer. What Claude said is very clear" [06:16] — the running-average analogy for Kimi's linear attention comes from that conversation [06:41]. At the end of the video he jokes that the harness repo has "600 readers, including myself and Claude" [19:53], treating Claude as a co-contributor to the agent-harness project.

That collaboration extends to the channel's memory work: Claude Opus 4.8 is one of the models run through the Waku harness's memory gates in the same video, retrieving semantic memory and calling calendar tools alongside Kimi and the others [10:28]. The harness's memory system — durable semantic memory, episodic memory, and chat logs [10:00] — is model-agnostic, and Claude is both a client of those memory layers and the tool (via Claude Code and MCP) Sean uses to build them.

## Part of / Related

- [MCP in AI Agents](/concepts/mcp-in-ai-agents.md)
- [AI Sales Agents](/concepts/ai-sales-agents.md)
- [Kimi K3](/entities/kimi-k3.md)
- [Mixture of Experts](/concepts/mixture-of-experts.md)
- [Agent Memory System](/concepts/agent-memory-system.md)

## Sources

- [claude-mcp-ai-sales-agents](/sources/claude-mcp-ai-sales-agents.md)
- [you-can-learn-why-kimi-k3-blew-up](/sources/you-can-learn-why-kimi-k3-blew-up.md)
