---
type: entity
title: "Hermes Agent"
description: "A local-first, self-improving AI agent harness with a built-in learning loop that writes its own skills and memories."
tags: [hermes, harness, memory, self-improving]
sources: [raw/you-can-learn-hermes-agent-harness.md, raw/you-can-learn-ai-agent-harness-in-real-code.md]
timestamp: 2026-08-17T17:00:00Z
---

# Hermes Agent

Hermes is "one of the most popular harness agent system right now... an open source project... more than 200,000 stars" [00:05-00:13], built by Neural Research as "a self-improving AI agent... it's a built-in learning loop. It creates its own skills from experience instead of you telling the AI" [00:14-00:24]. It runs entirely on your machine ("you can use either local command lines, Docker, SSH, or a virtual VPS") with two interaction modes: communication apps like WhatsApp, or the desktop app [01:51-02:25]. Functionally "it's still a chatbot, just like Clawcode" [02:21-02:22], and its system prompt is an editable local file with a memorable name: "The system prompt for Hermes is interesting. It's called soul.md. I really like how they name it. It says soul" [03:00-03:06] - Sean rewrote his to make Hermes talk like Pikachu ("Every reply starts and with pika pika pika p" [03:29-03:34]).

Loop engineering is where Hermes shows its tool surface: "the terminal, the browser... It can delegate task, which means that it can spawn up some sub agents for you" (including one that calls "your claw code CLI to write code for you"), "It can schedule cron job... It can do skill management as well. It can connect to MCPs as well" [04:53-06:15]. Sean's demos exercise each: a terminal call reading his OS version and shell history [06:29-07:06]; a browser run researching his YouTube channel where a wrong URL hit "an end loop guardrail. The guardrail stopped and said, 'It didn't find anything'", then after retry "a mechanism that says, 'Okay, end the loop, no more tool calls, and send the answer'" [09:15-09:40]; a cron job that delivered Pokémon and developer jokes to WhatsApp (with a bug - "your Chrome job is not updating it unless I ask for the results" [17:03-17:20]); `delegate task` spawning two parallel research sub-agents on LLM eval harnesses and VLM architecture [14:30-14:57]; and a sub-agent driving Claude CLI in headless mode to build a Hacker News fetcher [15:02-16:03].

The memory system is Hermes's signature. Procedural memory is "basically how you act" and lives as `skill.md` files under the Hermes skills directory (e.g. a skill for how Hermes should "delegate any coding to claw code CLI" [10:37-11:05]); semantic memory is `memory.md`, "some durable facts or things related to the user profile" [11:08-11:18]; episodic memory is chat history in a local `state.db` [12:08-12:26]. Retrieval is deliberately simple: "instead of doing the embeddings, it's actually just using plain text... It's using top top K keyword instead of doing the embedding or the rack system" [11:22-11:30]. The system also consolidates itself: "it will start to consolidate some of those chats using the Hermes auxiliary models, which are cheaper, non-important models to do this summarization task so that it will distill some facts into... semantic memory" [12:29-12:42].

What makes Hermes special, per Sean, is the self-improving loop. When a YouTube scraping attempt hit a wrong URL, "it realized that it had a mistake, so it updated itself with a memory. This is a self-iterating process of this harness" [08:43-08:48]. The general rule: "Every time when it realized that something is a mistake that it should learn from or it's a repeated task, it will start to summarize... in order to serve this user well" [10:19-10:32]. The demo had limits - asked whether it saved any skills by itself, it admitted "You did not self- realize you need to save skill. It should proactively offer to save a skill after difficult iterative task with five or more tool calls" [16:43-16:52] - and LLM Ops is missing: "I don't think it has an LLM ops or an eval system... it does trace the run... trajectory export and logs... but there's no eval" [18:25-18:41]. Sean's verdict: "what makes Hermes special, at least compared to Clawcode, is that it's self-updating all these things locally" [19:26-19:30], and that accumulation is the moat - "the skill and memory accumulation is probably the most valuable thing in this, because the user kind of just over time get locked in" [20:18-20:27].

## Part of / Related

- [Loop Engineering](../concepts/loop-engineering.md)
- [AI Agent Harness](../concepts/ai-agent-harness.md)
- [Agent Memory System](../concepts/agent-memory-system.md)
- [Waku Agent](../entities/waku-agent.md)
- [Pi Coding Agent](../entities/pi-coding-agent.md)

## Sources

- [you-can-learn-ai-agent-harness-in-real-code](/sources/you-can-learn-ai-agent-harness-in-real-code.md)
- [you-can-learn-hermes-agent-harness](/sources/you-can-learn-hermes-agent-harness.md)
