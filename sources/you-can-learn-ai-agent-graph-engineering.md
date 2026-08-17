---
type: Source
title: "You Can Learn AI Agent Graph Engineering In 21 Min | Loop, Harness, System Design, Waku Agent"
description: "Explains the loop versus graph engineering debate by walking the AI agent engineering ladder and demoing graph workflows in the open-source Waku-Agent harness."
youtube_id: IMLwvK08JVc
resource: https://www.youtube.com/watch?v=IMLwvK08JVc
published: 2026-08-01
tags: [agent-graphs, loop-engineering, system-design, waku-agent]
sources: [raw/you-can-learn-ai-agent-graph-engineering.md]
timestamp: 2026-08-17T16:00:00Z
---

# You Can Learn AI Agent Graph Engineering In 21 Min | Loop, Harness, System Design, Waku Agent

This video demystifies the loop-versus-graph debate that went viral after Peter Steinberger's post asking "are we still talking about loops or did we shift to graphs yet?" [00:22]. Sean frames the discussion with an "AI agent engineering ladder" [02:01]: prompt engineering (role-playing an LLM into a persona), context engineering (feeding workflows real data from CRMs, sheets, and APIs), skills (procedural memory that encodes how the agent should behave without repeating instructions), then loops, and finally graphs. A loop is an open-ended iteration where "the model decides what to call one step at a time" toward a goal, while a graph is a predetermined procedure that "is basically saying, 'Okay, I know exactly what you should be checking... Do it the way I want'" [10:44]. His core thesis is that graph is the synthesis of both: skills (strict procedure following) plus loops ("agents, go figure it out yourself") mixed together [06:48].

The practical guidance is about when to use each. You should consolidate workflows into a graph "when the workflow stops changing" [07:39], such as standardized e-commerce customer service SOPs, while loops remain the right tool for exploratory work like deep research [07:52]. From a system design view, loops run tool calls sequentially (the model decides the next call each time), while graphs run predefined nodes in parallel because "we already told it, 'You need these four tools'" [16:16]. He insists the two coexist: "You cannot say graph engineering is replacing loop engineering because they're coexisting" [16:41].

The concrete demonstration is Waku-Agent, an open-source harness (github.com/shenseanchen/waku-agent) with a gateway, retrieval gate for procedural/semantic/episodic memory, an agent loop, and LLM ops. Its graph tab ships two workflows: triage, which in parallel classifies whether complex agent calls are needed while checking the calendar [13:31], and gather, which scans GitHub, the web, calendar, and memory in parallel before synthesizing a morning brief [14:28]. Under the hood, graphs are defined in code as nodes (tool calls, LLM calls, agent calls, routers) and edges that say where to go after each tool [17:06].

He closes by answering "isn't this just a deterministic workflow from 2023?" — the new parts are non-deterministic nodes (LLM calls inside the graph), model-picked edges (routing, where the LLM judges whether a simple or complex model should answer), and guards that older DAG schedulers never had [20:27].

## Key moments

- **[00:01]** Frames the topic as the two biggest buzzwords in AI agents: loop versus graph engineering.
- **[00:22]** Credits Peter Steinberger's viral post asking whether the community has shifted from loops to graphs yet.
- **[02:01]** Introduces the AI agent engineering ladder covering the past three years.
- **[02:13]** Defines prompt engineering as role-playing, where you draft prompts to make the LLM respond a certain way.
- **[02:57]** Explains context engineering as feeding real data (CRM, sheets, APIs) into agent workflows.
- **[03:58]** Defines skills as procedural memory that encodes procedures the agent should follow.
- **[05:23]** Introduces the loop: a goal plus a set of tools the agent iterates over until finished.
- **[06:15]** Asks why graphs are needed and argues graph is a mixture of skills and loops.
- **[07:39]** Advises consolidating workflows into graphs when they stop changing.
- **[07:52]** Cites deep research as an early example of loop engineering.
- **[08:28]** Contrasts loop (discovers what to do next) with graph (standardized, often parallel, process).
- **[11:54]** Walks through the full Waku-Agent harness: gateway, retrieval gate, agent loop, and LLM ops.
- **[12:44]** Shows the graph tab with two predefined workflows: triage and gather.
- **[13:31]** Demonstrates triage classifying agent-call needs while checking the calendar in parallel.
- **[14:12]** Triggers the gather graph with a slash command and receives a morning brief with PRs and research.
- **[15:38]** Compares loop versus graph execution from a time and parallel processing perspective.
- **[16:41]** Concludes loop and graph engineering coexist and are needed for different use cases.
- **[17:06]** Shows how graphs are coded as engines, nodes, and edges in the repo.
- **[19:13]** Introduces the /graphs command and invites community workflow contributions.
- **[20:27]** Explains what is new versus 2023 deterministic workflows: non-deterministic nodes, model-picked edges, and guards.

## Concepts covered

- [agent-graph-engineering](/concepts/agent-graph-engineering.md)
- [loop-engineering](/concepts/loop-engineering.md)
- [agent-harness](/concepts/ai-agent-harness.md)
- [procedural-memory](/concepts/agent-memory-system.md)
- [workflow-routing](/concepts/agent-graph-engineering.md)
- [waku-agent](/entities/waku-agent.md)