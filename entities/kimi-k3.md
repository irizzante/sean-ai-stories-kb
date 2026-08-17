---
type: entity
title: "Kimi K3"
description: "Kimi's open-source 2.8T-parameter model: MoE with 896 experts, delta attention, loop reuse, and its results in the channel's 8-task harness benchmark."
tags: [model, open-source, kimi, moe]
sources: [raw/you-can-learn-why-kimi-k3-blew-up.md]
timestamp: 2026-08-17T17:00:00Z
---

# Kimi K3

Kimi K3 is an open-source large language model from the Kimi (Moonshot AI) team that "blew up the internet" at launch — the release post had "more than 22 million views" [00:03]. Its headline specs are 2.8 trillion parameters with a 1-million-token context [00:11], and the launch language Sean highlights is "give me delta attention, attention residuals, and built for long horizon agentic coding" [00:15]. His video exists to translate those phrases: he walks through the mixture-of-experts architecture and delta attention conceptually, then tests the model in a real harness rather than trusting hype [00:22].

Architecturally, K3 is a sparse mixture-of-experts model: "we're going to have 896 experts in total and only 16 of them will be awake every single time when you ask a question" [04:29]. This doubles the sparsity of K2's 384 experts with 8 active [04:41], so only about 50 billion parameters fire per request out of 2.8 trillion [03:41]. Kimi delta attention turns the n² all-pairs attention problem into a running-average style computation — "an attention computed like a running average instead of a resuming everything each step" [07:06] — so a 1M-token context processes at linear attention cost [06:09]. The model is also built for loops, reusing computation on tokens seen in previous iterations to make agent loops "10 times cheaper" [07:31], which the video presents as the answer to why agentic coding is affordable on such a large model.

In the channel's 8-task benchmark on the Waku agent harness, K3 finished mid-field on quality and strong on price. Its grade was 7.5, behind Grok 4.5 at 8.3, Claude Opus 4.8 at 7.9, and its sibling K2.7 at 7.6 [17:21]. On cost, "Kim K3 is bottom three, which is cheaper than Claude, Opus, and Fable" [17:10] — Sean notes it spent "slightly more money" than K2.7 but "almost half of anthropic opus 4.8" [14:50]. He summarizes the placement as Kimi sitting "kind of in the top left corner" of the score-vs-cost chart, i.e. high value for money [18:15].

The video also shows K3 operating inside the harness as an everyday agent: asked "tell me what is on my calendar today," it decides to retrieve semantic memory, loops over tools, calls list-events, and reports a Pokemon training session at 6-7 p.m. [09:00]. It ran the same gates as every other model — memory retrieval, create-event, web search, and the delegate-task tool that spawns Pi coding sub-agents for the Snake game task [16:18].

## Part of / Related

- [Mixture of Experts](/concepts/mixture-of-experts.md)
- [Model Evaluation](/concepts/model-evaluation.md)
- [Waku Agent](/entities/waku-agent.md)
- [Pi Coding Agent](/entities/pi-coding-agent.md)

## Sources

- [you-can-learn-why-kimi-k3-blew-up](/sources/you-can-learn-why-kimi-k3-blew-up.md)
