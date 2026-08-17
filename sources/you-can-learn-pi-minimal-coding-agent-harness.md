---
type: Source
title: "You Can Learn Pi Minimal Coding Agent Harness In 22 Min | Skills, Extensions, Packages, Bash"
description: "How Pi's deliberately minimal coding-agent harness works: four tools, one 792-line loop, and skills, extensions, and packages as opt-in extensibility."
youtube_id: 0sI0MbCt4f4
resource: https://www.youtube.com/watch?v=0sI0MbCt4f4
published: 2026-07-25
tags: [pi-coding-agent, coding-agent, agent-harness, loop-engineering]
sources: [raw/you-can-learn-pi-minimal-coding-agent-harness.md]
timestamp: 2026-08-17T16:00:00Z
---

# You Can Learn Pi Minimal Coding Agent Harness In 22 Min | Skills, Extensions, Packages, Bash

Sean walks through the system design of Pi, the 77.3k-star open-source coding agent, whose whole pitch is radical minimalism: "They basically claim that they don't do any MCPs, no sub agents, and no plan mode, no to-do's, no permission pop-ups, none of those" [00:08]. His thesis is that "some of the greatest projects are always built on top of some very simple, minimalistic building block" [00:25], and he verifies that claim by reading the actual Pi source code rather than the marketing site.

The harness turns out to be extremely small. It has four interfaces: a terminal UI, a one-shot CLI (`pi -p`), a JSON event stream that exposes the full thinking process (`pi --mode json`), and an RPC live pipe [02:58]. Context is assembled from just an `agents.md` file that defines response style — "no fluff or cheerful filler text" [06:36] — plus a system prompt in `packages/coding-agent/src/core/system-prompt.ts` [07:20]. The loop in `agent-loop.ts` is only 792 lines [12:42], and it runs exactly four tools: read, write, edit, and bash [09:04]. Finished sessions are stored as a forkable JSON tree in `~/.pi/sessions`, which Sean likens to version control for conversations [09:49].

The absence of MCPs is deliberate context discipline: "sometimes one MCP can add tens of thousands of hundreds of thousands of contexts into your 1 million token context window. And most of the time you probably won't even use it" [14:13]. Instead of default integrations, Pi grows through four user-controlled mechanisms: skills (a `.agents/skills` folder, "a procedural memory, basically" [15:13]), extensions (TypeScript files under `pi/extensions` that define real tools, "think of it as, you know, some kind of MCP" [17:36]), packages that bundle skills and extensions and install via `pi install` (an ecosystem of 2000+ packages [19:13]), and plain bash [20:43].

Sean also demonstrates Pi as a pluggable component inside a bigger harness: his own Waku-Agent spins up a sub-agent via a `delegate task` tool, and that sub-agent calls the Pi CLI to write code, which he believes is how Open Claw does its coding too [01:26]. Live demos cover a Pokedex skill [15:42], a Pokémon type-match extension [18:21], and a packaged `pi-pokedex` [19:38], all running locally on Haiku 4.5.

## Key moments

- **[00:08]** Pi claims no MCPs, no sub-agents, no plan mode, no todos, and no permission pop-ups
- **[00:42]** The Pi repo has 77.3k GitHub stars
- **[00:53]** Waku-Agent's `delegate task` tool spawns a sub-agent that calls the Pi CLI
- **[01:40]** Demo: a Pokémon script request is delegated to Pi as the coding specialist
- **[02:58]** Four faces of Pi: TUI, one-shot CLI, JSON event streaming, and RPC live pipe
- **[04:22]** `pi -p` runs a single prompt and returns one answer
- **[04:43]** `pi --mode json` streams the entire thinking process
- **[06:17]** `agents.md` defines response behavior, including "no fluff or cheerful filler text"
- **[07:20]** The system prompt lives in `packages/coding-agent/src/core/system-prompt.ts`
- **[09:04]** The loop has only four actions: read, write, edit, and bash
- **[09:49]** Sessions are stored as a JSON tree and can be forked with `/fork`
- **[12:42]** The entire loop is `agent-loop.ts` at 792 lines
- **[14:08]** MCP context bloat is the reason Pi ships with no default MCPs
- **[14:51]** Pi gets stronger through user-written skills, extensions, packages, and bash
- **[15:08]** A skill is procedural memory stored in the `.agents/skills` folder
- **[15:42]** The Pokedex skill fetches types, stats, and abilities from a public Poké API
- **[17:21]** Extensions are TypeScript files under `pi/extensions` defining tools
- **[18:21]** The pokemon-battle extension's `type_match` function reasons about 4x effectiveness
- **[19:13]** The Pi ecosystem has more than 2000 packages
- **[19:38]** `pi install` pulls a packaged skill-and-extension bundle

## Concepts covered

- [pi-coding-agent](/entities/pi-coding-agent.md)
- [agent-harness](/concepts/ai-agent-harness.md)
- [loop-engineering](/concepts/loop-engineering.md)
- agent-skills
- agent-extensions
- minimal-agent-design