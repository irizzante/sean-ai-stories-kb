---
type: entity
title: "Pi Coding Agent"
description: "A minimal open-source coding agent harness with only read, write, edit, and bash tools, extended via skills, extensions, and packages."
tags: [pi-agent, coding-agent, harness, open-source]
sources: [raw/you-can-learn-pi-minimal-coding-agent-harness.md]
timestamp: 2026-08-17T17:00:00Z
---

# Pi Coding Agent

Pi is a deliberately minimal open-source coding agent harness - "They basically claim that they don't do any MCPs, no sub agents, and no plan mode, no to-do's, no permission pop-ups, none of those," a list you can verify on pi.dev's "what we did not build" page [00:08-00:23]. Sean's interest came from the philosophy: "some of the greatest projects are always built on top of some very simple, minimalistic building block" [00:26-00:33], and the repo backs it up with 77.3 thousand GitHub stars [00:42-00:45]. Pi exposes only "four main costumes" as interfaces: the TUI, one-shot CLI (`pi -p`), event streaming (`pi --mode json`, which "will spit out all those thinking steps"), and an RPC live pipe [02:58-03:20]. You log in via `/login` (Anthropic account or API key) and pick models with `/model` - Sean's demos run Claude Haiku 4.5 [03:49-04:10]. Its behavior file, `agents.md`, sets the tone: "no fluff or cheerful filter text. If you're saying thanks, just don't say thanks so much" [06:40-06:49].

The design is small and readable. Context preparation combines `agents.md` with a system prompt from `packages/coding-agent/source/core/system-prompt.ts` - "You are an expert coding assistant operating inside Pi a coding agent harness" - and "these two will be combined into a JSON file, which is forkable, and they'll be fed into the Pi Agent loop" [07:20-07:52]. The loop itself is `agent-loop.ts`, "It's got only 792 lines" [12:42-13:04]. Tools live in `packages/coding-agent/source/core/tools`: "bash.ts, they've got edits.ts, find, grep... Basically, four main tools: read, write, edit, bash. Super simple" [09:23-09:47]. Sessions are stored as "a JSON file with some kind of tree structure" in the local `~/.pi/sessions` folder, browsable with `/tree` and branchable with `/fork` - "it's technically version control, right? You can trace back to exactly what you wrote in the past and it can branch into different sessions" [09:51-12:13].

Pi's minimalism is a deliberate answer to context bloat. "Sometimes one MCP can add tens of thousands of hundreds of thousands of contexts into your 1 million token context window. And most of the time you probably won't even use it" [14:09-14:22]. So Pi "reduced that completely... instead of saying, 'Hey, by default, let me connect all these MCPs back to you.' I'll let you decide" [14:44-14:51] through four extension mechanisms: skills ("a skill is basically you can tell an agent to behave in a way that you want... It's a procedural memory" [15:06-15:15]), extensions (TypeScript files defining real tools - "think of it as, you know, some kind of MCP, which will sort of let you use some tools" [17:36-17:42]), packages ("the pi agent ecosystem has got more than 2000 packages" built from bundled skills and extensions [19:11-19:21]), and plain bash plus a readme. Sean's Pokédex demos show each: a skill that pulls Pokémon stats from the Poké API (Snorlax "is much slower because it's fat... Its ability is has thick fat" [16:35-16:53]); an extension `pokemon-battle.ts` whose `type_match` function reasons "rock type is very effective on fire and flying. So the effect becomes four times" [18:30-18:46]; and an installable `pi install` package wrapping both [19:38-19:50].

Pi's real strength is as a pluggable coding specialist inside other harnesses. Sean's Waku-Agent demo uses "this tool called delegate task. Delegate task basically spun up the sub-agent called Pi Agent" which calls the Pi CLI to write code and returns it [00:53-02:30] - "you can literally just plug in into any of these harness systems you build yourself" [02:09-02:14]. He suspects "this is how Open Claw did the coding for themselves" [01:26-01:34]. The trade-off is honesty: Pi is "not as good as Claude code" out of the box, precisely because Claude Code is "a closed source coding agent harness" with "a ton of MCPs, sub-agents" and permission pop-ups [13:31-14:07]. The community energy - extensions shared in the "shitty coders club" Discord - is, for Sean, why "an open source project like pie agent is very popular" [20:10-20:39].

## Part of / Related

- [AI Agent Harness](../concepts/ai-agent-harness.md)
- [Loop Engineering](../concepts/loop-engineering.md)
- [Waku Agent](../entities/waku-agent.md)
- [Hermes Agent](../entities/hermes-agent.md)

## Sources

- [you-can-learn-pi-minimal-coding-agent-harness](/sources/you-can-learn-pi-minimal-coding-agent-harness.md)
