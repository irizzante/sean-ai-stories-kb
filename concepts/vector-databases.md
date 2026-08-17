---
type: concept
title: "Vector Databases and Retrieval for Agent Memory"
description: "Embedding-based stores and top-K RAG retrieval compared against SQLite FTS5 keyword search in the Waku memory arena."
tags: [vector-databases, rag, agent-memory]
sources: [raw/you-can-learn-ai-agent-memory-system.md, raw/you-can-learn-ai-agent-memory-layers.md]
timestamp: 2026-08-17T17:00:00Z
---

# Vector Databases and Retrieval for Agent Memory

Vector stores exist because "computers cannot process on words. They can only process numbers or higher dimensions of numbers" [13:43]. A vector store "usually store[s] information in vectors... embed[s] every single word into a high-dimensional vector" [13:31], so semantic memory and episodic memory are "actually saved not in files but we would call vector stores" [04:32]. Retrieval is similarity search: ask about "food" and the system "calculate[s] what other words that are embedded in the same dimensions in our database have a high similarity to food. Maybe it's going to be apple, maybe it's going to be sausages" [06:38]. This is semantic search rather than literal keyword matching. Common products Sean names are Weaviate and Pinecone, plus Supabase, which "is a relational database... but they do have a SQLite extension called PG Vector" that stores rows with vector columns [13:13].

The retrieval pattern on top of a vector store is RAG - retrieval augmented generation - using a "top case search method" [05:31]: "if K is five, then it's looking for the top five most relevant pieces of information from the vector store to feed into answering this question" [07:25]. Selective fetching matters because a ten-year-old company's database could be gigantic, and feeding everything to the LLM "would be very expensive, and secondly, that's probably not feasible" [06:03]. Even with context windows around one million tokens, "you don't want to overload your LLMs because that also makes things much slower and not accurate anymore" [06:15]. In Sean's memory-system design, RAG fetches the static, durable facts of the semantic memory, while episodic memory - the dated event log - is also stored as vectors and updated continuously [08:30]. Maintenance is by upsert or delete, optionally wrapped in a consolidation module like the one used for state.db [14:20].

The Waku agent's "memory rays" arena seeded the same dinner-party facts - Jensen Huang knocking chili oil onto a rug, Elon Musk moving his arrival from 7:00 to 9:00 p.m., Tom Holland revealing a film ending, Paul Graham owing 20 quid from a Lisbon bakery - into SQLite, Mem0, LangMem, Zap, and a memory-less control, then asked identical questions [18:43]. SQLite keyword search was fastest at 4.6 seconds and correct [23:50], but stumbled when the question came in Chinese while the memory was in English, taking 10.3 seconds: "maybe because SQLite is a little bit too simple for keyword searching, so it doesn't really know how to search in Chinese" [24:31]. Mem0, which stores both raw and graph memories as vectors, answered correctly and replied in Chinese [24:39]. LangMem was slowest at 7.5 seconds [24:08] - it is not a store at all but "a package that allows you to store locally... your own stores search... and you're extracting and resolving the store update before writing into anything" [17:28].

The control group proved the memories do the work, correctly reporting no information about Jensen or Elon [24:15]. The same question set also exercised superseding: the Elon arrival update from 7:00 to 9:00 p.m. should "keep the previous information but make it, you know, kind of outdated" [25:25], and all three stores answered the updated time correctly [25:32]. The takeaways on trade-offs: keyword search is fast and simple for same-language durable facts but weak on semantic or cross-language queries; vector search generalizes across languages and paraphrase at the cost of embedding infrastructure; and graph-backed memory adds relationship context at a heavy latency cost. The arena deliberately excluded Supabase because "we're not testing embeddings here" [20:04] - the embeddings-versus-graph comparison is left to the RAG and Graph RAG layers.

## Part of / Related

- [AI Agent Memory System](/concepts/agent-memory-system.md)
- [Graph RAG](/concepts/graph-rag.md)
- [Waku Agent](/entities/waku-agent.md)
- [Hermes Agent](/entities/hermes-agent.md)

## Sources

- [you-can-learn-ai-agent-memory-layers](/sources/you-can-learn-ai-agent-memory-layers.md)
- [you-can-learn-ai-agent-memory-system](/sources/you-can-learn-ai-agent-memory-system.md)
