---
type: concept
title: "Loop Engineering"
description: "The reason-act-observe cycle an agent runs until a goal is reached, bounded by end-loop guardrails."
tags: [ai-agents, loops, system-design]
sources: [raw/you-can-learn-ai-agent-harness-loop-engineering.md, raw/you-can-learn-hermes-agent-harness.md, raw/you-can-learn-ai-agent-graph-engineering.md, raw/you-can-learn-ai-agent-harness-in-real-code.md, raw/you-can-learn-pi-minimal-coding-agent-harness.md]
timestamp: 2026-08-17T17:00:00Z
---

# Loop Engineering

A loop is the part of the harness that lets the agent work out its own plan: "A loop is basically saying, 'Hey, maybe sometimes you have a goal and you want to finish that goal, but we don't know the exact skills that you should have to finish that goal... here's a bunch of tools. Use them. Loop it until at some point you finish the goal'" [05:25-06:13]. It sits inside the harness because "a loop is also helping us to control this technology to make sure it runs the way we want it to run" [10:56-11:01]. At its simplest, "what a loop does is that it discovers what to do next" [08:33-08:35].

The mechanics are a reason-act-observe cycle. Pi Agent shows the minimal version: the LLM first checks "what kind of tools are there... Are we going to use any tools? If not, send the reply. If yes, are we allowed to use that tool?" - and if yes, it takes one of the four actions: read, write, edit, or bash [08:49-09:12]. Tool outcomes, including failures, flow back into the next iteration: "if it's blocked, it should return the results back to the LLM and the LLM is basically going to continue to run through the loop to determine if you have finished the goal" [12:28-12:38]. A richer example is the customer-service case: the agent reads CRM complaints (30 in two months), discovers 8 unreimbursed customers, schedules follow-up meetings for them, and might even "use the reimbursement trigger on Stripe or Alipay to refund the customer... Can you see that this is a loop until we finish the task?" [12:02-12:43].

The essential design question is when to stop, answered by end-loop guardrails: "If we give this horse or this LLM technology full power, it could just continuously do this forever... That's why we have this mechanism called end loop guardrails" [10:33-10:51]. "The very, very essential part of this loop is that it needs to know when it should stop" [12:53-12:58]. Guardrails can be simple - "the task is done" - or they can require user confirmation of the ending point, or proactive notification hooks: "you can set up a loop or set up a hook in clock code and telling it that you should always send me a notification on my laptop if you are pending on some permissions from me" [13:32-13:41]. Hermes demonstrates both sides: when a browser search found nothing, "the guardrail stopped and said, 'It didn't find anything'"; when the task succeeded, a mechanism fired: "Okay, end the loop, no more tool calls, and send the answer" [09:19-09:40].

Loops also have an economics side. Waku-Agent caps runs explicitly: "by default we set the maximize maximum iterations to be 10" [16:40-16:42], and its dashboard "is showing us how much money it's spending" per run [01:13-01:15]. Minimalism is measurable too: Pi's entire loop is `agent-loop.ts`, "It's got only 792 lines" [13:01-13:04]. Pure exploratory loops - deep research is "one of the early examples of a loop engineering workflow here, where you just say, 'Hey, go crazy. Just go search the internet. I want a report'" [07:52-08:01] - cost more than deterministic ones, which is part of why graphs emerged as a complement rather than a replacement.

Some loops never fully close; they improve themselves. Hermes is built around "a built-in learning loop. It creates its own skills from experience" [00:14-00:20]: "Every time when it realized that something is a mistake that it should learn from or it's a repeated task, it will start to summarize, 'Okay, here's some new memories I should know for the future'" [10:19-10:32]. A second, cheaper loop runs in the background: "it will start to consolidate some of those chats using the Hermes auxiliary models, which are cheaper, non-important models to do this summarization task" [12:29-12:42]. Finally, loops are not being replaced by graphs - loops live inside graph nodes, since "having an agent loop to search the web or have an agent loop to fix the bugs on GitHub is part of this graph" [10:30-10:44].

## Part of / Related

- [AI Agent Harness](../concepts/ai-agent-harness.md)
- [Agent Graph Engineering](../concepts/agent-graph-engineering.md)
- [LLM Ops](../concepts/llm-ops.md)
- [Hermes Agent](../entities/hermes-agent.md)
- [Pi Coding Agent](../entities/pi-coding-agent.md)

## Sources

- [you-can-learn-ai-agent-graph-engineering](/sources/you-can-learn-ai-agent-graph-engineering.md)
- [you-can-learn-ai-agent-harness-in-real-code](/sources/you-can-learn-ai-agent-harness-in-real-code.md)
- [you-can-learn-ai-agent-harness-loop-engineering](/sources/you-can-learn-ai-agent-harness-loop-engineering.md)
- [you-can-learn-hermes-agent-harness](/sources/you-can-learn-hermes-agent-harness.md)
- [you-can-learn-pi-minimal-coding-agent-harness](/sources/you-can-learn-pi-minimal-coding-agent-harness.md)
