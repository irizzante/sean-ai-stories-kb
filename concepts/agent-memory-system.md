---
type: concept
title: "AI Agent Memory System"
description: "Working memory fed by procedural, semantic, and episodic stores, with gated consolidation and a decide/retire/attribute/reflect maintenance loop."
tags: [ai-agents, agent-memory, architecture]
sources: [raw/you-can-learn-ai-agent-memory-layers.md, raw/you-can-learn-ai-agent-memory-system.md, raw/ai-memory-system-for-service-agencies.md]
timestamp: 2026-08-17T17:00:00Z
---

# AI Agent Memory System

An AI agent memory system exists because "any LLM call does not carry any weight for long terms" [00:05]; the reason ChatGPT and Claude Code remember past conversations is that their makers "already crafted this memory system for their own AI agent harness" [00:14]. Sean Chen's architecture, implemented in his open-source Waku agent and compared against Hermes, treats the agent run as a loop that prepares a working memory "with retrieving from three main pillars, which is procedural memories... a skill, semantic memory, which is some durable facts, and episodic memory, which is some dated events" [00:38]. That working memory - a "context RAM" - is fed by the user prompt, the current chat history, and the system prompt before the LLM replies [01:13]. On its own, a session is ephemeral: "nothing here will get saved unless you manually save them in a database" [02:57].

The three pillars divide cleanly by role. Procedural memory is how the agent should behave - skills written as markdown, loaded by trigger, like a rule that "if you realize that the customer is really angry, you should answer them politely and always apologize" [03:52]. Semantic memory holds durable facts and user profiles - who the company is, what it sells - retrieved by RAG top-K search [05:26]. Episodic memory is "the dated events or activities that happened... like a timeline" [07:40]: past chat histories, purchases, complaints, each stamped with a time. The key design move is consolidation: Waku saves every conversation into a SQLite state.db, then "consolidate[s] the information after every, you know, say five or 10 conversations using some cheaper auxiliary models" and distills facts into the memory.md [11:19]. This keeps semantic memory short and updated while the episodic log keeps everything, because "you don't want the AI agent to always search these kind of information from an episodic memory because that's just a huge database" [09:17]. It "not only saved a lot of token usage every single time, and also it's making your tools much faster" [09:58].

Consolidation is gated to avoid double-storing everything: "we only consolidate after a certain number of chats. It could be 20 conversations, it could be, you know, 100 activities" [10:19], after which a summarizer agent distills the batch - "we call this the steel into facts" [10:50]. Without this gate "the database is just exploding" [11:15]. Maintenance is the second half of the system, summarized in four operations: decide (add, delete, overwrite, or do nothing) [07:32]; retire - invalidating a fact with a time range rather than deleting it, as when Waku's star count goes from 1,000 in 25 days to 1.3k on day 26 while "these contexts are still important for future tracing purposes" [07:48]; attribute - "tracing where the source comes from... maybe I got the memory from the users communicating with your agent or maybe I got it from some web search" [08:39]; and reflect - dropping or merging duplicates and outdated information in a background "postmortem" pass, "similar to what Anthropic has proposed, which is dreaming. Dreaming happens when we are not working" [09:00].

How the agent finds memories is a separate decision from where they are stored: do nothing (a short memory.md "is supposed to be read by default... so that it's always in the context" [05:14]); SQLite FTS5 keyword search on state.db [05:47]; RAG similarity search over embeddings [06:20]; or Graph RAG, which embeds nodes and edges so results "might return a relationship graph here, so that the agent has more context about the memories in relationships" [07:16]. A retrieval gate can decide which skills and semantic memories to load per turn, though "whether or not we should have retrieval gate, that's completely up to you" [12:29]. Chen's core claim is that the harness is replaceable but the memory is not: "What matters most to you eventually is the memories... these memories are the most valuable assets for any AI agent harness" [12:18].

## Part of / Related

- [Graph RAG](/concepts/graph-rag.md)
- [Vector Databases](/concepts/vector-databases.md)
- [Business Memory System](/concepts/business-memory-system.md)
- [AI Agent Harness](/concepts/ai-agent-harness.md)
- [Waku Agent](/entities/waku-agent.md)

## Sources

- [ai-memory-system-for-service-agencies](/sources/ai-memory-system-for-service-agencies.md)
- [you-can-learn-ai-agent-memory-layers](/sources/you-can-learn-ai-agent-memory-layers.md)
- [you-can-learn-ai-agent-memory-system](/sources/you-can-learn-ai-agent-memory-system.md)
