---
type: Source
title: "You Can Learn Why Kimi K3 Blew Up In 20 Min | MoE, Delta Attention, Tested vs Claude, GPT, Grok"
description: "Explains Kimi K3's architecture (mixture of experts and delta attention) and benchmarks it against Claude, GPT, Grok, and Gemini in a local agent harness."
youtube_id: d3IxIvHOuUE
resource: https://www.youtube.com/watch?v=d3IxIvHOuUE
published: 2026-07-22
tags: [kimi-k3, mixture-of-experts, delta-attention, model-evaluation]
sources: [raw/you-can-learn-why-kimi-k3-blew-up.md]
timestamp: 2026-08-17T16:00:00Z
---

# You Can Learn Why Kimi K3 Blew Up In 20 Min | MoE, Delta Attention, Tested vs Claude, GPT, Grok

This video explains why the open-source Kimi K3 model went viral — its announcement post had more than 22 million views [00:03] — by breaking down two core architectural ideas and then testing the model in a real agent harness. K3 is a 2.8-trillion-parameter model with a 1 million token context, marketed with phrases like "delta attention, attention residuals, and built for long horizon agentic coding" [00:11]. Sean frames the concepts with simple analogies: parameters are like neurons in a brain, and attention means comparing every word with every other word, which is why 2x words yields 4x work [04:10].

The first key idea is mixture of experts (MoE). Instead of keeping the entire 2.8-trillion-parameter brain active, K3 "has 896 experts in total and only 16 of them will be awake every single time" [04:29], roughly doubling the sparsity of K2's 384 experts with 8 active [04:38], so only about 50 billion parameters run per query [03:41]. This sparse activation saves enormous compute as long as the expert-switching mechanism stays fast [04:59]. The second idea is delta attention: standard attention is an n-squared problem that recomputes relevance for every token pair, but K3 "will compute the same thing recursively instead of recomputing" — like a running mean or exponentially weighted moving average instead of re-summing all data [06:39]. That lets the model process a 1 million token context at linear attention cost [06:09].

The model is also "built for loops" [07:28]: agent loops resend almost the same context every iteration, and K3 reuses work from tokens it has already seen, making looped calls "10 times cheaper" [07:38]. On pricing, Sean notes K3 is "cheaper than Opus 4.8 and GPT 5.5" [07:55].

The second half is a live benchmark inside Waku-Agent's compare tab, pitting K3 and K2.7 against Claude Opus 4.8, GPT 5.3, Grok 4.3/4.5, Gemini 3.1/3.5, and Fable 5 across eight tasks — calendar scheduling, memory retrieval, building a Pokemon team, web search, and coding a Snake game in Python — using GPT 5.6 Soul as the judge because GPT 5.6 does not allow tool calls [11:17]. After eight races, Grok 4.5 topped grades at 8.3, with Opus 4.8, K2.7, and K3 at 7.9, 7.6, and 7.5 [17:21]; Fable 5 scored worst while costing far more than the rest [17:42]. On cost, K2.7 was the most token-efficient, and K3 sat in the bottom three by cost — more expensive than most models but "way cheaper than Anthropic Opus 4.8 and Fable 5" [12:31]. Sean closes with a brief history of language models — bag-of-words to LSTM to the 2017 "Attention Is All You Need" paper to transformers — arguing LLMs hit a cost wall because attention is n-squared, which is exactly what MoE and linear attention solve [19:13].

## Key moments

- **[00:03]** Notes Kimi K3's announcement post had more than 22 million views.
- **[00:11]** Lists the headline specs: 2.8 trillion parameters and 1 million context.
- **[02:29]** Defines MoE and the expert/neuron analogy for parameters.
- **[03:41]** Explains only about 50 billion parameters are awake at a time.
- **[04:10]** Illustrates why attention is quadratic: 2x words means 4x work.
- **[04:29]** Reveals K3's architecture: 896 experts with only 16 active per query.
- **[04:38]** Compares to K2's 384 experts with 8 active, roughly doubling sparsity.
- **[05:30]** Introduces Kimi delta attention as the second core concept.
- **[06:09]** Claims delta attention processes a 1 million token context at linear cost.
- **[06:39]** Explains the recursion as a running mean, an exponentially weighted moving average.
- **[07:28]** Explains K3 is built for loops, reusing work from tokens seen in prior iterations.
- **[07:38]** Claims looped calls become 10 times cheaper because context is not recomputed.
- **[07:55]** States K3 is cheaper than Opus 4.8 and GPT 5.5.
- **[11:17]** Explains GPT 5.6 Soul is used as judge because GPT 5.6 lacks tool calling.
- **[13:10]** Runs the calendar scheduling task across all models with create event.
- **[14:26]** Shows OpenAI failing a tool call during the Pokemon team task.
- **[17:02]** Reports eight tasks tested as eight model races.
- **[17:21]** Reveals grades: Grok 4.5 first at 8.3, then Opus 4.8, K2.7, and K3.
- **[17:42]** Notes Fable 5 was the worst performer despite high cost.
- **[18:37]** Recaps model history from bag-of-words through LSTM, attention, and transformers.

## Concepts covered

- mixture-of-experts
- delta-attention
- linear-attention
- agent-loop-economics
- model-evaluation
