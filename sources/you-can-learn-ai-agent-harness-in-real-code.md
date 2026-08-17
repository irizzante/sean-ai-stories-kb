---
type: Source
title: "You Can Learn AI Agent Harness In Real Code In 20 Min | Loop Engineering, Memory, Eval, Open Source"
description: "A real-code walkthrough of Waku-Agent, a local open-source personal assistant implementing harness, loop, memory, eval, and LLM ops."
youtube_id: rvRyBhILrls
resource: https://www.youtube.com/watch?v=rvRyBhILrls
published: 2026-07-14
tags: [agent-harness, loop-engineering, memory-system, agent-evaluation]
sources: [raw/you-can-learn-ai-agent-harness-in-real-code.md]
timestamp: 2026-08-17T16:00:00Z
---

# You Can Learn AI Agent Harness In Real Code In 20 Min | Loop Engineering, Memory, Eval, Open Source

This video is the implementation companion to Sean's earlier system-design videos: he walks through Waku-Agent, an open-source local assistant he built to cover "the entire four pillars that matters to an agent system today, which is harness, loop, memory, eval and LLM ops" [00:07]. The opening demo sets the template for everything that follows: asked to find the remaining World Cup games and add them to a calendar, the agent checks its retrieval gate, decides no memory retrieval is needed [00:41], runs the loop engine with tools like web search [00:46], asks for calendar permission [01:22], and produces a trace of the whole run with token usage and cost [03:13].

The memory system is the heart of the design, split into three stores. Semantic memory holds durable facts, such as "Sergey is a close friend who loves swimming and often cooks delicious food" [02:24], kept in a local `memory.md` [07:30]. Procedural memory is the skills folder: markdown instructions for how the agent should act, like the `schedule meeting` skill that resolves relative dates, checks attendees, and calls the create-event tool [10:22]. Episodic memory stores dated events like the World Cup bookings [17:18], and a consolidation task continuously distills durable facts from episodic history into semantic memory [17:28]. The system prompt itself is an editable `soul.md` file, and Sean demonstrates changing the agent's personality to say "muchas gracias" and watching the file update in real time [06:38].

Eval and LLM ops round out the pillars. The `eval` folder contains deterministic rule-based checks — for example, whether the Apple Calendar tool works — and a `judge` folder where an LLM (Anthropic) scores qualitative questions about response quality [08:49]-[09:46]. Every run is traced locally with tools used, tokens in/out, and timing [08:00]; Sean contrasts this with cloud tools like LangFuse or LangGraph and notes you could connect those instead [08:22]. The agent loop itself is capped at 10 iterations by default [16:40].

The code walkthrough covers the gateway (Telegram via BotFather, plus a voice mode activated by the wake word "Waku Waku" [14:26]-[14:50]), the `Class Waku` main app that composes model, system prompt, messages, tools, iterations, and streaming [18:14], and tools like Apple Calendar and Tavily web search [17:54]. Sean closes by recapping the full flow: request through gateway, retrieval gate, procedural/semantic/episodic memory, tool-calling loop, tracing with eval, and post-reply consolidation of facts [18:41].

## Key moments

- **[00:07]** Four pillars: harness, loop, memory, eval, and LLM ops
- **[00:35]** Demo: find World Cup games and add them all to the calendar
- **[00:41]** The retrieval gate decides no memory retrieval is needed
- **[01:22]** The agent asks permission before accessing the calendar
- **[02:12]** "Who is Sergey?" triggers retrieval and a semantic memory hit
- **[02:24]** Semantic memory holds durable facts like friends' traits
- **[03:13]** The trace tab shows tokens, cost, and LLM calls per run
- **[03:48]** A Telegram bot is set up through BotFather as a second gateway
- **[04:37]** Saying "remember that Vincent and I went to Paris" calls the save-note tool
- **[06:38]** `soul.md` is the editable local system prompt
- **[08:00]** Traces record tools used, results, and token usage with timestamps
- **[08:49]** The eval folder splits into deterministic rules and an LLM judge
- **[09:46]** Anthropic is configured as the judge model
- **[10:32]** Skills are procedural memory: instructions for how the agent acts
- **[11:10]** Editing the schedule-meeting skill adds a heart emoji to new events
- **[12:16]** A new skill is created by adding a folder and `skill.md` for YouTube title writing
- **[14:50]** Voice mode activates on the wake word "Waku Waku"
- **[16:40]** The loop defaults to a maximum of 10 iterations
- **[17:28]** A consolidation task distills episodic history into semantic memory
- **[18:14]** The main app is `Class Waku`, a Q&A agent composing model, prompt, tools, and observers

## Concepts covered

- [agent-harness](/concepts/ai-agent-harness.md)
- [loop-engineering](/concepts/loop-engineering.md)
- [memory-system](/concepts/agent-memory-system.md)
- [procedural-memory](/concepts/agent-memory-system.md)
- [semantic-memory](/concepts/agent-memory-system.md)
- [episodic-memory](/concepts/agent-memory-system.md)