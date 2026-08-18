# Sean's AI Stories Knowledge Base

A queryable OKF (Open Knowledge Format) knowledge base built from the YouTube channel
[Sean's AI Stories](https://www.youtube.com/@SeanAIStories) — videos about building AI
products, agent harness engineering, memory systems, and startup interviews.

The bundle distills 15 videos into interlinked concept and entity pages, so an AI agent
(or a human) can query the knowledge without re-reading transcripts.

## Structure

```
raw/        # 15 immutable video transcripts with [mm:ss] timestamps
sources/    # one page per video: synthesis + key moments
concepts/   # 16 cross-video concept pages (one idea per file)
entities/   # 13 pages: tools, organizations, people
index.md    # mandatory entry point for every query
log.md      # change history
```

- **`raw/`** - the source of truth. Transcripts are read-only; every factual page cites them.
- **`sources/`** - per-video pages: what the video teaches, key moments with timestamps, and links to the concepts and entities it covers.
- **`concepts/`** - the ideas that span multiple videos, e.g. `ai-agent-harness`,
  `loop-engineering`, `agent-memory-system`, `graph-rag`, `mixture-of-experts`,
  `ai-startup-fundraising`. Each page synthesizes every video that discusses the topic.
- **`entities/`** - tools (`pi-coding-agent`, `hermes-agent`, `waku-agent`, `kimi-k3`),
  organizations (`a16z`, `character-labs`, `automanus`), and people interviewed on the channel.

## How to query it

Always start from `index.md`, then drill down:

```
index.md → concepts/index.md → concepts/agent-memory-system.md
```

Pages carry frontmatter (`type`, `title`, `description`, `tags`, `sources`) for filtering and
traversing, and link to each other root-relative — the link graph is the knowledge graph.

For an agent, the natural flow is progressive disclosure: read the top index, pick the section
index that matches the question, then read the relevant pages. Do not feed raw transcripts
directly; that is what the concept pages are for.

## Coverage

| | |
|---|---|
| Videos | 15 (2026-03 → 2026-08) |
| Source pages | 15 |
| Concept pages | 16 |
| Entity pages | 13 |
| Format | OKF v0.1, lint-clean |

## Extending

When a new video is published:

1. Download its transcript into `raw/<slug>.md` with `[mm:ss]` timestamps.
2. Write a `sources/<slug>.md` page (`type: Source`, `sources: [raw/<slug>.md]`).
3. Grep the affected concept/entity pages and make surgical edits; create new concept pages
   for genuinely new ideas.
4. Re-link and lint.

Every factual page keeps a `sources` entry pointing at the raw files it was compiled from;
compile from `raw/`, never from memory of a prior page.

## License

Transcripts and summaries derive from the videos of [Sean's AI Stories](https://www.youtube.com/@SeanAIStories)
and remain the property of their author. The synthesis pages in this bundle are provided for
reference and learning.
