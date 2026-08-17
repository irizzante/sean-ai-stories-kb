# You Can Learn AI Agent Memory System In 12 Min | Semantic & Episodic Memory, RAG, Vector Database

youtube_id: mY3bR9qjZr4
published: 2026-06-19

**[00:00]** Hey everyone, this is Shawn. So, today I
**[00:01]** want to explain to you what an AI agent
**[00:03]** memory system looks like, and it's very
**[00:05]** important to understand how memory works
**[00:07]** these days. Because if you have been
**[00:08]** using tools like ChatGPT or Claude, or
**[00:10]** code, you're probably already using a
**[00:12]** memory system without even realizing it.
**[00:14]** For example, when you ask your AI tool
**[00:16]** about who you are and the question that
**[00:18]** you asked them for the past week, they
**[00:20]** all know what's going on. And if you're
**[00:21]** an AI builder or startup founder,
**[00:23]** sometimes they even remember what your
**[00:24]** company is without you needing to
**[00:26]** explain it. So, in this video I want to
**[00:27]** explain to you the essential part of how
**[00:29]** does this exactly work? And I'm going to
**[00:31]** walk you through this system design you
**[00:33]** can see on the screen step-by-step, so
**[00:35]** that you will understand what matters in
**[00:37]** this kind of system design, and also
**[00:39]** what will help you for efficient token
**[00:41]** usage in a memory system for AI agents.
**[00:44]** Let's get started. So, when we talk to
**[00:46]** ChatGPT or Claude or anything, the first
**[00:48]** thing you're going to do is going to
**[00:49]** you're going to ask a question, which in
**[00:51]** our language is called a user prompt,
**[00:53]** okay? A prompt is basically something
**[00:54]** that you send to to a chatbot and be
**[00:56]** like, "Hey, what's the weather like
**[00:57]** today? How do I build an app? How do I
**[00:59]** understand Einstein's theory?" So, we
**[01:01]** might think that we're asking the
**[01:02]** question to this pink bubble, which is
**[01:04]** an LLM, which is a Q&A agent, which
**[01:06]** allows you to ask questions and answer
**[01:07]** your questions, and then you will get a
**[01:09]** reply. In between that, there's some
**[01:11]** more steps that's happening before that,
**[01:13]** okay? So, this question will firstly
**[01:15]** flow into this thing called a working
**[01:17]** memory or a context RAM. What does that
**[01:20]** mean? It means that instead of asking a
**[01:21]** simple question such as, "What does my
**[01:23]** company do?" in which case the large
**[01:25]** language model might not even remember
**[01:26]** or don't even know, it needs to have a
**[01:28]** working memory that either includes some
**[01:30]** information from the internet or from
**[01:33]** the current context itself or from some
**[01:35]** databases that you would that you stored
**[01:37]** such information previously. And then
**[01:39]** this working memory also needs to be fed
**[01:41]** with something called a current chat
**[01:43]** history and a system prompt. The chat
**[01:45]** history is basically everything you have
**[01:46]** talked about in a in a conversation with
**[01:48]** AI, okay? That's easy to understand. For
**[01:50]** system prompt is basically a role-play.
**[01:52]** For example, if you want AI to be able
**[01:54]** to respond to you like Elon Musk, then
**[01:56]** you need to put in the system prompt
**[01:58]** that, "Hey, you're Elon Musk. You must
**[02:00]** talk to me like Elon Musk." So, the user
**[02:02]** question, the user prompt, the current
**[02:04]** chat history, and the system prompt are
**[02:07]** the basic components that will be fed
**[02:09]** into this working memory or the current
**[02:11]** context so that your Q&A agent will be
**[02:14]** able to understand, "Okay, here's the
**[02:16]** entire context. I'm going to process
**[02:18]** these information before I send this
**[02:19]** user a reply." But, what if we need more
**[02:22]** than just the current chat history?
**[02:24]** Okay, what if we need something else?
**[02:25]** Let's say you're setting up an agent to
**[02:27]** allow your customers to talk to you and
**[02:29]** ask any questions about your products,
**[02:31]** about the deal that you're talking
**[02:32]** about. The customer might might be
**[02:34]** asking you something related to the
**[02:35]** quality of your products, related to
**[02:36]** your previous conversations, a follow-up
**[02:39]** question, these kind of things. All
**[02:40]** right, and the current chat history is
**[02:42]** all the history that happened in that
**[02:44]** e-commerce app. And the system prompt is
**[02:46]** probably like, "Oh, you are a bot that
**[02:49]** will take care of all of my customers on
**[02:51]** this e-commerce site." And the
**[02:52]** conversation happening here is called an
**[02:55]** AI agent session. And this session is
**[02:57]** ephemeral, which means that nothing here
**[03:00]** will get saved unless you manually save
**[03:02]** them in a database cuz there's no
**[03:03]** database here yet. We're literally just
**[03:05]** making an LLM call right here. Well, you
**[03:07]** could argue that the current chat
**[03:08]** history has a bit of memory, but that's
**[03:10]** just happening in this current
**[03:12]** conversation. This current session does
**[03:13]** not know anything about your product
**[03:15]** stocks, about you know, your previous
**[03:18]** purchase history, your customers' taste,
**[03:21]** um anything you have argued about, any
**[03:23]** complaints in the past, these kind of
**[03:24]** things. Okay. That's why we need to
**[03:26]** build up on this working memory and give
**[03:28]** it more rich information and make it
**[03:30]** efficient as well. So, there are three
**[03:31]** main pillars that will make this working
**[03:33]** memory more complete. And they are
**[03:35]** procedural memory, semantic memory, and
**[03:38]** episodic memory. I'll explain them one
**[03:39]** by one. A procedural memory is basically
**[03:42]** how the agent should be behaving. It's
**[03:44]** usually related to how they should act.
**[03:46]** And also, if you're familiar, uh you
**[03:48]** could write some skills to teach agent
**[03:50]** to do some repeated tasks. For example,
**[03:52]** it could be something like if you
**[03:53]** realize that the customer is really
**[03:54]** angry, you should answer them politely
**[03:57]** and always apologize. This is a skill
**[03:59]** that your agent should learn and there's
**[04:01]** no memory about this thing, right? You
**[04:03]** can think of this as like a habit you
**[04:04]** want to teach to your employee to behave
**[04:06]** in a certain way or teach your kids,
**[04:08]** right? To behave in a certain way. And
**[04:10]** it's just a procedure, right? This is
**[04:12]** how you react when such a situation
**[04:14]** happens. And they are usually saved in
**[04:16]** files or text and you know, for skills
**[04:20]** can save them as a markdown file. All
**[04:21]** right? So, I'm going to connect this to
**[04:23]** the working memory and this is usually
**[04:27]** inputted as a skill.md markdown file.
**[04:30]** Okay? And semantic memory and episodic
**[04:32]** memory are slightly different. They're
**[04:34]** actually saved not in files but we would
**[04:36]** call vector stores. And these vector
**[04:38]** stores will feed information into this
**[04:40]** memory that will be plugged in to the
**[04:42]** working memory. Let's dive a little bit
**[04:43]** deeper into what these memories actually
**[04:45]** mean, okay? So, for semantic memory,
**[04:47]** it's basically saving things like
**[04:49]** durable facts or user profile. Let's say
**[04:52]** I start a new store online today and if
**[04:54]** I just ask ChatGPT who what my products
**[04:56]** are, ChatGPT will have no idea who you
**[04:57]** are. Well, if they do have some idea of
**[04:59]** who you are, say you if you're Walmart,
**[05:01]** then that means you're already famous,
**[05:02]** okay? Then their models has already
**[05:04]** trained on you or they can search on the
**[05:06]** internet to find about you, all right?
**[05:08]** But in your case, because the
**[05:09]** foundational large language model does
**[05:11]** not know who you are, you need to save
**[05:13]** some durable facts or the profile of
**[05:16]** your company or about yourself in a
**[05:18]** database so that when one of your
**[05:20]** customers is asking a question about a
**[05:22]** certain product, your agent will be able
**[05:24]** to understand where to fetch that
**[05:26]** information. And this is a process we
**[05:28]** call RAG, which is retrieval augmented
**[05:31]** generation. And normally it uses a top
**[05:33]** case search method. I have a dedicated
**[05:35]** video about retrieval augmented
**[05:36]** generation on my channel, feel free to
**[05:38]** watch them. But basically RAG is
**[05:40]** something that will allow the AI agent
**[05:43]** to have access to and also be able to
**[05:45]** select and fetch the most relevant
**[05:48]** information related to your questions,
**[05:50]** okay? Why is selectively fetching so
**[05:52]** important? It's because if you run a
**[05:54]** company for 10 years, let's say, your
**[05:56]** database could be really huge. You could
**[05:58]** have like gigantic amount of images or
**[06:00]** text or documentations about a company.
**[06:03]** You don't want to feed the whole thing
**[06:04]** into the LLM because firstly, that would
**[06:07]** be very expensive, and secondly, that's
**[06:09]** probably not feasible, okay? These days,
**[06:11]** I think the context window for most LLMs
**[06:13]** is roughly 1 million tokens. Right? If
**[06:15]** you go beyond that, good luck with that,
**[06:17]** but you don't want to overload your LLMs
**[06:18]** because that also makes things much
**[06:20]** slower and not accurate anymore. So, you
**[06:22]** want something to smartly fetch
**[06:24]** information for you, and this method is
**[06:26]** called RAG. You can watch my previous
**[06:27]** video to understand a bit better about
**[06:28]** what RAG means. But here is basically
**[06:30]** just helping you to fetch the static and
**[06:33]** durable facts about your company, what
**[06:34]** products you're selling, who you are,
**[06:37]** what kind of branding you have, what
**[06:38]** kind of ways do you put yourself out
**[06:40]** there in front of customers, okay? These
**[06:42]** things don't change normally. Or the
**[06:43]** facts could be like, oh, who this
**[06:45]** customer is, like if they message me
**[06:47]** very often, I want to remember who they
**[06:48]** are, right? Otherwise, it sounds like
**[06:50]** you don't really care about your
**[06:51]** customers. I'm going to explain how
**[06:52]** we're going to make semantic memory to
**[06:53]** also remember your customer side as well
**[06:56]** in a bit, okay? And then we're covering
**[06:58]** the episodic memory, which is also
**[07:00]** stored in a vector store. Again, a
**[07:02]** vector store is a embedded list of
**[07:06]** arrays or numbers that is representing
**[07:08]** all the text cuz remember, computers
**[07:10]** cannot process text or documents. It can
**[07:12]** only process numbers. So, how how AI is
**[07:15]** understanding our world is basically
**[07:17]** it's turning every single word into a
**[07:19]** list of numbers, and then it's going to
**[07:20]** do some similarity search, which is
**[07:22]** basically RAG. RAG, again, it's doing
**[07:25]** the top K search, and if K is five, then
**[07:27]** it's looking for the top five most
**[07:29]** relevant pieces of information from the
**[07:31]** vector store to feed into answering this
**[07:34]** question from the user. But the main
**[07:36]** difference between an episodic memory
**[07:38]** and a semantic memory is that the
**[07:40]** episodic memory is recording the dated
**[07:44]** events or activities that happened. It's
**[07:46]** like a timeline with like everything
**[07:48]** that happened has a time on it or it's
**[07:50]** just a past chat history. Remember we
**[07:52]** mentioned that in this box, this AI
**[07:54]** agent session, everything is going to be
**[07:57]** gone after the conversation is is gone,
**[07:59]** right? So So we're going to save this
**[08:01]** conversation, the current chat history,
**[08:04]** into the episodic memory
**[08:06]** later so that it has the entire record
**[08:10]** of the previous conversations related to
**[08:13]** this agent activities with their users.
**[08:15]** Well, the examples here for selling
**[08:17]** items online could be that, you know,
**[08:19]** you're you're storing like who's
**[08:20]** purchasing what items on what day and
**[08:22]** then and when was the item delivered
**[08:25]** and when was the last time somebody
**[08:26]** filed a complaint for your service,
**[08:29]** something like that, okay? So we're
**[08:30]** going to need to add an arrow here to
**[08:32]** link the reply to this database and this
**[08:35]** is basically saving
**[08:37]** the messages or actually
**[08:40]** activities as well, okay? So that this
**[08:43]** episodic memory is constantly being
**[08:45]** updated. It's basically a log of all
**[08:48]** previous history. So here's the fun
**[08:49]** part. If you have been using ChatGPT or
**[08:52]** Claude and you use their memories, you
**[08:54]** will realize that sometimes you can edit
**[08:56]** the memories for yourself and you
**[08:58]** realize that the memories are not very
**[08:59]** long, but then they're constantly being
**[09:00]** like updated. For example, it remembers
**[09:03]** that I'm building a company that is
**[09:05]** working on certain type of problem. I
**[09:07]** don't need to explain anything, but
**[09:08]** sometimes we do a small pivot and we
**[09:10]** talked about it in the in our
**[09:11]** conversations and then the memory just
**[09:13]** remembered that, okay? For an efficient
**[09:15]** agent memory system to work, you don't
**[09:17]** want the AI agent to always search these
**[09:19]** kind of information from an episodic
**[09:21]** memory because that's just a huge
**[09:23]** database about everything that happened
**[09:25]** in the past. You want some kind of
**[09:27]** durable summarized facts that you think
**[09:30]** is uh very important for AI to know,
**[09:32]** okay? So that's why ChatGPT and Claude
**[09:34]** and all these AI agents are all doing
**[09:36]** something similar, which is that it's
**[09:38]** summarizing at a certain frequency,
**[09:40]** which is not too frequent, of all of
**[09:41]** these
**[09:42]** activities that happened into the
**[09:44]** semantic memory, so that the facts about
**[09:48]** you, about your company, about
**[09:50]** everything is condensed and saved
**[09:54]** properly for future retrievals, okay?
**[09:58]** And this is actually very smart because
**[09:59]** it not only saved a lot of token usage
**[10:02]** every single time, and also it's making
**[10:04]** your tools much faster. But let's pause
**[10:06]** here for 1 second.
**[10:08]** If we summarize every single bit of new
**[10:11]** activities into the semantic memory,
**[10:13]** then that sounds like we're just saving
**[10:15]** the information twice. What's the point
**[10:16]** of having a durable facts anyways? And
**[10:19]** that brings us into this concept of a
**[10:21]** gate, which is we only consolidate after
**[10:24]** a certain number of chats. It could be
**[10:26]** 20 conversations, it could be, you know,
**[10:28]** 100 activities, could be anything, okay?
**[10:31]** So, in order for these system to work
**[10:33]** together, we need a system that will,
**[10:37]** you know, do some consolidation after
**[10:39]** certain number messages, and then we
**[10:42]** feed that into the summarizer agent.
**[10:45]** And then the summarizer agent will then
**[10:48]** summarize the information into the
**[10:50]** semantic memory, and we call this the
**[10:52]** steel
**[10:54]** into facts. So, congratulations, this is
**[10:57]** pretty much it. You have built up an
**[10:59]** entire memory system that is, in my
**[11:01]** opinion, quite modern in these days
**[11:03]** context, and it should be embedded in
**[11:07]** any AI applications that we're building
**[11:08]** these days, because it's so easy for
**[11:11]** users to engage with an AI agent, and
**[11:13]** it's so easy to build software.
**[11:15]** But then what happens is that the
**[11:17]** database is just exploding if you're
**[11:18]** recording all these activities. So, we
**[11:20]** need to figure out a way to very
**[11:22]** efficiently not only record the data,
**[11:25]** but also, you know, summarizing the
**[11:27]** data, and then turn them into sort of
**[11:29]** some core memory, which is semantic, and
**[11:32]** then some episodic memory, which is um
**[11:34]** just a timeline of list of things. And
**[11:36]** at the same time, you can define the
**[11:38]** best practices of how the agent should
**[11:40]** behave in a certain task, okay? Which is
**[11:43]** what skills is about. I also made a
**[11:45]** video about agent skills, agent teams in
**[11:47]** the past, feel free to check them out.
**[11:48]** But overall, I believe this is a very
**[11:50]** complete way to understand what an AI
**[11:53]** agent system should be performing with a
**[11:55]** memory that will be added as a context
**[11:58]** layer on top of the entire interaction.
**[12:00]** I hope you enjoy this. Let me know if
**[12:01]** you have any questions, and I'll see you
**[12:03]** next time. Thanks.
