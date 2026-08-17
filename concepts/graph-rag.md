---
type: concept
title: "Graph RAG and Temporal Graph Memory"
description: "Graph-structured agent memory that embeds nodes and edges, with temporal graph memory that invalidates facts over time instead of deleting them."
tags: [graph-rag, agent-memory, knowledge-graphs]
sources: [raw/you-can-learn-ai-agent-memory-layers.md, raw/you-can-learn-ai-agent-memory-system.md]
timestamp: 2026-08-17T17:00:00Z
---

# Graph RAG and Temporal Graph Memory

Graphs are the third way to store agent memories, alongside plain text and tables: "it's basically a way to build up connections between information" [03:49]. In Zap's relational graph, a founder Alex connects to a Lisbon AI meetup event, to his robotics startup, and to product launch dates in May and June, so the agent can traverse relationships instead of matching isolated records [04:06]. Graph RAG builds retrieval on top of this: "it's still embedding the information, but it embeds things like the nodes... And it also embed[s] that edge, like is it a part of the observation or is it a relationship" [07:00]. When a user asks a question, similarity search runs over both nodes and edges, and "it might return a relationship graph here, so that the agent has more context about the memories in relationships" [07:23] - which is what distinguishes it from plain RAG, where only standalone chunks or words are embedded.

Zap's product adds a time dimension with what it calls temporal graph memory: "this graph is evolving over time. It's got the nodes, got the edges, it's got the validity" [16:39]. The claim is that retrieval is vector search across nodes, edges, and full-graph traversal [16:51], and that old facts are handled by invalidation rather than deletion: "it can invalidate with some time range like superseding. Like similar to superseding you never delete it but the history survives here" [17:01]. This mirrors the retire operation in Chen's maintenance loop, where a fact like "1,000 stars in 25 days" stays traceable after the count becomes 1.3k [08:05]. The live demo showed the graph actually reasoning over edges: for Tom Holland, "this edge is saying revealed ending of. So Tom Holland revealed the ending of his next movie. So it did some summarization for me" [28:20].

In practice, Chen's memory arena found the trade-offs stark. Graph RAG beat keyword retrieval in the cross-language case where "SQLite is a little bit too simple for keyword searching, so it doesn't really know how to search in Chinese" while Mem0 answered correctly in Chinese [24:33] - but Zap was dramatically slower, still seeding while every other store had finished: "maybe saving data using temporal graph is a pain because it's being delayed for so long" [27:06]. Querying took so long that Chen lost patience and addressed the team directly: "Zep team, if you're watching this, I think this is a big pain point. Love the product, love the visualization, but please fix speed" [29:51]. The graph also dropped attribution, showing that chili oil stained the rug "but it didn't say Elon... I feel like it lost some information here" [28:48].

The verdict is that graph memory is a scaling choice, not a default: "Maybe it's an overkill for a lot of these smaller use cases, which is why I think that Hermes and Pi agent... make things very simple" [29:07]. Hermes and Waku deliberately use plain text and keyword search instead of embeddings or graphs [01:10], and graph memory in Mem0 is gated behind a paid tier while its raw memory is open [16:20]. The lesson is to pick the layer that matches the workload: keyword for simple durable facts, vectors for semantic search, and graphs when relationships themselves carry meaning - but only if you can tolerate the seeding and traversal latency. For maintenance, a graph needs the same discipline as any store: add, update, delete, noop - and ideally supersede - while periodically traversing to merge duplicates and outdated nodes [16:12].

## Part of / Related

- [AI Agent Memory System](/concepts/agent-memory-system.md)
- [Vector Databases](/concepts/vector-databases.md)
- [Agent Graph Engineering](/concepts/agent-graph-engineering.md)
- [Waku Agent](/entities/waku-agent.md)
- [Hermes Agent](/entities/hermes-agent.md)

## Sources

- [you-can-learn-ai-agent-memory-layers](/sources/you-can-learn-ai-agent-memory-layers.md)
- [you-can-learn-ai-agent-memory-system](/sources/you-can-learn-ai-agent-memory-system.md)
