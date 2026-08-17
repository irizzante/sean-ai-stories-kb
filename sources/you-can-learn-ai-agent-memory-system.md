---
type: Source
title: "You Can Learn AI Agent Memory System In 12 Min | Semantic & Episodic Memory, RAG, Vector Database"
description: "A step-by-step system design of AI agent memory: working memory fed by procedural, semantic, and episodic memory, with RAG top-K retrieval and gated periodic consolidation into durable facts."
youtube_id: mY3bR9qjZr4
resource: https://www.youtube.com/watch?v=mY3bR9qjZr4
published: 2026-06-19
tags: [ai-agents, agent-memory, rag, vector-databases]
sources: [raw/you-can-learn-ai-agent-memory-system.md]
timestamp: 2026-08-17T16:00:00Z
---

# You Can Learn AI Agent Memory System In 12 Min | Semantic & Episodic Memory, RAG, Vector Database

The video walks through a complete memory system design for an AI agent, starting from what happens on a single chat turn: the user prompt flows into a working memory, "a context RAM", that is also fed with the current chat history and a system prompt, and only then does the Q&A agent produce a reply [01:15]. Working memory is needed because the model may not know "what does my company do" on its own; the context has to be assembled from the internet, the current conversation, or databases where information was stored previously [01:20]. Critically, an AI agent session is ephemeral - "nothing here will get saved unless you manually save them in a database" [02:55] - so a persistent system must be built around three pillars: procedural memory (how the agent should behave, expressed as skills in markdown files), semantic memory (durable facts and user profiles in a vector store), and episodic memory (dated events and past conversations in a vector store) [03:30].

Semantic memory stores the durable facts - what products you sell, your branding, who a frequent customer is - because "the foundational large language model does not know who you are" [05:09]. These are fetched through RAG, retrieval augmented generation, which selectively pulls the most relevant information with a top-K similarity search over vectors [05:28]. Selective fetching matters because feeding a decade of company data into the model would be very expensive and probably infeasible; "the context window for most LLMs is roughly 1 million tokens" [06:11]. Episodic memory is different: it records dated events like a timeline - who purchased what on which day, when an item was delivered, when a complaint was filed - and it is constantly updated by saving every conversation and activity into it [07:44].

The most important design trick is consolidation: ChatGPT and Claude keep their memories short but constantly updated because a summarizer agent periodically condenses episodic activity into durable semantic facts, which "not only saved a lot of token usage every single time, and also it's making your tools much faster" [09:58]. Without a gate you would simply save everything twice, so the system only consolidates "after a certain number of chats" - maybe 20 conversations or 100 activities - and feeds the accumulated episodes to a summarizer agent that distills them into facts [10:19]. The result is a modern agent architecture where memory is a context layer on top of every interaction, with skills defining behavior, semantic memory holding core durable facts, and episodic memory acting as the timeline log [11:50].

## Key moments

- **[00:07]** Users of ChatGPT and Claude are already using a memory system without realizing it
- **[00:46]** Every chat starts with a user prompt sent to the Q&A agent
- **[01:13]** The prompt first flows into a working memory, a context RAM
- **[01:39]** Current chat history and the system prompt are fed into working memory
- **[02:55]** An AI agent session is ephemeral: nothing persists unless saved to a database
- **[03:30]** Three pillars complete the working memory: procedural, semantic, and episodic memory
- **[03:39]** Procedural memory is skills - habits the agent should follow, saved as markdown
- **[04:45]** Semantic memory holds durable facts and user profiles in a vector store
- **[05:28]** RAG does top-K similarity search to fetch only the most relevant information
- **[06:11]** LLM context windows are roughly 1 million tokens, so selective fetching is essential
- **[06:58]** Episodic memory records dated events and activities like a timeline
- **[08:35]** Episodic memory is constantly updated, acting as a log of all previous history
- **[08:48]** ChatGPT and Claude memories are short but constantly updated through pivots and conversations
- **[09:36]** A summarizer condenses episodic activity into semantic memory at a not-too-frequent cadence
- **[10:19]** A gate triggers consolidation only after a set number of chats to avoid double-saving
- **[11:50]** The finished system adds memory as a context layer on top of the entire interaction

## Concepts covered

- agent-memory-system
- working-memory
- procedural-memory
- semantic-memory
- episodic-memory
- rag
