---
type: concept
title: "Model Evaluation"
description: "The channel's 8-task model benchmark: how Kimi K3, Claude Opus 4.8, GPT, Gemini, Grok, and Fable 5 were raced on a local agent harness and what grades and costs revealed."
tags: [benchmarking, evaluation, agents, cost]
sources: [raw/you-can-learn-why-kimi-k3-blew-up.md]
timestamp: 2026-08-17T17:00:00Z
---

# Model Evaluation

To test Kimi K3 fairly, the channel races models inside its own local agent harness (Waku agent) using the compare tab, with a chart that "shows the scores in terms of the cost in terms of the grades for every model's performance" [01:31]. The field includes Claude Opus 4.8, Gemini 3.1 and 3.5 Flash, Kimi K3 and K2.7, Grok 4.5 and 4.3, OpenAI 5.4 mini and 5.3 chat, and Fable 5 [10:28]. Notably, GPT 5.6 is excluded because "it does not allow us to use tools" — the harness requires web search, calendar tools, code writing, and sub-agent spawning — so GPT 5.6 Soul is used instead as the referee and judge [10:52].

The grading rubric is deliberately rough and public. The hover card explains that 1-4 means "partial, vague, or partly wrong," while "9 to 10 means it's fully addressed the request, correct, concise, and honest" [11:54]. Scores are plotted against cost, so a model can win on quality, price, or the combination.

The benchmark ran eight questions covering the harness's tools. A trivial factual question (capital of France) passed everyone, though "Fable 5 triples the cost in terms of just answering" [11:20]. A calendar task — "schedule a coffee with Alex next Tuesday at 9:00 a.m." — required every model to pass the memory gate and call the create-event tool [13:10]. A Pokemon-team task exposed a real failure: "OpenAI failed for calling a tool... it's two out of three" [14:26]. A web-search task (England vs France World Cup, then draft a message to Sergey) showed very different tool habits: "Some people do full tools, some people do three tools, some people search the web twice, maybe even three times. Anthropic only searched once" [15:35]. The final task — build a Snake game in Python — forced the models through the delegate-task tool that spawns sub-agents using the Pi coding agent [16:18].

After eight races the results were clear. On cost, Grok 4.3 was cheapest and Kimi K2.7 second; "Kim K3 is bottom three, which is cheaper than Claude, Opus, and Fable," while Fable 5 cost "so much more money than the rest" [17:06]. On grades, "the best performing one so far, very interestingly, is Grock 4.5. It's got 8.3 and then Opus 4.8, Kim K 2.7, Kim K3 are 7.9, 7.6, 7.5, and then it's Gemini and everybody dropped under seven and surprisingly Fable 5 has the worst model" [17:21]. Anthropic's API pricing drew a strong reaction: "whoever is using Anthropic APIs, Jesus Christ, we're using so much more money than the rest of the models" [12:45]. Kimi's models landed in the top-left corner of the score-vs-cost chart: high quality, low spend [18:15].

Sean is candid about the limits of the method. Because GPT 5.6 Soul is the judge, he wonders "if it's because Chad GPT doesn't like Fable 5" [17:47]. He also stresses that model testing is "a dynamic game. Things will change over time" [17:51], and that a stable harness matters more than any single result: "having a stable harness for testing agents is really important... it's not an easy task. There's so many things you bump into to prepare a fair game for every model" [16:37].

## Part of / Related

- [Mixture of Experts](/concepts/mixture-of-experts.md)
- [Kimi K3](/entities/kimi-k3.md)
- [Waku Agent](/entities/waku-agent.md)
- [LLM Ops](/concepts/llm-ops.md)

## Sources

- [you-can-learn-why-kimi-k3-blew-up](/sources/you-can-learn-why-kimi-k3-blew-up.md)
