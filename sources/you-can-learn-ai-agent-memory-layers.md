---
type: Source
title: "You Can Learn AI Agent Memory Layers | Graph RAG, Vector DB, SQLite, Hermes, Waku"
description: "How to architect AI agent memory: three storage styles (text, tables, graphs), four retrieval approaches (always-on, keyword, RAG, Graph RAG), and four maintenance operations, tested live across SQLite, Mem0, LangMem, and Zap."
youtube_id: 072eNztI06k
resource: https://www.youtube.com/watch?v=072eNztI06k
published: 2026-08-16
tags: [ai-agents, agent-memory, graph-rag, vector-databases]
sources: [raw/you-can-learn-ai-agent-memory-layers.md]
timestamp: 2026-08-17T16:00:00Z
---

# You Can Learn AI Agent Memory Layers | Graph RAG, Vector DB, SQLite, Hermes, Waku

Any LLM call by itself carries no long-term memory: "[00:05] any LLM call does not carry any weight for long terms", and the reason ChatGPT and Claude Code remember past conversations is that their makers have already "crafted this memory system for their own AI agent harness" [00:14]. The video surveys five ways to architect agent memory around a harness like the author's open-source Waku agent, using three organizing questions: what is the memory, how does the agent find it, and how is it maintained [02:37]. Storage options are plain text or markdown (Hermes' memory.md, Waku's soul.md system prompt), tables like SQLite or Google Sheets, and graphs with nodes and edges such as the Zap relational graph [02:44]. Vector embeddings are not a separate storage category but live inside one of these - with Supabase pgvector, for instance, the data "is going to be still in rows in the table" with vector columns [04:46].

Retrieval also has layers: doing nothing, because a short memory.md is read by default and always in context [05:07]; keyword search via SQLite FTS5, as used on the Hermes state.db [05:47]; RAG semantic search, where a word like "food" is embedded into a high-dimensional vector and compared for similarity against stored vectors [06:20]; and Graph RAG, which embeds both nodes and edges so the similarity search "might return a relationship graph" and give "the agent has more context about the memories in relationships" [07:23]. Maintenance is the most underrated pillar: decide whether to add, delete, overwrite, or do nothing [07:32]; retire or invalidate with a time range rather than delete - the Waku agent example where 1,000 stars in 25 days is superseded by 1.3k stars on day 26 while the old fact stays traceable [07:48]; attribute, tracing where a memory came from [08:39]; and reflect, a background "postmortem" pass that drops or merges duplicates, similar to what Anthropic calls dreaming, scheduled when the agent is not running [09:14].

The second half stress-tests real memory layers through the Waku agent's "memory rays" arena, which seeds a dinner-party fact set - Jensen Huang spilling chili oil on a rug, Elon Musk shifting his arrival from 7:00 to 9:00 p.m., Tom Holland revealing a film ending, Paul Graham owing 20 quid - into SQLite, Mem0, LangMem, Zap, and a memory-less control, then asks the same questions of all five [18:39]. SQLite answered in 4.6 seconds and was the fastest correct responder [23:50]; Mem0 answered correctly and even replied in Chinese to a question asked in Chinese, while SQLite's keyword search struggled across languages at 10.3 seconds [24:39]; LangMem was slowest at 7.5 seconds [24:08]; Zap's temporal graph was so slow to seed and query that the demo nearly gives up, though its graph visualization did surface an edge summarizing "revealed ending of" [28:20] while also losing the attribution that Elon spilled the chili oil [28:51]. The control group correctly had no answers, proving the memories do the work [24:15]. The verdict: graph memory may be "an overkill for a lot of these smaller use cases" [29:07], while the memories themselves are "the most valuable assets for any AI agent harness" [12:24].

## Key moments

- **[00:05]** LLM calls carry no long-term weight, which is why every serious agent needs a memory system
- **[00:19]** The video covers five ways of architecting agent memory around a harness
- **[02:37]** Three pillars frame the whole design: what is it, how to find it, how to maintain it
- **[02:44]** Three storage styles: text/markdown files, tables, and graphs of nodes and edges
- **[04:46]** Embeddings still live in rows with Supabase pgvector, or in NoSQL stores
- **[05:07]** Retrieval option one is doing nothing: short memory files are always in context
- **[05:47]** Keyword search comes from SQLite FTS5 on the Hermes state.db
- **[06:20]** RAG embeds words into high-dimensional vectors and does semantic similarity search
- **[06:55]** Graph RAG embeds nodes and edges and returns a relationship graph
- **[07:32]** Four maintenance operations: decide (add/delete/overwrite/noop), retire, attribute, reflect
- **[07:58]** Superseding keeps the old fact: 1,000 stars in 25 days is invalidated by 1.3k stars on day 26
- **[09:14]** Reflect mirrors Anthropic's "dreaming", scheduled when the agent is not working
- **[13:13]** Market vector stores include Supabase pgvector, Weaviate, and Pinecone
- **[14:37]** Mem0 offers raw (row) memory and graph memory, both vector-stored, with supersede
- **[16:35]** Zap's temporal graph memory evolves over time and never deletes history
- **[18:39]** The memory rays arena seeds dinner-party facts into SQLite, Mem0, LangMem, Zap, and a control
- **[23:50]** SQLite is fastest and correct at 4.6 seconds on the chili oil question
- **[24:39]** Mem0 crosses languages and answers the Chinese question correctly in Chinese
- **[25:00]** Elon's arrival update from 7:00 to 9:00 p.m. tests superseding across all stores
- **[29:07]** Verdict: temporal graphs may be overkill for smaller use cases; simple memory wins

## Concepts covered

- agent-memory-layers
- graph-rag
- vector-databases
- temporal-graph-memory
- memory-maintenance
- sqlite-fts5
