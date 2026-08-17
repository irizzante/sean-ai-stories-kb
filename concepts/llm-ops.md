---
type: concept
title: "LLM Ops"
description: "The trace, evaluate, diagnose, and fix loop that keeps an AI agent system healthy and improving over time."
tags: [llm-ops, evaluation, tracing, rag]
sources: [raw/you-can-learn-ai-agent-harness-loop-engineering.md, raw/you-can-learn-ai-agent-harness-in-real-code.md, raw/you-can-learn-hermes-agent-harness.md]
timestamp: 2026-08-17T17:00:00Z
---

# LLM Ops

LLM Ops is "large language models operations," paired with eval, "which stands for evaluation system for AI agents" [00:05-00:12]. The motivation is blunt: "The biggest problem here is that we don't know how well it's performing. And that's why we need a feedback loop" [14:33-14:42]. The questions that loop answers are concrete: "can we have a better system prompt? Can we have a better large language model configurations? Is there something we should change for how we retrieve the AI agent memories?" [14:55-15:08]. The goal is iteration "until it's a healthy and well-performing system" [15:17-15:22].

The first step is tracing. One agent run means a user question sent to the LLM and a reply returned - tool calls inside it don't change that boundary [15:30-15:52]. "Every agent run, we should trace like a tree of events that happened," using tools like "LangFuse, could be LangSmith" [15:56-16:06]. What gets traced: "what did the person actually ask, what retrievals did the model actually retrieve, how many times did the large language model actually call the tools... how was the response time... and how many tokens have we used" [16:08-16:29]. Waku-Agent shows this in real code: its trace view records "how much tokens, how much money I have spent, how many LLM calls," what activated the retrieval gate, and which tasks were slowest - "the one that I asked about with the World Cup games took me almost 100 seconds" - all stored in local trace files, with an upgrade path to "Superbase or just use LangFuse directly" [03:13-03:44, 08:35-08:40].

The collected traces feed evaluation, which answers two questions: "Was it a good system run? And was it healthy?" [16:41-16:46]. Evaluation can be done "as a deterministic code" or "use an AI agent" - "we can probably use large language model as a judge here to give us a score on how well it performed" [16:49-17:14]. Waku's eval folder mirrors this split: a `deterministic` folder with rule-based tests ("checking if Apple Calendar was working perfectly" and whether "the working memory is working properly") and a `judge` folder where "we have Anthropic as a judge. It basically runs Anthropic models to assess some results," e.g. response quality [08:49-09:57]. These evals run automatically "right after the agent replied to you" [09:08-09:10].

Then comes the fix loop: diagnose, decide, and ship. Diagnosis asks where and why something broke - the meeting event never triggered, or latency is 20 seconds instead of 2 milliseconds - with typical causes like "maybe the working memory is too large" or unnecessary retrieval: "Maybe not every single question requires a retrieval from all these gigantic memory system... The model itself already knows" [17:21-18:07]. That insight is exactly Waku's retrieval gate: sometimes it skips retrieval entirely [18:54-18:59]. Shipping goes through a gate: "if the evaluation system passed, well, you can define the rules, we can either ship some very simple fix, have a new version of the prompt, or update the model configuration"; "The LLM Ops will feed the improved system prompt and the configuration of the model back to this agent run system" [18:16-18:37]. If something is deeply broken, the cycle restarts: "go fix the bug, rerun the agent run, resend the question, and then retrace the events, and then redo this evaluation system" [18:42-18:55]. The end state: "an autonomous system that will just self-evolve and grow over time" [19:49-19:51].

RAG is part of this loop, because retrieval is where much of the quality comes from. Semantic memory retrieval "is just rags" over facts and files; episodic memory is a time series that needs "a SQL query to query something that's pretty recent," but semantic questions over history need embedding-style search too: "You don't want the entire 2,000 messages. You want that 20 messages out of these 2,000 that are exactly relevant to what you want" [08:36-09:32]. Not every harness implements full LLM Ops: "on Hermes, based on my current research, I don't think it has an LLM ops or an eval system... it does trace the run... trajectory export and logs... but there's no eval" [18:25-18:41] - a gap users must fill themselves.

## Part of / Related

- [AI Agent Harness](../concepts/ai-agent-harness.md)
- [Loop Engineering](../concepts/loop-engineering.md)
- [Graph RAG](../concepts/graph-rag.md)
- [Model Evaluation](../concepts/model-evaluation.md)
- [Waku Agent](../entities/waku-agent.md)

## Sources

- [you-can-learn-ai-agent-harness-in-real-code](/sources/you-can-learn-ai-agent-harness-in-real-code.md)
- [you-can-learn-ai-agent-harness-loop-engineering](/sources/you-can-learn-ai-agent-harness-loop-engineering.md)
- [you-can-learn-hermes-agent-harness](/sources/you-can-learn-hermes-agent-harness.md)
