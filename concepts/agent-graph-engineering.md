---
type: concept
title: "Agent Graph Engineering"
description: "Designing predetermined node-and-edge workflows where LLM-powered nodes run in parallel and the model can route between edges."
tags: [ai-agents, graphs, workflows, system-design]
sources: [raw/you-can-learn-ai-agent-graph-engineering.md, raw/you-can-learn-ai-agent-harness-loop-engineering.md]
timestamp: 2026-08-17T17:00:00Z
---

# Agent Graph Engineering

Graph engineering became the agent buzzword of mid-2026 when "Peter Steinberger, who's also the author of this little lobster, which is open claw, said that are we still talking about loops or did we shift to graphs yet? And he posted this on July 18th, 2026... And he got 3 million views" [00:20-00:37]. Sean's read on the virality: "these important people in the space who mention a keyword and then everybody's going to start talking about it" [00:44-00:50]. His job in this video is to demystify the term with a system-design ladder.

The ladder of AI agent engineering, per Sean: prompt engineering came first - "the most accurate word to describe this was role-playing," telling ChatGPT 3.5 "you are the best poet, like you're Shakespeare or Li Bai" [02:24-02:36]. Then context engineering, because real workflows "not only need prompt, but also you need to feed in data" like CRM records [03:06-03:13]. Then skills, "sort of teaching the AI what kind of procedure it should follow... In AI agent harness, this is called procedural memory" [04:02-04:12]. Then loops, where instead of prescribing a procedure you say "agents, go figure it out yourself" [06:53-06:54]. Graphs complete the ladder: "To eventually we realize that, 'Hey, we need a mixture of both.' That, in my opinion, is graph" [06:57-07:01].

A graph is "a procedure that is predetermined" [06:19-06:21]. It applies when a workflow has a known shape: for repeated business processes - "if you're working in e-commerce, maybe you see exactly how your customer service should be answering questions related to logistics, to refund" - "you can really consolidate this into a graph when the workflow stops changing" [07:25-07:41]. Sean acknowledges the criticism that this is "not new because maybe in 2023... people were already using Airflow, people are using step functions" [06:27-06:37]. What is new: "some of the nodes we're using right now are non-deterministic. Could be a LLM call. And at the same time, sometimes the model can pick the edge" - LLM-as-judge routing, plus "some guards, which a previous directional graph scheduling never did" [20:35-21:00].

Nodes are the unit of design. In Waku-Agent's graph engine, "you're going to add nodes, which in our case could be web search tools, could be agent calls, could be MCPs, anything"; node types are explicitly "Tool calls, LLM calls, agent calls, router" [17:16-17:44]. Edges define flow: "you're also defining edges, which is okay... where do we go after using one tool? After the web search, do we go synthesizing or do we go somewhere else?" [17:24-17:29]. A workflow is then a predefined wiring of these nodes: Waku ships `triage` (start, then classify whether agent calls are needed while checking the calendar in parallel) and `gather` (scan GitHub, search the web, check calendar and memories in parallel, then synthesize) [12:44-14:28].

The decisive difference from loops is parallel execution. In a loop, "web search is going to decide what's going to do first... calling tools one by one"; in the gather graph, "it used multiple tools in parallel because we already told it, 'You need these four tools'" - then "it's going to synthesize the information" [15:48-16:35]. But the two are not competitors: "you cannot say graph engineering is replacing loop engineering because they're coexisting... A loop is something you need when the model decides what to call one step at a time. A graph is something like when you know the shape and you just want them to move together" [16:39-16:59]. Workflow routing is also community-facing: contributors can submit graph workflows as `.py` files, and once approved they become available to everyone through commands like `/gather` - "triage is the router. It's basically going to read the local files of these workflows from graphs, and people can use it" [18:55-19:26].

## Part of / Related

- [Loop Engineering](../concepts/loop-engineering.md)
- [AI Agent Harness](../concepts/ai-agent-harness.md)
- [LLM Ops](../concepts/llm-ops.md)
- [Waku Agent](../entities/waku-agent.md)

## Sources

- [you-can-learn-ai-agent-graph-engineering](/sources/you-can-learn-ai-agent-graph-engineering.md)
- [you-can-learn-ai-agent-harness-loop-engineering](/sources/you-can-learn-ai-agent-harness-loop-engineering.md)
