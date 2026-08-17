---
type: concept
title: "AI Agent Harness"
description: "The wrapper of memory, tools, and rules that steers a powerful LLM, like a rider controlling a horse."
tags: [ai-agents, harness, system-design]
sources: [raw/you-can-learn-ai-agent-harness-loop-engineering.md, raw/you-can-learn-hermes-agent-harness.md, raw/you-can-learn-ai-agent-harness-in-real-code.md, raw/you-can-learn-pi-minimal-coding-agent-harness.md]
timestamp: 2026-08-17T17:00:00Z
---

# AI Agent Harness

Sean's go-to way to explain an agent harness is the horse metaphor: "Imagine this large language model is a horse, right? This horse is very powerful, they can run around, but if you don't have a good set of tools to ride this horse, you could just get hurt, you might go anywhere, you might go somewhere random" [03:48-03:59]. A harness is therefore "a set of tools that allows you to control over this really powerful horse, which is the LLM itself" [03:54-04:02]. Control matters because an LLM "is actually predicting the probability of the next word that it should spit out. When everything comes with probability, there's randomness in it" [04:37-04:46]. At the same time, Sean insists the term is not deep: "Harness is a very vague concept. Just don't fantasize it. It's nothing complicated. It's just a buzzword" [04:23-04:28].

Why a harness is needed: "a large language model can't do these things by itself. It's like a really powerful brain that knows everything about humanity... But, it does not know you" [03:15-03:27]. The harness's core job is context preparation: it takes the user prompt, chat history, and system prompt, then augments them with three memory types - procedural memory (skills, "how the agent should act"), semantic memory (durable facts like who Sean is), and episodic memory (dated events and past chats) - before feeding the result into the LLM as working memory [01:56-02:41]. In the Waku walkthrough he puts it in one line: "all the agents trying to do is how do we prepare the right memory" [18:44-18:51]. Concretely, Pi merges its `agents.md` behavior file with a system prompt "combined into a JSON file, which is forkable" [07:20-07:28], while Hermes and Waku expose the system prompt as an editable `soul.md` file [03:01-03:06].

A complete harness has more than memory. Sean's frame is four pillars: "harness, loop, memory, eval and LM ops" [00:11-00:16]. Around the LLM sit a gateway (the entry point - Telegram, WhatsApp, desktop chat, or voice [19:11-19:13]), a loop engine that decides tool calls until the task is done, a tool layer, and an LLM Ops sidecar that traces, evaluates, and ships fixes back into the system. Ready-made tooling exists: "you could try tools like LangGraph, LangChain, or Pydantic" [04:54-05:00], or study an open-source reference implementation like Waku-Agent, which walks through gateway, memory, loop, eval, and tracing in real code [05:34-05:46].

Harness designs range from minimal to maximal, and Sean contrasts the two extremes. Pi Agent claims "no MCPs, no sub agents, and no plan mode, no to-do's, no permission pop-ups" [00:08-00:13], exposing only four actions: read, write, edit, and bash [09:04-09:12]. Claude Code is the opposite: "a closed source coding agent harness" that has "plugged in a ton of MCPs, sub-agents" and asks for permissions constantly [13:44-14:07]. Pi's argument is context economics: "sometimes one MCP can add tens of thousands of hundreds of thousands of contexts into your 1 million token context window. And most of the time you probably won't even use it" [14:09-14:22]. Instead of wiring every integration by default, Pi "will let you decide" through user-written skills, extensions, and packages [14:44-14:59].

Harnesses are also building blocks for bigger systems. Because Pi can be invoked as a CLI, another harness can spawn it as a sub-agent - Sean demonstrates Waku-Agent's `delegate task` tool spinning up Pi to write code - "you can literally just plug in into any of these harness systems you build yourself" [02:09-02:14]. He even suspects "this is how Open Claw did the coding for themselves" [01:26-01:34]. Whether minimal (Pi) or feature-rich (Claude Code, Hermes, OpenClaw), the harness is the same idea: structure and constraint around an LLM so it runs "in the right direction... to do the right task" [19:20-19:25].

## Part of / Related

- [Loop Engineering](../concepts/loop-engineering.md)
- [Agent Graph Engineering](../concepts/agent-graph-engineering.md)
- [LLM Ops](../concepts/llm-ops.md)
- [Agent Memory System](../concepts/agent-memory-system.md)
- [Hermes Agent](../entities/hermes-agent.md)

## Sources

- [you-can-learn-ai-agent-harness-in-real-code](/sources/you-can-learn-ai-agent-harness-in-real-code.md)
- [you-can-learn-ai-agent-harness-loop-engineering](/sources/you-can-learn-ai-agent-harness-loop-engineering.md)
- [you-can-learn-hermes-agent-harness](/sources/you-can-learn-hermes-agent-harness.md)
- [you-can-learn-pi-minimal-coding-agent-harness](/sources/you-can-learn-pi-minimal-coding-agent-harness.md)
