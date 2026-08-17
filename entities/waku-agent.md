---
type: entity
title: "Waku Agent"
description: "Sean's open-source, local-first personal AI assistant covering harness, loop, memory, eval, and LLM Ops, with agent graphs."
tags: [waku-agent, harness, open-source, local-first]
sources: [raw/you-can-learn-ai-agent-harness-in-real-code.md, raw/you-can-learn-ai-agent-graph-engineering.md, raw/you-can-learn-pi-minimal-coding-agent-harness.md]
timestamp: 2026-08-17T17:00:00Z
---

# Waku Agent

Waku-Agent is Sean's own open-source project (GitHub: Shen Sean Chan / Waku-Agent), created to demonstrate every pillar of agent system design in real code: "I have open sourced a local first-person assistant that will cover the entire four pillars that matters to an Asian system today, which is harness, loop, memory, eval and LM ops" [00:07-00:16]. Within a few weeks it passed "more than 700 stars" [01:13-01:15] and gained a pip package: "recently, we released a new package in Python called waku-agent" [11:23-11:28]. It is deliberately local: "everything you have seen right now is local... You literally own this agent, just like Hermes, just like Openclaw" [04:29-04:34, 13:38-13:43].

The harness starts with a gateway and a retrieval-gated memory system. Gateways include the chat dashboard, Telegram (via BotFather), and a voice mode whose wake word is "Waku Waku" - "in Japanese is Waku Waku. So that's why I wanted Waku Waku to be the wake up word for this voice agent" [16:11-16:15]. Incoming questions pass "a retrieval gate here deciding if we should retrieve or not," which then pulls from procedural memory (skills like "resolve the relative dates, check the memory context for attendees' preferences, call the tool create event" [10:19-10:29]), semantic memory (`memory.md` durable facts - Sergey, Raj, Vincent), or episodic memory ("a dated event. For example, I was asking it to help me label all the World Cup games" [17:18-17:27]), with semantic facts consolidated in the background [17:28-17:36]. The system prompt is the editable `soul.md` in the dashboard [06:40-06:44]. The headline demo: "find me the rest of the World Cup games and add all of them to my calendar," which looped through the `search web` and `create event` tools and landed real events on the local calendar [00:27-01:36].

Loop, eval, and LLM Ops are all visible. The agent loop runs "by default... the maximize maximum iterations to be 10... until it reaches the goal" [16:40-16:47]. The eval folder splits into `deterministic` rule tests (Apple Calendar and working memory checks) and `judge` tests where "we have Anthropic as a judge" for response quality, run automatically after each reply [08:49-10:08]. Tracing is built in locally: "you can see the exact tracing of how much tokens, how much money I have spent, how many LLM calls," what activated the retrieval gate, and "what are some of the tasks that took the longest time. So, the one that I asked about with the World Cup games took me almost 100 seconds" - all stored in local trace files, with an upgrade path to "Superbase or just use LangFuse directly" [03:13-03:44, 08:35-08:40].

The graph video added agent graphs and community workflows. Waku gained a graph tab with two predefined workflows: `triage` (start, then classify whether agent calls are needed while checking the calendar in parallel) and `gather` (scan GitHub, search the web, check calendar and memories in parallel, then synthesize), both invoked through chat or `/gather` [12:44-14:28]. Under the hood they are node-and-edge definitions - "Tool calls, LLM calls, agent calls, router" - and contributors can add workflows as `.py` files that become available to everyone [17:34-19:13]. On benchmarks, a gather run surfaced that "Harrison Chase published your harness, your memory, and your own videos in Harness Eval our ranking" [14:52-14:59]. Waku also showcases harness composability: its `delegate task` tool spawns sub-agents that call the Pi coding agent's CLI to write code - "your own sub agent can call Pi Agent as the coding agent to finish the task for you" [01:15-01:24].

## Part of / Related

- [Agent Graph Engineering](../concepts/agent-graph-engineering.md)
- [AI Agent Harness](../concepts/ai-agent-harness.md)
- [Loop Engineering](../concepts/loop-engineering.md)
- [LLM Ops](../concepts/llm-ops.md)
- [Pi Coding Agent](../entities/pi-coding-agent.md)

## Sources

- [you-can-learn-ai-agent-graph-engineering](/sources/you-can-learn-ai-agent-graph-engineering.md)
- [you-can-learn-ai-agent-harness-in-real-code](/sources/you-can-learn-ai-agent-harness-in-real-code.md)
- [you-can-learn-pi-minimal-coding-agent-harness](/sources/you-can-learn-pi-minimal-coding-agent-harness.md)
