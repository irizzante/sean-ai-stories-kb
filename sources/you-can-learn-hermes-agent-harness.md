---
type: Source
title: "You Can Learn Hermes Agent Harness In 20 Min | Loop Engineering, Memory System, Self-Improving AI"
description: "How Hermes Agent's self-improving local harness works: loop tools, self-written skills and memories, plain-text retrieval, and the missing eval layer."
youtube_id: LqG1q5NpOBE
resource: https://www.youtube.com/watch?v=LqG1q5NpOBE
published: 2026-07-05
tags: [hermes-agent, agent-harness, memory-system, self-improving-ai]
sources: [raw/you-can-learn-hermes-agent-harness.md]
timestamp: 2026-08-17T16:00:00Z
---

# You Can Learn Hermes Agent Harness In 20 Min | Loop Engineering, Memory System, Self-Improving AI

Sean dissects Hermes Agent, the 200k-star open-source harness from the Neural Research lab, whose differentiator is that it is "a self-improving AI agent" with "a built-in learning loop. It creates its own skills from experience instead of you telling the AI like claw code to make skills" [00:14]-[00:20]. Everything runs locally (CLI, Docker, SSH, or a VPS [01:51]) and everything learned is persisted on your machine rather than the cloud [10:14].

The mechanics follow the standard harness pattern Sean has diagrammed before: user prompt, chat history, and system prompt flow into working memory, the LLM agent runs a loop engine calling tools, and an end-loop guardrail terminates the loop and sends a reply [02:30]-[02:50]. The system prompt is a local `soul.md` file, which Sean edits to make Hermes talk like Pikachu [03:01]. The tool set includes terminal, browser, delegate task (spawning sub-agents, including ones that call the Claude CLI headless to write code [05:04]-[05:12]), cron jobs [05:16], skill management, and MCP connections [06:12].

What makes Hermes special is the self-improving memory loop. During an agent run it writes its own `skill.md` (procedural memory: how the agent acts) and `memory.md` (semantic memory: durable user facts) [09:57]. When the browser hit the wrong YouTube URL, Hermes saved a memory about the scraping quirk — "because it realized that it had a mistake, so it updated itself with a memory" [08:43]. Episodic memory lives in a local `state.db` [12:11], and over time cheaper auxiliary models consolidate chat history into semantic facts [12:30]. Notably, retrieval is plain text with top-K keyword matching rather than embeddings or a RAG system [11:20].

The live demos cover cron-scheduled Pokémon jokes [05:24], terminal use to check OS version and shell history [06:29], browser-based YouTube title generation [07:41], explicit memory saves ("my favorite testing framework is pytest" [13:01]), explicit skill creation [13:53], parallel sub-agents via delegate task [14:32], and the Claude CLI writing a Hacker News fetcher [15:02]. The one gap: Hermes has no eval or LLM ops layer, only trajectory export and logs [18:16]. Sean's verdict is that while most of it matches Claude Code or Open Claw, the local self-updating memory is the lock-in: "the user kind of just over time get locked in. And it remembers who I am" [20:24].

## Key moments

- **[00:10]** Hermes has more than 200,000 GitHub stars
- **[00:14]** It is a self-improving agent from the Neural Research lab
- **[00:20]** It creates its own skills from experience, unlike Claude Code
- **[00:40]** Pikachu-personality demo enabled by editing `soul.md`
- **[00:53]** WhatsApp works as an alternative gateway to the desktop app
- **[01:51]** It runs locally via CLI, Docker, SSH, or a VPS
- **[02:30]** Prompt, chat history, and system prompt are fed into working memory
- **[03:01]** The system prompt file is called `soul.md`
- **[03:54]** Harness metaphor: tools that control the powerful LLM "horse"
- **[04:53]** Tools include terminal, browser, delegate task, cron job, skill management, and MCPs
- **[05:24]** Cron-job demo: a Pokémon joke every minute for 10 minutes
- **[06:29]** Terminal demo: OS version and last 10 shell-history lines
- **[07:41]** Browser demo: scrape the channel and generate new video titles
- **[08:21]** After a wrong URL, Hermes self-saves a memory about the scraping quirk
- **[09:19]** An end-loop guardrail stops tool calls and sends the answer
- **[11:20]** Retrieval uses plain text and top-K keyword matching, not embeddings
- **[12:22]** Episodic memory lives in `state.db` and is consolidated by cheaper auxiliary models
- **[13:01]** Explicit memory save: favorite testing framework is pytest
- **[13:53]** Explicit skill creation: the "video prep" skill with style rules
- **[14:32]** Delegate task spawns two sub-agents working in parallel
- **[15:02]** A sub-agent runs the Claude CLI headless to build a Hacker News script
- **[16:50]** Self-saved skills should trigger after difficult tasks with 5+ tool calls
- **[18:16]** No eval or LLM ops system: only logs and trajectory export
- **[20:14]** Accumulated skills and memories are the lock-in value

## Concepts covered

- hermes-agent
- agent-harness
- loop-engineering
- memory-system
- self-improving-ai
- procedural-memory
