---
type: concept
title: "Mixture of Experts"
description: "How Kimi K3's sparse 896-expert architecture, delta attention, and loop reuse cut the cost of running a 2.8T-parameter model."
tags: [model-architecture, kimi, attention, cost]
sources: [raw/you-can-learn-why-kimi-k3-blew-up.md]
timestamp: 2026-08-17T17:00:00Z
---

# Mixture of Experts

The channel's Kimi K3 explainer starts from a mental model: a parameter is like a neuron, and a 2.8-trillion-parameter model is "a brain with 2.8 trillion parameters" [02:31]. The obvious question is why models don't just grow to 100 trillion parameters, and Sean's answer is blunt: "it's going to be very very slow. Mathematically speaking, you don't want all the parameters or neurons to be awake at the same time" [03:33]. Running every parameter on every token costs far too much compute, so sparse activation becomes the whole game.

Mixture of Experts (MoE) is the mechanism that keeps the brain large but mostly asleep. Instead of activating the entire model, Kimi K3 has "896 experts in total and only 16 of them will be awake every single time when you ask a question" [04:21]. Sean contrasts this with the previous generation: K2 had 384 experts with only 8 active, so K3 "technically doubles that sparsity" [04:47]. Different questions wake different experts: asking about breakfast fruit and asking about a World Cup result should route to different subsets, and the expert-switching mechanism has to react fast for the approach to scale [05:01]. Sparse activation means attention and weight calculations only touch the awake experts, which "is going to save you so much time" [04:49].

The second idea is why plain attention alone would be too expensive. Standard attention compares every word with every other word, so 10 words become 100 calculations — "if you have 2x words you're going to get 4x work" [04:13]. Kimi delta attention avoids this n² blowup by computing attention recursively, like a running average: "you would never get a mean by resuming all data on every new point... it's going to run a running mean and update it over time, which is an exponentially weighted moving average" [06:41]. Sean's summary: "kim delta attention is an attention computed like a running average instead of a resuming everything each step" [07:06]. With a 1-million-token context, this lets K3 process at linear attention cost [06:09].

The model is also "built for loops" [07:28]. Agent loops resend nearly the same context every iteration — "it's going to pass down the entire previous conversations into the LLM. So, it's a waste of tokens and money" [07:48]. K3's answer is reuse: "when the model already saw some of those tokens in the last loop, it reuses the work instead of recomputing it, which makes it 10 times cheaper" [07:31]. This matters precisely because the channel tests the model inside a loop-based agent harness.

Why sparse activation changes economics: total parameter count and per-token compute are decoupled, so a 2.8T-parameter model can stay affordable while getting larger. Sean frames the history of language models the same way: counting words, then LSTM, then attention, then transformers, then "large language models hit the cost wall because there are too many parameters and the attention weight you're calculating becomes n squared — which is why we need mixture of model mechanism and the linear approximation for the Kimmy delta attention" [19:13]. The practical result in the video: Kimi K3 is claimed to be "cheaper than Opus 4.8 and GBD 5.5" [07:55], and in the channel's own benchmark it cost roughly half of Claude Opus 4.8 [14:55].

## Part of / Related

- [Kimi K3](/entities/kimi-k3.md)
- [Model Evaluation](/concepts/model-evaluation.md)
- [Loop Engineering](/concepts/loop-engineering.md)
- [AI Agent Harness](/concepts/ai-agent-harness.md)

## Sources

- [you-can-learn-why-kimi-k3-blew-up](/sources/you-can-learn-why-kimi-k3-blew-up.md)
