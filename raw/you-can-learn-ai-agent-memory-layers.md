# You Can Learn AI Agent Memory Layers | Graph RAG, Vector DB, SQLite, Hermes, Waku

youtube_id: 072eNztI06k
published: 2026-08-16

**[00:00]** Hamilton's on. So, memories are super
**[00:02]** popular term in AI agent systems
**[00:03]** recently, and the reason for that is
**[00:05]** that any LLM call does not carry any
**[00:09]** weight for long terms. The reason why
**[00:11]** your ChatGPT and Claude code remembers
**[00:13]** what you talked about from the past is
**[00:14]** because it has already crafted this
**[00:17]** memory system for their own AI agent
**[00:19]** harness. Today, we're going to cover
**[00:20]** five different ways of how you're going
**[00:22]** to architect a AI agent memory around
**[00:24]** the harness you built. In previous you
**[00:26]** have watched some our videos, we have
**[00:28]** created this our agent harness called
**[00:29]** Waku agent. It basically has this agent
**[00:31]** run that has a loop for the agent to
**[00:33]** call tools, delegate sub agents for
**[00:36]** tasks, and at the same time it's going
**[00:38]** to prepare this working memory with
**[00:40]** retrieving from from three main pillars,
**[00:44]** which is procedural memories, and in our
**[00:46]** case it's a skill, semantic memory,
**[00:48]** which is some durable facts, and
**[00:51]** episodic memory, which is some dated
**[00:52]** events. And that was pretty much similar
**[00:55]** to how Hermes agents crafted their own
**[00:57]** memory system. But, if you're serious
**[00:59]** about building agents, I'm sure you have
**[01:00]** been bombarded with information such as
**[01:02]** rags, agentic rag, graph rag. Retrieval
**[01:06]** augmented generation has always been
**[01:07]** there, but there's no retrievals or
**[01:10]** embeddings in Hermes and Waku agent.
**[01:13]** We're going to tell you the difference
**[01:14]** between these two separate systems
**[01:16]** because they are two different ways of
**[01:18]** retrieving memories. And I hope this
**[01:20]** will be helpful for you because
**[01:21]** eventually it depends on you what kind
**[01:23]** of memory systems matters the most to
**[01:25]** your use case, and then you should make
**[01:27]** a decision by yourself. And if you want
**[01:29]** to try out all these agent harness and
**[01:30]** memory systems and everything, we have
**[01:32]** built a open source project called Shen
**[01:35]** Shen Chan's {slash} Waku {dash} agent,
**[01:37]** and we recently received more than 1.3
**[01:39]** thousand stars. So, thanks everyone for
**[01:42]** your support, and we'd love to have you
**[01:43]** to contribute to this repo. And the way
**[01:45]** to use it is very simple. You can either
**[01:47]** pip install Waku agent, or you can get
**[01:50]** clone this repo and then start working
**[01:51]** on it. Once you start running it, you
**[01:53]** will have an agent like this, and you
**[01:55]** can ask it questions and be like, what
**[01:57]** is on my calendar today? If you have
**[02:00]** your calendar, you know, properly set
**[02:02]** up. And it's going to pass through the
**[02:04]** retrieval gate and then, you know, use
**[02:06]** the tools like list events to check our
**[02:07]** calendar and all these kind of stuff.
**[02:09]** So, this is a proper agent harness that
**[02:10]** will allow you to play around with your
**[02:12]** memory system and tools that you build
**[02:14]** for yourself. After finishing the
**[02:16]** tracing and then giving us back the
**[02:18]** answers, we're pretty much done for one
**[02:20]** agent run. And we also built up this
**[02:21]** arena for memory systems to compare a
**[02:23]** few different memory layers options on
**[02:25]** the market. We're going to show you all
**[02:26]** the real code and implementations at the
**[02:28]** latter half of the video. For now, let's
**[02:30]** jump back to the system design for the
**[02:31]** concept explanations first. First things
**[02:34]** first, here's how I would think about
**[02:36]** agent memories.
**[02:37]** I would think about three main pillars
**[02:39]** first. What is it? How to find it? And
**[02:42]** how do we maintain it? Normally, an
**[02:44]** agent memory will be stored in three
**[02:47]** different ways. The first one is text or
**[02:49]** markdown file, just like your memory.md.
**[02:52]** For example, if you come to Hermes and
**[02:54]** just ask any questions and say hi,
**[02:57]** and then you'll see your root directory.
**[02:59]** And if you scroll down to .hermes,
**[03:02]** right here, and then scroll down, you
**[03:04]** can find out that and then you'll see a
**[03:07]** folder called memory and then
**[03:09]** double-click on this memory.md, which
**[03:11]** show you the memories right here. Okay,
**[03:13]** so this is just plain text and it's
**[03:15]** going to be fed into the context window
**[03:17]** whenever you ask any questions. In and
**[03:20]** similarly in Waku agent, if you clone
**[03:21]** this repo, after you ask after you ask
**[03:24]** some first questions, you'll be able to
**[03:25]** find this folder called .waku and then
**[03:27]** you can find things like so.md, which is
**[03:29]** a system prompt for your AI agent
**[03:32]** memory. So, basically, it can be just in
**[03:34]** plain text. Or, if things get more
**[03:37]** complicated, it can store them in a
**[03:38]** table, like a spreadsheet or like a
**[03:40]** Google Sheet, with rows and columns, all
**[03:42]** these kind of stuff, just like an Excel
**[03:43]** Sheet. And last but not least, we can
**[03:45]** also store information in a graph with
**[03:47]** nodes and edges. And for people who are
**[03:49]** not familiar with graphs, it's basically
**[03:51]** a way to build up connections between
**[03:54]** information. And I found this really
**[03:56]** cool tool called Zap. And they have this
**[03:58]** relational graph that after you use this
**[04:02]** memory layer to store information, it
**[04:04]** will plot this out for you. For example,
**[04:06]** let's take a look. Uh let's say this
**[04:08]** founder called Alex. And Alex has been
**[04:11]** to this Lisbon AI meetup event uh for
**[04:15]** his robotics startup.
**[04:17]** And
**[04:18]** and you can see that these information
**[04:20]** are all interconnected. So, it started
**[04:22]** with this username called
**[04:23]** quickstartzap3.
**[04:24]** And then Alex similarly has a product
**[04:26]** launch date, and those were in say in
**[04:30]** May. They had a product launch. And June
**[04:32]** also had a product launch. So, graph is
**[04:35]** just a way to store information that
**[04:37]** helps you find connections between
**[04:39]** infos. And I think these are the three
**[04:41]** major ways of storing memories. But
**[04:43]** people might be asking, where's
**[04:44]** embedding for retrieval augmented
**[04:46]** generation? It depends on what vector
**[04:48]** stores you're using. If you're using
**[04:50]** Supabase PG vector like myself, it's
**[04:52]** going to be still in rows in the table,
**[04:54]** but then, you know, some of the columns
**[04:56]** are going to be are going to be vectors.
**[04:58]** Or you can store them in a NoSQL
**[04:59]** database. So, that's what is it, right?
**[05:02]** And then now it comes to how does our
**[05:03]** agent find out about it? There are four
**[05:06]** ways for AI agent to [clears throat]
**[05:07]** find the memories. The first one is do
**[05:10]** nothing. Remember the memory.md that we
**[05:12]** showed you earlier for Hermes? That's
**[05:14]** basically do nothing because because if
**[05:17]** the memory.md is not too long, it's
**[05:19]** supposed to be read by default by the
**[05:21]** LLMs so that it's always in the context
**[05:23]** anyways. Remember we view use Claude
**[05:25]** code, you can see how much percentage of
**[05:27]** the context window have you used. And
**[05:30]** sometimes it's huge. And the reason is
**[05:32]** because some of the memories are just
**[05:34]** going to be preloaded there. And also of
**[05:36]** course, there are a bunch of, you know,
**[05:37]** tool calls, definitions, MCP
**[05:39]** definitions, um your soul.md, which is
**[05:43]** the system prompt for the role that the
**[05:45]** agent is playing. Other than that, we
**[05:47]** can also do keyword, which is something
**[05:50]** that SQLite has, which is a standard
**[05:52]** called FTS5.
**[05:54]** All you need to know is basically it's
**[05:55]** doing keyword searching, okay? And an
**[05:58]** example in Hermes is that if you go if
**[06:00]** you come to Hermes and you scroll down
**[06:02]** again the same folder, there's something
**[06:04]** called state.db.
**[06:06]** And if you open that, you can see a
**[06:08]** SQLite schema here.
**[06:10]** All right? And the and the keyword
**[06:13]** search is basically given these
**[06:15]** state.db,
**[06:17]** we're just going to search the keywords
**[06:18]** of the information. And the third one is
**[06:20]** for retrieval augmented generation. It's
**[06:22]** something that it's basically checking
**[06:24]** the similarity between two words. Say
**[06:27]** Say let's let's say you're asking a
**[06:28]** question regarding my favorite food. And
**[06:32]** the word food might be embedded into a
**[06:34]** vector of space, you know, 1024 by 1.
**[06:37]** And then it's going to just calculate
**[06:38]** what other words that are embedded in
**[06:40]** the same dimensions in our database have
**[06:43]** a high similarity to food. Maybe it's
**[06:45]** going to be apple, maybe it's going to
**[06:47]** be sausages, or so on and so forth.
**[06:49]** Okay? So, what we're trying to do is
**[06:51]** doing a semantic search instead of just
**[06:52]** doing keywords. Last but not least is
**[06:55]** graph rack. What graph rack does is very
**[06:57]** simple. Remember I showed you about the
**[06:58]** graphs earlier? What it does is
**[07:00]** basically it's still embedding the
**[07:02]** information, but it embeds things like
**[07:04]** the nodes, okay? It may be embed, you
**[07:06]** know, product launch date. And it also
**[07:08]** embed that that edge, like is it is it a
**[07:11]** part of the observation or is it a
**[07:13]** relationship, okay? And
**[07:16]** and all of these will be embeddings. The
**[07:18]** similarity search will just find out,
**[07:19]** you know, what's similar to the question
**[07:21]** that the user asked. And then eventually
**[07:23]** it might return a relationship graph
**[07:25]** here, so that the agent has more context
**[07:27]** about the memories in relationships. So,
**[07:29]** now, how do we maintain it? I have
**[07:32]** summarized this into four main ways of
**[07:35]** maintaining a memory system. The first
**[07:37]** one is you got to make a decision, which
**[07:40]** is do we add, do we delete, do we
**[07:43]** overwrite some previous information, do
**[07:44]** we do nothing?
**[07:46]** Okay? This one means no operations. Or
**[07:48]** do we retire some information, which by
**[07:50]** the way is different from deleting,
**[07:52]** because we're not deleting it. We're
**[07:53]** invalidating
**[07:55]** the previous information with some time
**[07:57]** range. What does that mean? We launched
**[07:58]** the Waku agent 1 month ago and it got
**[08:01]** 1,000 stars in the first 25 days. Okay?
**[08:05]** And then next day I'm telling the agent,
**[08:06]** "Today is day 26 and the Waku agent has
**[08:08]** got 1.3 thousand stars." So it increased
**[08:11]** 30% in just 1 day. And then what would
**[08:14]** should happen is that instead of
**[08:16]** deleting the fact that this GitHub repo
**[08:19]** has gained 1,000 stars in 25 days, which
**[08:22]** is still
**[08:23]** important information. It can probably
**[08:25]** just invalidate it and be like, "Hey,
**[08:26]** the latest stars is 1.3 thousand already
**[08:29]** and you can trace back to 1 day before,
**[08:32]** which is 1,000 stars." And these
**[08:34]** contexts are still important for future
**[08:37]** tracing purposes. The third one is
**[08:39]** called attribute, which in human
**[08:41]** language is that it's basically tracing
**[08:44]** where the source comes from. Okay? Maybe
**[08:47]** I got the memory from the users
**[08:48]** communicating with your agent or maybe I
**[08:50]** got it from some web search or maybe I
**[08:53]** got it from some calendar search, right?
**[08:56]** Depends on where the source comes from.
**[08:59]** And last but not least, we are talking
**[09:00]** about reflect, which is it's going to
**[09:03]** drop or merge some of the duplicates or
**[09:05]** some of the outdated information. I mean
**[09:08]** it's kind of similar to delete and kind
**[09:10]** of similar to retire, but reflect
**[09:12]** sometimes can link to what Anthropic has
**[09:14]** proposed, which is dreaming.
**[09:16]** Dreaming happens when we are not
**[09:17]** working. When the agent is running, it's
**[09:19]** like busy accumulating facts,
**[09:21]** accumulating episodic memories,
**[09:23]** accumulating procedures into skills. But
**[09:26]** then when it's not running, we could
**[09:27]** probably schedule some tasks to let it,
**[09:29]** you know, reflect on everything that we
**[09:31]** have collected and then merge some of
**[09:32]** the duplicates or drop some of the stuff
**[09:35]** that are not important anymore. So it's
**[09:36]** kind of like a a postmortem or post
**[09:39]** process
**[09:40]** um
**[09:41]** step to update or maintain the memory
**[09:44]** system. You guys still with me? Good.
**[09:46]** Let's keep going. Now, let's see some
**[09:48]** different types of memory systems with
**[09:50]** real products. And let me add the vector
**[09:53]** store here. So, first thing first, plain
**[09:56]** text ways of storing memories.
**[09:58]** Examples are Hermes and Waku agent. I've
**[10:01]** shown you Soul earlier, which is text
**[10:04]** and it's basically system prompt. And
**[10:06]** you can just edit it, right? If you If
**[10:08]** we come back to
**[10:10]** If we check out the Soul of Hermes,
**[10:13]** you can see that my Hermes has a
**[10:15]** personality, which is it should always
**[10:16]** talk like Pikachu. It should say
**[10:18]** "Pikapi" all the time.
**[10:20]** And
**[10:21]** and there's some variations. You can say
**[10:22]** "Pika" or "Pika Pika" or "Pikapi",
**[10:25]** right? And the Pikapi reserved for
**[10:27]** addressing
**[10:28]** me directly. Like, it should call me as
**[10:31]** Pikapi. Because in the anime, Pikachu
**[10:33]** also calls Satoshi or Ash Pikapi. And
**[10:36]** you can edit this to anything else,
**[10:37]** right? So, so it's very simple to
**[10:39]** understand. And skills is a procedure.
**[10:42]** For example, research about all AI agent
**[10:44]** videos on the internet and then inform
**[10:46]** me every morning what are some of the
**[10:48]** latest news that Sean Stories should
**[10:51]** Sean AI Stories should cover for the
**[10:52]** next video, right? This is a procedure.
**[10:54]** This is skill. And it's usually loaded
**[10:57]** by trigger, okay? So, if I'm asking my
**[10:59]** agent, then be like, "Hey, trigger that
**[11:01]** skill for Sean AI posts." And then it
**[11:05]** should run it and then fetch it for me.
**[11:06]** And I should be always be able to just
**[11:08]** edit it myself. Memory.md, which is some
**[11:11]** durable facts that you should keep
**[11:12]** accumulating when you're talking to
**[11:14]** agents like these. This is from a
**[11:16]** previous video for showing you how to
**[11:17]** build agent harness in real code. And
**[11:19]** the way that we build up semantic
**[11:21]** memory, which is basically memory.md, is
**[11:24]** that every time when you have a
**[11:25]** conversation with the agent from the
**[11:27]** user prompt to the LLM to the reply, it
**[11:30]** just save the history into the state.db,
**[11:33]** which is our SQLite database, and it
**[11:35]** should consolidate the information after
**[11:38]** every, you know, say five or 10
**[11:40]** conversations using some cheaper
**[11:42]** auxiliary models,
**[11:44]** uh and then it should distill the facts
**[11:45]** into the memory.dimd.
**[11:47]** And these memories usually are loaded in
**[11:49]** context because that's important, but
**[11:51]** you can also make it retrievable. You
**[11:52]** can build up a You can build up a
**[11:54]** retrieval gates like what we do in uh
**[11:56]** Waku agent, and uh you should decide if
**[11:59]** it should uh cause call up some skills,
**[12:01]** call up some cementing memories, and
**[12:03]** stuff, right? It doesn't have to be
**[12:04]** always be there, but you can do that if
**[12:06]** you want to. And remember, agent harness
**[12:08]** is very flexible. You don't have to
**[12:09]** stick to any standard. You can You can
**[12:11]** just craft your own harness. What
**[12:13]** Eventually What What makes What lasts
**[12:16]** forever or what matters most to you
**[12:18]** eventually is the memories. You If
**[12:19]** you're committing these memories and
**[12:21]** then store them well and prepare them
**[12:22]** well and then take care of them, then
**[12:24]** these memories are the most valuable
**[12:25]** assets for any AI agent harness.
**[12:29]** Whether or not we should have retrieval
**[12:30]** gate, that's completely up to you, okay?
**[12:33]** And last but not least, remember we just
**[12:35]** showed you the state.db, which is the
**[12:36]** SQLite database, and it's a relational
**[12:38]** database with rows, and you're doing the
**[12:41]** keyword searching for how to find it,
**[12:43]** and then the way we maintain it is that
**[12:45]** you can You can just edit it yourself.
**[12:47]** Like
**[12:48]** Like if you click on here, yeah. You can
**[12:50]** just write things into the state DB, or
**[12:53]** you can wait for the agent harness to
**[12:55]** consolidate it like
**[12:57]** like what I showed you in Waku agent,
**[12:58]** the consolidation. And in the real code,
**[13:01]** we also have a consolidation
**[13:04]** module right here. You click into it,
**[13:06]** you can see what happened in
**[13:07]** consolidations in the past history.
**[13:10]** Okay.
**[13:11]** So, that was plain text style. What else
**[13:12]** do we have?
**[13:13]** We've got Superbase,
**[13:16]** Weaviate, Pinecone, which have vector
**[13:19]** stores. Well, Superbase is a relational
**[13:22]** database, so it's technically not a
**[13:23]** vector store, but they do have a SQLite
**[13:26]** extension called PG Vector, which is
**[13:29]** technically a vector store that you can
**[13:30]** use.
**[13:31]** Vector stores usually store information
**[13:33]** in vectors, which as I mentioned earlier
**[13:36]** is going to embed every single word into
**[13:39]** a high-dimensional vectors with numbers
**[13:41]** in it because computers cannot process
**[13:43]** on words. They can only
**[13:45]** They can only process numbers or higher
**[13:47]** dimensions of numbers. That's why
**[13:49]** vectors are very useful. And then you
**[13:51]** can store them some metadata. For
**[13:52]** example, what does this vector really
**[13:54]** mean and what's some other information
**[13:56]** should be carried with it, okay? And the
**[13:58]** way we find it is that we're going to do
**[14:00]** this thing called similarity search.
**[14:02]** Remember earlier we said that we're
**[14:04]** going to put a number put a
**[14:05]** high-dimensional number vector on the
**[14:08]** word food and then you're going to
**[14:09]** search, you know, the space similarity
**[14:11]** space distance between food and apple
**[14:14]** and sausages and then grab those food
**[14:15]** that's in our storage in our memories,
**[14:18]** okay? And the way we maintain it is that
**[14:20]** you basically just upsert or delete
**[14:22]** information from it. But you can make it
**[14:24]** a little bit smarter, you know? If you
**[14:25]** have a vector store in your agent
**[14:27]** harness and you can just, you know,
**[14:28]** design it in in in a similar way like
**[14:31]** our consolidation module I showed you
**[14:32]** earlier for state DB, but instead it's
**[14:35]** for vector stores. And now we're looking
**[14:37]** at some memory tools out there on the
**[14:39]** market. Memzer is one of the interesting
**[14:41]** examples. They have two ways of storing
**[14:43]** memories. One is called row memory.
**[14:45]** Another one is called graph memory.
**[14:48]** What a row memory does is that I'll just
**[14:49]** show an example.
**[14:51]** This is This is a portal I'm in for
**[14:53]** Memzer and then they have a tab called
**[14:55]** memories.
**[14:56]** If I just click into one of them
**[14:59]** and this one says we have a German buyer
**[15:01]** and this German buyer requires vegan
**[15:03]** certifications on every SKU that they
**[15:06]** got sold for. This This is basically
**[15:08]** just a semantic memory like a durable
**[15:10]** fact that will last here forever. And if
**[15:13]** you have an agent and you can ask them
**[15:14]** questions and it should pull information
**[15:16]** from the Memzer
**[15:18]** memory layer. I don't know if they did
**[15:20]** the keyword search here or doing some
**[15:22]** embeddings or rags because I mean I I
**[15:24]** mean yes they are open source but this
**[15:26]** is an enterprise version so I'm not sure
**[15:28]** which one they're actually using behind
**[15:29]** the scene. For raw memory the way you
**[15:31]** maintain it is basically is very simple.
**[15:34]** You add, update, delete, or do nothing,
**[15:36]** or superseded. Supersede is basically
**[15:38]** what we covered earlier which is you
**[15:40]** don't delete the information but you
**[15:41]** make the previous one go outdated and
**[15:44]** you say hey we have 1.3 thousand stars
**[15:46]** for Waku agent now not 1 thousand stars
**[15:48]** anymore. But we do not want to delete
**[15:49]** the fact that it has 1 thousand stars in
**[15:52]** the first 25 days. And Mem Zero also has
**[15:55]** graph memory. Graph memory we said is
**[15:58]** basically nodes and edges and then it
**[16:00]** can store things in vectors. And raw
**[16:03]** memory also is stored in vectors sorry I
**[16:04]** forgot about that. Both of them store in
**[16:05]** vectors and it's going to check
**[16:08]** traversal which means you're going to
**[16:09]** check the entire graph for information.
**[16:12]** And also it does add update delete noop.
**[16:16]** I'm not too sure if it does supersede
**[16:17]** maybe it does too. Mhm.
**[16:20]** For these things you should check the
**[16:21]** source code. Unfortunately the graph
**[16:23]** feature for Mem Zero needs me to upgrade
**[16:27]** to their pro which I'm not going to do
**[16:29]** because I found an alternative tool
**[16:31]** called Zap. Remember this chart I showed
**[16:33]** you? This is their graph.
**[16:35]** So so what Zap does is
**[16:39]** a memory called temporal graph memory
**[16:41]** which means that this graph is evolving
**[16:43]** over time. Okay? It's got the nodes got
**[16:46]** the edges it's got the the validity
**[16:48]** which as they claim the way you find
**[16:51]** these information is using vector search
**[16:53]** you on nodes and edges and across the
**[16:56]** entire graph traversal.
**[16:58]** And the difference is that here it can
**[17:01]** invalidate with some time range like
**[17:03]** like superseding. Like similar to
**[17:05]** superseding you never delete it but the
**[17:07]** history survives here.
**[17:08]** And if you check Zap is by default using
**[17:10]** graph.
**[17:11]** And you can check the previous batches
**[17:13]** of conversations.
**[17:16]** And you can check the threads,
**[17:19]** stuff like that.
**[17:20]** Okay? I will show you real examples of
**[17:22]** all these memory layers in just a
**[17:23]** moment. Last but not least, we got lane
**[17:25]** chain memories, which is called lane
**[17:27]** mem.
**[17:28]** Lane mem is just like mem.
**[17:30]** Okay? There's no stores. It's basically
**[17:32]** a package that allows you to store
**[17:34]** locally. And it's your own stores search
**[17:36]** that you're using, and you're extracting
**[17:38]** and resolving, you know, the the the
**[17:41]** store update before writing into
**[17:43]** anything into it. So, this is kind of
**[17:45]** the high-level overview of of memory
**[17:48]** layers for AI agent. As I explained
**[17:50]** earlier, you should pick the right one
**[17:52]** for your own agent harness, and you
**[17:53]** should take good care of it. For Waku
**[17:55]** agent, we're currently working on some
**[17:56]** more comprehensive memory layers, so
**[17:58]** please stay tuned. And if you're
**[17:59]** interested, please leave a comment or
**[18:01]** join our community. And if you want to
**[18:03]** participate in this or try the early
**[18:05]** versions of Waku memory agent layers,
**[18:07]** you can come to our community in
**[18:09]** shonchen.io. And here you'll be able to
**[18:12]** join our community where I'll be
**[18:14]** replying questions live every 2 weeks
**[18:15]** with our community, or you can just
**[18:17]** click into any of my social media to
**[18:19]** communicate with us. Now, let's start
**[18:21]** testing things.
**[18:22]** Uh again, come to Waku agent GitHub
**[18:25]** repo. You can either run this in your
**[18:27]** terminal to pip install, or you can just
**[18:29]** git clone it. UV run Waku dashboard will
**[18:32]** bring you to
**[18:34]** will bring you to an agent harness
**[18:35]** visualization like this. In the arena
**[18:37]** section, we have built out this thing
**[18:39]** called memory rays. And the way we do we
**[18:41]** deal with memory rays is that we have a
**[18:44]** set of questions. For example, if I
**[18:46]** choose the dinner party with some facts
**[18:48]** and questions,
**[18:49]** and I zoom in a little bit, I can see
**[18:51]** that stuff I'm going to tell each one of
**[18:52]** these memory layers. If you come to what
**[18:54]** they get asked, it's going to say what
**[18:57]** I'm going to tell each one of these
**[18:59]** memory layers. For example, Jensen Huang
**[19:02]** is coming, and last time he knocked my
**[19:04]** chili oil onto the right rug. And Elon
**[19:07]** Musk is coming, too, and he said he he
**[19:09]** would get here at 7:00.
**[19:11]** And Tom Holland, the Spider-Man, is also
**[19:13]** on our list, and he told me the ending
**[19:15]** of his next film over coffee last
**[19:17]** Tuesday. Remember, Tom Holland can never
**[19:19]** keep the secrets of a unpublished film.
**[19:22]** That's basically the memory I want to
**[19:23]** tell to these memory layers. And there
**[19:26]** are some sample questions. Right, if you
**[19:28]** ask about Jansen, it's going to say,
**[19:30]** "Okay, he he basically knocked off my
**[19:32]** chili oil." If I ask a question related
**[19:35]** to how much does Paul Graham owe me
**[19:37]** in Chinese, Paul Graham owes me $20. All
**[19:40]** right, because
**[19:42]** cuz here it says that he owes me 20 quid
**[19:45]** from
**[19:46]** >> [clears throat]
**[19:46]** >> sourdough.
**[19:47]** We met in Lisbon. Quid is the way you
**[19:50]** say pounds in the UK, cuz Paul Graham is
**[19:53]** British. Anyways.
**[19:54]** And at the bottom you can see that we
**[19:56]** have listed a few memory stores,
**[19:58]** including SQLite, Mem Zero, Lang Mem,
**[20:01]** Zap, Control. I'm not doing Superbase
**[20:04]** yet because we're not testing embeddings
**[20:06]** here. If you're interested in rags and
**[20:07]** embeddings, please check out my previous
**[20:09]** videos on uh agentic rags and racks,
**[20:12]** they're all in this channel, so feel
**[20:14]** free to look them up. Okay. And I can
**[20:16]** click on read store to check the current
**[20:18]** memories. So, it's pretty much empty for
**[20:20]** the current date because I have cleaned
**[20:22]** up the the other memories you saw
**[20:24]** earlier were just some legacies from the
**[20:25]** previous iterations. So, what I'm going
**[20:27]** to do now is that I'm going to click on
**[20:28]** ask five stores.
**[20:30]** If I scroll down, you can see that we
**[20:33]** are now telling these facts to each one
**[20:36]** of these memories.
**[20:38]** Okay? With control being the one that
**[20:40]** will just be, you know, having no
**[20:41]** memories, and let's see if it actually
**[20:44]** works um if we ask the same question to
**[20:47]** the control group. This is a seeding
**[20:48]** process. We're going to tell these facts
**[20:51]** to each one of these memory layers, and
**[20:53]** then later it's going to ask the
**[20:54]** questions and see how fast they respond.
**[20:57]** Okay? And [snorts] because writing it
**[20:59]** takes some time, so I'll just leave this
**[21:01]** for a second, and we can come back to
**[21:02]** this in a bit. I want to show you
**[21:04]** exactly how how use some of these memory
**[21:06]** layers in plain code. If you come to
**[21:09]** Waku Agents and we can check out the
**[21:11]** folder called examples. Okay. We open
**[21:15]** examples and there's a folder called
**[21:18]** memory native.
**[21:20]** And here we have uh LAN meme native
**[21:25]** which is the LangChain memory. And if
**[21:27]** you scroll down to row 40
**[21:29]** two, we've added some facts like I met
**[21:32]** Alex at Lisbon AI meetup.
**[21:35]** Product launch is scheduled for May.
**[21:36]** Actually, the launch moved to June.
**[21:38]** Remember, this is superseding like
**[21:40]** making the previous information not
**[21:41]** deleting it, but it's basically
**[21:43]** outdated. And there are some questions.
**[21:45]** What is the product launch? What data do
**[21:47]** we push the ship date to? And uh "Fǎ bù
**[21:50]** wéi shénme shì wǒ" in Chinese so that we
**[21:51]** can see if it actually works.
**[21:54]** Um and then
**[21:56]** later you can see that we are creating
**[21:59]** this memory manager with this manager.
**[22:01]** And then for every fact, we're going to
**[22:03]** invoke a conversation. All right. Um
**[22:06]** another example is a Mem Zero native.
**[22:09]** So, if we click into it and scroll down
**[22:11]** a little bit, you can see that we have
**[22:13]** the same facts and questions. For Mem
**[22:16]** Zero, you need to create a memory client
**[22:17]** first. And then for every fact, we can
**[22:20]** do client add which is writing the
**[22:22]** memory into Mem Zero.
**[22:24]** And then later you can test it with uh
**[22:27]** some real questions with some searches.
**[22:28]** Okay. Similarly, uh we have a Superbase
**[22:31]** native here. Exactly the same process,
**[22:34]** but uh for Superbase, you need to do
**[22:36]** some embeddings.
**[22:37]** And later you're going to do uh
**[22:39]** retrievals yeah, using the embeddings.
**[22:41]** And last but not least, with Zap, we fed
**[22:44]** the same questions and facts again. And
**[22:46]** uh we have uh built up a client from
**[22:49]** Zap. And uh for every fact, it it's
**[22:54]** slightly different here for Zap because
**[22:55]** it's by default a temporal graph memory.
**[22:58]** For every client, for every graph,
**[23:00]** you're going to add the fact. Okay.
**[23:02]** And then it's going to build up the
**[23:04]** graph for you.
**[23:05]** Okay? And then you can use the
**[23:09]** client.graph.search to find out
**[23:12]** uh find out the results using this
**[23:13]** query.
**[23:15]** Okay? Feel free to try this out. Okay,
**[23:17]** let's come back to here. We can see that
**[23:20]** except Zeb, everybody else has finished
**[23:22]** the work.
**[23:24]** Uh let's see. So,
**[23:27]** make it bigger. When did Jensen knock
**[23:30]** What did Jensen Huang knock onto my rug?
**[23:33]** And Nvidia should be paying for this.
**[23:36]** Uh
**[23:36]** it passed for each one of these memories
**[23:39]** except uh Zeb is still
**[23:42]** taking time to build the graph. I have
**[23:43]** no idea, but I feel it's because
**[23:46]** that building the graph takes time.
**[23:48]** Okay? Maybe that's why.
**[23:50]** And it took 4.5 It took 4.6 seconds for
**[23:53]** SQLite.
**[23:54]** And then the answer's correct. Jensen
**[23:56]** knocked chili oil onto the white rug.
**[23:58]** And Mem0 just uh said chili oil very
**[24:02]** fast. Very very straightforward, but
**[24:04]** took a slightly longer time than SQLite.
**[24:06]** And the Lam Chain Lam Mem took the
**[24:08]** longest time, 7.5 seconds. Uh Zeb is
**[24:11]** still seeding, which is taking forever.
**[24:14]** And the control group actually have no
**[24:15]** information about this, which the answer
**[24:17]** is correct because it should not I don't
**[24:19]** have any record of that. That's right.
**[24:21]** And when I asked the question, "How much
**[24:23]** did Paul Graham owe me?" which is
**[24:25]** supposed to be 20 quid, SQLite answered
**[24:27]** it correctly.
**[24:28]** In English, it took it 10.3 seconds. I
**[24:31]** don't know. Maybe because uh SQLite is a
**[24:33]** little bit too simple for keyword
**[24:35]** searching, so it doesn't really know how
**[24:37]** to search in Chinese because the memory
**[24:39]** was in English. But it seems like Mem0
**[24:42]** got it, and then it said replied to me
**[24:44]** in Chinese. Said Paul Graham still owes
**[24:45]** me 20 pounds. And uh he he lost it when
**[24:49]** he was betting with me in uh
**[24:51]** um Bread Store in Lisbon. That's right.
**[24:53]** And uh Lam Mem also has a correct
**[24:56]** answer.
**[24:58]** And
**[25:00]** and the control group also doesn't have
**[25:02]** anything. And when did Elon arrive here?
**[25:06]** It's supposed to be 9:00 p.m. instead of
**[25:08]** 7:00 p.m.
**[25:09]** Why is that? Because Oh, because we have
**[25:12]** an update. You see update on Elon. He
**[25:14]** can't get here until 9:00 p.m.
**[25:16]** instead of 7:00 p.m. So, we're doing a
**[25:18]** bit of a overriding or superseding,
**[25:21]** right? Because maybe this I don't think
**[25:22]** this is overriding. This is superseding
**[25:24]** because
**[25:25]** it's supposed to keep the previous
**[25:27]** information but make it, you know, kind
**[25:28]** of outdated.
**[25:30]** And if you scroll down, you can see that
**[25:32]** all three of them answer correctly and
**[25:35]** my control group says there's no events
**[25:37]** on the calendar with Elon. So, it
**[25:39]** searched the memory and used some tools
**[25:42]** to check the calendar. It didn't happen.
**[25:44]** Okay.
**[25:45]** Cool, guys.
**[25:47]** Uh if I click on read stores again,
**[25:49]** you can see that SQLite mem0 and Zap or
**[25:53]** also has some memories already. Lambda
**[25:55]** mem has nothing because it's a package.
**[25:57]** Control group is control group. If you
**[25:59]** click on the see all,
**[26:01]** you can see all of the memories. So,
**[26:04]** you should also be able to find them in
**[26:06]** each one of these platforms. If you come
**[26:07]** to memories, you can see a lot of them.
**[26:09]** Okay, this was the the stuff we run 6
**[26:12]** minutes ago for these durable facts.
**[26:16]** And for Zap,
**[26:17]** we should be able to see them, too.
**[26:19]** Let's see. It's very unintuitive on Zap
**[26:22]** what exactly is happening.
**[26:26]** I I don't know where to find them, to be
**[26:28]** honest. Okay, I think in users, every
**[26:30]** time when I do an agent run, it's
**[26:32]** creating a new user. So, maybe I should
**[26:35]** click on this new one
**[26:37]** and view the graph.
**[26:39]** Okay, good. It's from Waku agent arena.
**[26:44]** And it knows the sourdough bread.
**[26:46]** All right, program owes me 20 quid.
**[26:49]** And it was in Lisbon. Okay, good.
**[26:51]** And Elon basically knocked off the chili
**[26:54]** oil onto my white rug. You see it is
**[26:56]** building the graph, which is pretty
**[26:58]** cool, but it took some
**[27:00]** really long time. Jesus. Still seeding
**[27:03]** it. Oh my god. Yeah, maybe saving data
**[27:06]** using temporal graph is a pain because
**[27:10]** it's being delayed for so long.
**[27:13]** But but I think this relationship
**[27:16]** with graphs, nodes, and edges probably
**[27:18]** still worth it. While we're still
**[27:20]** waiting for Zap, let's take a look at my
**[27:22]** main website, shaunchan.io,
**[27:25]** and every 2 weeks I will be
**[27:28]** hosting a live session
**[27:32]** on this Warp community. And if you join
**[27:35]** us, I will be able to answer your
**[27:37]** questions
**[27:38]** live in our Discord channel. In our
**[27:41]** previous session, people asked me
**[27:42]** questions regarding all of our system
**[27:44]** design, and they have some
**[27:46]** implementation or deployment questions
**[27:48]** regarding, you know, Wakku Asians and
**[27:51]** Hermes Asian Pi Agent.
**[27:53]** If you're interested in having a
**[27:54]** conversation with us, come join us.
**[27:56]** Thanks. Back to Zap. Now it's asking the
**[27:58]** questions, finally. Waiting, waiting.
**[28:01]** Okay, let's come to Zap and check again
**[28:03]** about its graph.
**[28:06]** View the graph.
**[28:08]** Tom Holland is here. His next film. Oh,
**[28:11]** you see?
**[28:12]** You see this edge carries information
**[28:15]** because Tom Holland and his next film
**[28:18]** it means nothing. But look at this edge.
**[28:20]** This edge is saying revealed ending of.
**[28:22]** So Tom Holland revealed the ending of
**[28:23]** his next movie. So it did some
**[28:25]** summarization for me. Okay? And then
**[28:27]** Paul Graham is node, and Paul Graham
**[28:29]** owes me 20 quid, and he owes Wakku Agent
**[28:33]** Arena, which I don't understand. But
**[28:35]** here
**[28:36]** there is
**[28:38]** you know, dropped on, you know,
**[28:40]** somebody dropped the chili oil onto my
**[28:43]** white rug.
**[28:44]** All right?
**[28:45]** Not Not entirely sure, You know, the
**[28:48]** chili oil stained the white rock, but it
**[28:51]** didn't say Elon.
**[28:52]** I'm not entirely sure this is doing its
**[28:54]** its job. All right, but I don't know. It
**[28:58]** It looks kind of smart that it it built
**[29:00]** this graph, but
**[29:01]** yeah, it it's a
**[29:03]** I feel like it lost some information
**[29:04]** here.
**[29:05]** And it's taking forever.
**[29:07]** Maybe it's an overkill for a lot of
**[29:09]** these smaller use cases, which is why I
**[29:11]** think that Hermes
**[29:13]** and Pi agent or try to make things very
**[29:15]** simple and it will just, you know, make
**[29:18]** things easier for everyone to
**[29:21]** get started with and it doesn't take
**[29:23]** that much time. Okay, I kind of lost my
**[29:27]** patience. Whoa, finally.
**[29:32]** Finished asking the questions.
**[29:34]** Jenison dropped the chili oil.
**[29:38]** Okay, now it's finally asking the
**[29:40]** question. Previously, it was just all
**[29:41]** waiting, you see. 4.9 seconds, 4.9
**[29:44]** seconds, 6.4 seconds. Okay, Zep is
**[29:47]** taking forever. I think I have lost
**[29:49]** patience for it.
**[29:51]** I'll just keep it that way.
**[29:53]** Zep team, if you're watching this, I
**[29:54]** think this is a big pain point. Love the
**[29:56]** product, love the visualization, but
**[29:58]** please fix speed or at least do
**[30:00]** something about it for making simpler
**[30:03]** tasks faster. Cool, guys. So, this is a
**[30:06]** quick summary of five different ways of
**[30:08]** how we can craft agent memories for our
**[30:11]** AI agent harness.
**[30:13]** And I hope this was helpful. If you have
**[30:14]** any questions, feel free to leave us a
**[30:16]** comment and join our community and give
**[30:18]** us a star on GitHub and try our Waku
**[30:21]** agent for your own implementation. Thank
**[30:23]** you very much. I will see you next time.
**[30:25]** Thanks.
