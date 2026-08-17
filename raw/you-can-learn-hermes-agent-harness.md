# You Can Learn Hermes Agent Harness In 20 Min | Loop Engineering, Memory System, Self-Improving AI

youtube_id: LqG1q5NpOBE
published: 2026-07-05

**[00:00]** Have one of the shine. So, today we're
**[00:01]** going to walk through Hermes Asian
**[00:03]** harness and its loop engineering system.
**[00:05]** This is one of the most popular harness
**[00:07]** agent system right now and it's an open
**[00:08]** source project. If you check the GitHub,
**[00:10]** they've got more than 200,000 stars in a
**[00:13]** very short period of time. So, it's
**[00:14]** basically a self-improving AI agent
**[00:16]** built by this research lab called neural
**[00:18]** research and it's a built-in learning
**[00:20]** loop. It creates its own skills from
**[00:21]** experience instead of you telling the AI
**[00:24]** like claw code to make skills and then
**[00:26]** it also improves over time when you keep
**[00:27]** using it because it persistently stores
**[00:30]** knowledge in your local machine like a
**[00:31]** MacBook. But anyways, this is all the
**[00:33]** buzzwords. We're going to jump into this
**[00:35]** Hermes agent system design like usual.
**[00:37]** We're going to test it as well using
**[00:38]** their desktop app. Just give you a quick
**[00:40]** example. It's like a claw code, right?
**[00:42]** You can see that it was thinking and
**[00:43]** then it answered me in like a Pikachu
**[00:45]** style. It said, "Pikapi, just hang out
**[00:47]** in the my directory because it's
**[00:48]** literally a bot living in my local
**[00:50]** machine files. What are you building
**[00:51]** fixing today? Pikapika." And also, you
**[00:53]** can interact with it on WhatsApp and
**[00:55]** then you say, "Good morning."
**[00:57]** It's a little bit slow. I'm using a
**[00:59]** Gemini 1.5 model for this. It took like
**[01:02]** a good 5 seconds. And now it's basically
**[01:04]** just using WhatsApp as the gateway to
**[01:06]** receive information from my WhatsApp
**[01:08]** account so I can just text it and then
**[01:10]** ask it to do things for me. And say,
**[01:11]** "Pikapi, good morning." You probably
**[01:12]** realize that I've changed his
**[01:14]** personality a little bit and there are
**[01:15]** more interesting things I can show you.
**[01:17]** For those who have watched my previous
**[01:18]** agent harness loop engineering and
**[01:19]** memory system, you might realize that
**[01:21]** this chart is somewhat similar. This is
**[01:23]** what the previous chart looks like. And
**[01:25]** now if we look at harness or Hermes
**[01:27]** agent again, I added a bit more
**[01:28]** information, especially the difference
**[01:29]** between the Hermes harness versus a
**[01:32]** generic harness system. I marked the
**[01:34]** differences in red. But we're going to
**[01:36]** walk through this step by step. Also, I
**[01:37]** prepared some testing examples to cover
**[01:39]** harness, memory, skills, loop, gateway,
**[01:43]** and LM ops or eval because a lot of
**[01:45]** people were asking me if I could
**[01:46]** implement some real examples. So, here
**[01:48]** we are. Without further ado, let's jump
**[01:49]** right in. Okay. So, firstly, let's look
**[01:51]** at the foundation of Hermes harness
**[01:53]** agent. It's a harness that runs on your
**[01:55]** local machine. You can use either local
**[01:57]** command lines, Docker, SSH, or a virtual
**[02:00]** VPS. There are two main ways to interact
**[02:02]** with Hermes agent. One is using your
**[02:04]** favorite communication apps, and in my
**[02:06]** case, I used WhatsApp, or you can just
**[02:08]** use your desktop app with the Hermes
**[02:09]** agent. So, you can come to Hermes
**[02:11]** official website,
**[02:12]** hermes-agent.newresearch.com,
**[02:14]** and just click on download for Mac OS,
**[02:17]** or you can click on Windows over here to
**[02:18]** use the command line to install it.
**[02:20]** Essentially, it's still a chatbot, just
**[02:21]** like Clawcode, and then you ask the
**[02:22]** question to either the communication app
**[02:25]** or the desktop version. It's very
**[02:26]** similar to open claw, where you can use
**[02:28]** WhatsApp to control it. So, after user
**[02:30]** sends the prompt, the user prompt with
**[02:32]** the current chat history and the system
**[02:34]** prompt will be fed into working memory,
**[02:36]** and then this LLM agent is basically the
**[02:38]** Hermes agent that will be answering your
**[02:39]** question. And it will be using a loop
**[02:42]** engine over here to call up some tools
**[02:44]** that are only on Hermes. And eventually,
**[02:46]** after finishing the task, it's going to
**[02:48]** end the loop and then send the user a
**[02:50]** reply. Just literally sending a question
**[02:52]** throughout this entire ephemeral agent
**[02:53]** run, and then get the user reply, just
**[02:55]** like my Hermes was greeting me like a
**[02:57]** Pikachu. And by the way, how did this
**[02:58]** happen? Right, I'll show you right now.
**[03:00]** So, the system prompt for Hermes is
**[03:01]** interesting. It's called soul.md. I
**[03:04]** really like how they name it. It says
**[03:06]** soul. If you come to the right-hand
**[03:08]** side, you can see there's a little file
**[03:09]** bar, and this is your local files, and
**[03:12]** you can go find out there's a dot Hermes
**[03:14]** folder, and we open that, and we scroll
**[03:17]** down,
**[03:19]** you will see there's a file called
**[03:20]** soul.md. Double click on that,
**[03:23]** and you can edit this yourself, right?
**[03:25]** But since I've already edited it, after
**[03:26]** you edit anything, you can just click on
**[03:28]** save. I basically said you talk like
**[03:30]** Pikachu. Every reply starts and with
**[03:32]** pika pika pika p. If you are excited,
**[03:34]** say pika p with the lightning. If you're
**[03:35]** sad, say it quiet pika. I'm pretty sure
**[03:37]** you can do something similar in Clawcode
**[03:39]** for this. In Clawcode, something similar
**[03:41]** would be in customize,
**[03:43]** general, and you can see there's an
**[03:45]** instruction for Claude. You can tell
**[03:47]** Claude to do certain things and not to
**[03:49]** do some things. It's basically the
**[03:50]** system prompt used across the entire
**[03:52]** agent harness. If you didn't watch my
**[03:54]** previous video on harness and loop
**[03:55]** engineering, harness is basically a set
**[03:57]** of tools that allows you to control over
**[04:00]** this really powerful horse, which is the
**[04:02]** LLM itself. In our case, the LLM we're
**[04:04]** using is Gemini because I've got the
**[04:06]** Google credits. I don't want to burn my
**[04:08]** Anthropic credits, but feel free to use
**[04:09]** Anthropic. This is the This is the agent
**[04:12]** of the the horse, and the harness is
**[04:14]** this entire thing. It's like a horse
**[04:16]** harness that you ride on, and you make
**[04:18]** sure that the horse is not going
**[04:19]** anywhere random and it's using the tools
**[04:22]** accordingly to move in the right
**[04:23]** direction. Harness is a very vague
**[04:25]** concept. Just don't fantasize it. It's
**[04:26]** nothing complicated. It's just a
**[04:28]** buzzword. Now, we're going to continue
**[04:29]** to build up this harness right here for
**[04:31]** Hermes, but what I'm going to show you
**[04:32]** is what a loop is. The concept of loop
**[04:35]** got really popular because these days
**[04:37]** people build a lot of agents. You don't
**[04:38]** want to always tell the agent what to
**[04:40]** do. You want the agent to figure out
**[04:41]** what kind of prompt it should send, what
**[04:42]** kind of tools it should call. Let's take
**[04:44]** a look at what tools Hermes agent
**[04:46]** actually have to enable this loop
**[04:48]** engineering. We're going to cover this
**[04:50]** briefly, and then I'll show you real
**[04:51]** examples. So, first of all, the agent of
**[04:53]** Hermes is having a set of tools that
**[04:56]** include the terminal, the browser. Okay,
**[04:59]** you can use your laptop's terminal. You
**[05:01]** can start browser. It can delegate task,
**[05:04]** which means that it can spawn up some
**[05:06]** sub agents for you. For example, you can
**[05:08]** ask it to spawn up an agent which will
**[05:09]** call your claw code CLI to write code
**[05:12]** for you. If the task is basically fixing
**[05:14]** some bugs on my GitHub. And then it can
**[05:16]** schedule cron job. A cron job is
**[05:18]** basically it can schedule something that
**[05:19]** will happen at certain time. You don't
**[05:21]** need human intervention to do it. For
**[05:22]** cron job, let's just try right now. In
**[05:24]** Hermes agent, I can say, "Help me set up
**[05:26]** a cron job that will tell me a Pokémon
**[05:28]** joke every minute in the next 10
**[05:29]** minutes." Okay, I'm just going to send
**[05:31]** this.
**[05:32]** And also, I'm going to send this to our
**[05:34]** Hermes agent WhatsApp interface, too.
**[05:37]** Instead, I'll just say, "Tell me a
**[05:38]** developer joke every
**[05:40]** It just quickly called this a cron job,
**[05:43]** and it says repeats 10 times for the
**[05:45]** next 10 minutes. Because it says it's a
**[05:47]** thing in the terminal UI, it won't be
**[05:48]** able to print it. So, I need to ask it.
**[05:50]** I just ask like, "What's the first
**[05:53]** joke?" And you can see on WhatsApp it
**[05:55]** also got scheduled. The Chrome it says
**[05:57]** the joke machine is powered and
**[05:58]** scheduled. Uh I've set up a cron job to
**[06:01]** send you a fresher joke every minute in
**[06:03]** the next 10 minutes. You should receive
**[06:04]** the first one in about a minute.
**[06:06]** We'll see about that. Okay.
**[06:07]** Uh why did the Squirtle cross the ocean?
**[06:10]** To get the other tide. Pika pika. Okay,
**[06:12]** so that was cron job. It can do skill
**[06:14]** management as well. It can connect to
**[06:15]** MCPs as well. It depends on the question
**[06:17]** that the user asks. The agent will just
**[06:19]** leverage these tools until it's done and
**[06:22]** then it will send a reply to you. Okay.
**[06:24]** The example we just saw was cron job.
**[06:26]** I'm going to show you some more examples
**[06:27]** later, too. Let's test a few harness and
**[06:29]** loop examples. The first one is use a
**[06:32]** terminal tool to find out what OS
**[06:34]** version I'm on and read the last 10
**[06:35]** lines of my shell history. Let's do
**[06:37]** that. Let's start a new session.
**[06:39]** I'm just going to ask this exact
**[06:40]** question to it. So, you can see it ran
**[06:42]** this on my local machine and then it
**[06:45]** figured out that I'm on Mac OS 26.5.
**[06:48]** And the last 10 lines I used in shell
**[06:50]** history is basically text uh get status
**[06:52]** get status get status. I always like to
**[06:54]** check get status. And here what happened
**[06:56]** was that it ran through this agent run
**[06:58]** and then it called the terminal to do
**[07:01]** the task for me. Which is checking what
**[07:04]** system I'm on. This is a very simple
**[07:06]** example, but you can do more crazy
**[07:07]** things. You can ask it to use the local
**[07:09]** machine terminal to do things for you.
**[07:11]** If you're using Clockwork, you're you're
**[07:12]** very familiar with this already, all
**[07:13]** right? There's nothing special about it.
**[07:14]** I'm just showing you the example that
**[07:16]** this is a harness and there's a loop
**[07:17]** because after I fetched it, it will stop
**[07:20]** and tell me and reply to me. Let's look
**[07:21]** at the cron job as well. You can see
**[07:23]** that it sent me two jokes already.
**[07:25]** Why do Java developers wear glasses?
**[07:27]** Because they don't C#. Pika pika. I
**[07:31]** would tell you a UDP joke, but I have
**[07:33]** absolutely no guarantee that you would
**[07:35]** get it. I'm not going to wait for
**[07:36]** acknowledgement anyways. Pika.
**[07:39]** Okay, this one I didn't get it. So, one
**[07:41]** more example. browse to YouTube channel
**[07:43]** Shawn's AI stories, title plus views my
**[07:45]** last videos, create new video titles for
**[07:48]** this current video I am filming. So,
**[07:51]** here we're we're asking it to use the
**[07:52]** browser basically. Okay, you can see
**[07:54]** that it started doing the searching. All
**[07:56]** these things already exist on Clockcode.
**[07:58]** I'm just explaining it from a system
**[07:59]** design perspective and showing you
**[08:00]** examples, okay? And then also, I will
**[08:02]** show you what's the difference between
**[08:04]** Hermes and Clockcode. So, please bear
**[08:06]** with me. All right, so I need to run a
**[08:08]** Python script. can see it also used some
**[08:11]** of the clicking tools. Oh, there's an
**[08:12]** error. The website was wrong.
**[08:15]** Try this new one.
**[08:18]** It saved a little memory here, okay? It
**[08:21]** said the user profile updated. This is
**[08:24]** something I'm going to cover in a bit,
**[08:26]** but spoiler alert, Hermes agent will
**[08:28]** save agent memories by itself. It's
**[08:30]** basically in your local files, too. If
**[08:32]** you come here, within the Hermes folder,
**[08:35]** if you scroll down, in memories, you can
**[08:37]** see there's a memory.md. If we double
**[08:39]** click on that, it stored YouTube here,
**[08:42]** each of scraping quirk. So, because it
**[08:43]** realized that it had a mistake, so it
**[08:46]** updated itself with a memory. This is a
**[08:48]** self-iterating process of this harness.
**[08:50]** Good, so it read my previous YouTube
**[08:52]** titles. It realized that I've got this
**[08:54]** video that's got 100,000 views, and
**[08:56]** since I'm filming a new video now, it
**[08:58]** gave me some new titles. So, what
**[08:59]** happened here was the user, which is me,
**[09:01]** who asked the question through the
**[09:03]** desktop, and then it went through this
**[09:05]** agent run, and then this agent harness
**[09:08]** Gemini that I'm using was basically used
**[09:10]** calling the browser right here to search
**[09:13]** up my YouTube channel. And then it came
**[09:15]** back and said, "Hey, it didn't find
**[09:16]** anything." So, uh it basically stopped.
**[09:19]** There's an end loop guardrail. The
**[09:21]** guardrail stopped and said, "It didn't
**[09:22]** find anything." So, I realized that,
**[09:24]** okay, the previous URL was wrong, so I
**[09:26]** input it again.
**[09:27]** Uh it called the browser again, and it
**[09:29]** also called the terminal to run some
**[09:30]** Python script, and because it needed to
**[09:33]** do some task, and eventually it came
**[09:35]** back with the answer. There's a
**[09:36]** mechanism that says, "Okay, end the
**[09:38]** loop, no more tool calls, and send the
**[09:40]** answer." These are two quick examples of
**[09:42]** what a hard is loop engineering is. You
**[09:43]** see, you're already using it every
**[09:45]** single day. It's nothing fancy. So,
**[09:46]** don't get overwhelmed next time when you
**[09:47]** hear these terms. It's just a buzzword.
**[09:49]** So, what happened just now was this
**[09:51]** memory.md that we saw regarding YouTube
**[09:54]** memory, Hermes agent after or during the
**[09:57]** agent run is going to start to create
**[09:59]** its own skill.md and memory.md depending
**[10:03]** on if it's feeding into the procedure
**[10:05]** memory or if it's feeding into the
**[10:07]** semantic memory. We should add one more
**[10:09]** arrow here, basically. So, essentially,
**[10:11]** the way that Hermes agent works is that
**[10:14]** it's storing its own skills and memories
**[10:16]** completely locally. Nothing's stored in
**[10:18]** the cloud. It has its own self-improving
**[10:19]** loop. Every time when it realized that
**[10:21]** something is a mistake that it should
**[10:23]** learn from or it's a repeated task, it
**[10:25]** will start to summarize, "Okay, here's
**[10:27]** some new memories I should know for the
**[10:29]** future in order to serve this user
**[10:32]** well." It started to save these files
**[10:34]** into these two chunks of memory system.
**[10:37]** First one is called procedure memory.
**[10:38]** It's basically how you act, how the
**[10:40]** Hermes agent should be acting, and it's
**[10:42]** usually saved in this directory called
**[10:44]** Hermes skills skill.md. Hermes skills
**[10:48]** and any of these, okay? Autonomous AI
**[10:51]** agent, claw code, there's a skill for
**[10:53]** how Hermes will use claw code here. So,
**[10:55]** it will basically delegate any coding to
**[10:57]** claw code CLI. Shows you exactly how you
**[10:59]** should do it, like install Claude, run
**[11:02]** it, and do the authentication and all
**[11:04]** these kind of things. And what we just
**[11:06]** saw earlier was memories. Memory.md is
**[11:08]** saving the semantic memory, which are
**[11:10]** some durable facts or things related to
**[11:12]** the user profile. So, if the user has a
**[11:14]** habit or has some important facts or
**[11:16]** information it should remember, then it
**[11:18]** will be saved in the memory.md. And then
**[11:20]** what's interesting is that for Hermes,
**[11:22]** instead of doing the embeddings, it's
**[11:24]** actually just using plain text, okay?
**[11:26]** It's using top top K keyword instead of
**[11:28]** doing the embedding or the rack system.
**[11:30]** It's very interesting because I'm not
**[11:31]** too sure why, but it's just doing the
**[11:33]** text. So, remember that we say the agent
**[11:35]** run is ephemeral. Now that with the
**[11:37]** working memory to be fed into the agent
**[11:40]** for all the loop engineering,
**[11:41]** which includes procedure memory,
**[11:43]** semantic memory, and later we'll cover
**[11:45]** episodic memory, this will become a more
**[11:48]** complete memory system that will feed
**[11:50]** into the agent runs, which is making the
**[11:53]** harness more elegant. And the third
**[11:54]** pillar that we haven't covered is called
**[11:56]** episodic memory. It's basically the chat
**[11:57]** history or some dated events. It can be
**[12:00]** ragged or sequeld into the working
**[12:01]** memory. After every agent run, the
**[12:03]** information will flow into the episodic
**[12:06]** memory. What's different in Hermes is
**[12:08]** that the data is not saved in the cloud.
**[12:11]** It's saved in this place called
**[12:12]** state.db. Again, let's come back here.
**[12:14]** On the right-hand sidebar, if we again
**[12:17]** open Hermes folder, scroll down, you can
**[12:20]** see at the end there's a state.db.
**[12:22]** I can click on preview anyway. This is
**[12:24]** basically a database that will include
**[12:26]** all those info in your chat history, but
**[12:29]** also over time it will start to
**[12:30]** consolidate some of those chats using
**[12:32]** the Hermes auxiliary models, which are
**[12:35]** cheaper, non-important models to do this
**[12:37]** summarization task so that it will
**[12:38]** distill some facts into what we call the
**[12:41]** semantic memory or that memory.md. So,
**[12:43]** you can see this harness is running
**[12:46]** really in a self-improving autonomous
**[12:49]** situation, which is really cool. I know
**[12:51]** this chart is getting more complicated
**[12:52]** than usual, but I feel like this should
**[12:54]** be a complete summary for how the Hermes
**[12:56]** agent works. And let's go through a few
**[12:57]** more examples. Let's test out some of
**[12:59]** the stuff for memories. Save to memory
**[13:01]** that my favorite testing framework is
**[13:02]** pytest. So, this is an explicit saving,
**[13:05]** all right? It updated the memory file.
**[13:07]** So, if we go to memory,
**[13:10]** you can see one more block, which is
**[13:11]** user's favorite testing framework is
**[13:12]** pytest. That was an explicit ask from
**[13:15]** the gateway. The tool is basically,
**[13:16]** let's go update the memory over here.
**[13:19]** Search our past sessions. What was the
**[13:21]** very first thing I ever said to you? Now
**[13:23]** it's using the searching tool in the
**[13:25]** loop engineering iteration. Say the
**[13:27]** first thing I say is, "What can you do,
**[13:28]** Hermes? And what makes you special?"
**[13:30]** Let's double-check that. That's right.
**[13:32]** And it failed because I couldn't log in
**[13:35]** at that time. So, what happened was I
**[13:36]** asked the question through the
**[13:38]** interface. It went through the prompt.
**[13:40]** And in the working memory, because we
**[13:41]** asked that, so it queried the
**[13:43]** information from episodic memory, from
**[13:45]** state.db. It returned the memory into
**[13:48]** the agent. The agent was like, "Oh,
**[13:49]** okay. This is what you said." Let's try
**[13:51]** an example related to skills, which is
**[13:53]** procedural memory. So, we're going to
**[13:54]** say, "Create a skill called video prep
**[13:56]** that captures how I format my video
**[13:57]** scripts spoken in English, define jargon
**[13:59]** on inline, no m-dashes, closes with you
**[14:02]** can build anything, you can learn
**[14:03]** anything." This is an explicit call to
**[14:06]** update the skills. It used the skill
**[14:08]** management tool. Remember, in the loop
**[14:10]** engineering, there's a tool called skill
**[14:11]** management, and this is what it did. And
**[14:12]** say, "Pick-a-P, I have successfully
**[14:14]** created the video prep skill. Let's find
**[14:16]** out about it." Again, Hermes, skills,
**[14:19]** media,
**[14:20]** video prep. Double-click. It created
**[14:23]** this skill for me. It says, "No
**[14:24]** m-dashes, spoken English, define jargon
**[14:27]** inline, catchphrase, you can build
**[14:29]** anything, you can learn anything." Good.
**[14:30]** We can test the loop a little bit more.
**[14:32]** We can say, "Use delegate task to spawn
**[14:34]** two sub-agents." One is researching the
**[14:38]** LM eval harness, and another one
**[14:40]** researching VLM architecture. The agent
**[14:42]** was calling the tool called delegate
**[14:44]** task, and successfully spawned two
**[14:46]** background agents. So, you can see it's
**[14:47]** processing right now over here. They're
**[14:49]** working in parallel.
**[14:51]** Cool.
**[14:53]** Eventually, we returned the results to
**[14:54]** me. So, you can see that it spawned up
**[14:56]** some sub-agents to do tasks for me in
**[14:57]** parallel. We've already tried the cron
**[14:59]** job, and next one is spawn sub-agent
**[15:02]** that uses Claude CLI. This is my
**[15:04]** favorite. So, this is my favorite. Spawn
**[15:06]** a sub-agent that uses the Claude CLI in
**[15:08]** headless mode, basically using Claude to
**[15:10]** build a Python script fetching the top
**[15:12]** five Hacker News stories to markdown,
**[15:14]** and verify runs.
**[15:16]** Yep. It firstly delegated the task to
**[15:19]** Claude CLI. It's using the skill, you
**[15:21]** can see. Remember we read the skill here
**[15:24]** in autonomous AI agent Claude. It should
**[15:25]** be reading the skill. Is this helpful?
**[15:27]** Let me know if this is helpful. I mean,
**[15:29]** I was trying to show you more examples
**[15:31]** in the walk through so that it feels
**[15:32]** more concrete because a lot of people
**[15:34]** were asking me for implementations from
**[15:35]** my previous videos and I feel like
**[15:37]** Hermes is really good example.
**[15:42]** Okay, it created this
**[15:44]** code for me and used the Claude.
**[15:47]** It created the fetch hackernews.py.
**[15:50]** I'll just say show me the
**[15:52]** result after
**[15:55]** running the script.
**[15:58]** Yep, so these are the top five Hacker
**[16:01]** News stories on Hacker News. Let's come
**[16:03]** check. It's correct. Remember what
**[16:04]** happened was that we sent the question
**[16:06]** from the gateway, it went through the
**[16:07]** agent run and the LLM basically called
**[16:10]** up the tool called delegate task.
**[16:12]** Delegate task delegated the task to sub
**[16:14]** agent and the sub agent was running
**[16:16]** Claude code and Claude code wrote that
**[16:18]** script and sent it back. And then this
**[16:20]** agent run the script again and then we
**[16:22]** get the results. This was the hardest in
**[16:24]** the loop engineering in this entire
**[16:25]** thing. I don't think it self-triggered
**[16:28]** self-learning skills yet. It only
**[16:31]** triggered learning the memory. I'm just
**[16:33]** going to ask it explicitly, did you save
**[16:34]** any skills by yourself or did you only
**[16:36]** save memory so far? Oh yeah, but we
**[16:38]** created that but we created
**[16:41]** that skill.
**[16:43]** You did not self- realize
**[16:47]** you need to save skill.
**[16:50]** It should proactively offer to save a
**[16:52]** skill after difficult iterative task
**[16:54]** with five or more tool calls. So far we
**[16:56]** haven't done anything difficult. So we
**[16:58]** can test the gateway.
**[16:59]** I can summarize what we worked on today.
**[17:01]** Hmm, this Chrome job failed. It didn't
**[17:04]** tell me 10 jokes, it only told me two.
**[17:06]** What were the
**[17:08]** rest of the jokes?
**[17:10]** Don't lie to me because maybe you just
**[17:12]** created it. Anyways, Hermes team if
**[17:14]** you're watching this, your Chrome job is
**[17:16]** not updating it unless I ask for the
**[17:20]** results. So, maybe this is something you
**[17:21]** guys can fix. All right, let's move on
**[17:23]** and summarize what we worked on today
**[17:25]** because in this current chat, it doesn't
**[17:28]** know the rest of the stuff here. So,
**[17:29]** let's see if it's calling the actual,
**[17:32]** remember we say state DB, memory.md, and
**[17:35]** skills.md. Good, actually knows, okay?
**[17:37]** It says jokes on demand, system check on
**[17:40]** the OS version, which is what we did,
**[17:42]** YouTube stats, yes, we did that, Hacker
**[17:44]** News. Okay, good. WhatsApp here is just
**[17:47]** a gateway as an interface. It's doing
**[17:49]** the same thing as the Hermes agent
**[17:51]** desktop. This is very cool. This is I
**[17:53]** mean, this is similar to Open Claw, but
**[17:55]** still every time when I feel I can just
**[17:57]** have a personal assistant handy on my
**[17:59]** WhatsApp, this is really cool. And
**[18:00]** imagine if I host this on a virtual
**[18:02]** machine and it runs forever, I can just
**[18:04]** basically ask WhatsApp, what's going on?
**[18:06]** And it's going to reply to me. Ooh, I
**[18:08]** completely forgot. You should set up
**[18:10]** WhatsApp by typing in Hermes WhatsApp
**[18:12]** and then just follow the instructions to
**[18:14]** set it up. Should be straightforward.
**[18:16]** Last but not least, where is eval? Okay,
**[18:18]** where is our LLM ops? Remember in our
**[18:21]** original chart we had this blue box on
**[18:23]** the right-hand side called LLM ops. So,
**[18:25]** unfortunately, on Hermes, based on my
**[18:28]** current research, I don't think it has
**[18:30]** an LLM ops or an eval system. You'd
**[18:32]** probably need to build it yourself. But,
**[18:34]** it does trace the run. There's a thing
**[18:36]** called trajectory export and logs and
**[18:38]** it's basically just logging the whole
**[18:39]** thing, but there's no eval. If you
**[18:41]** watched our previous video, the eval is
**[18:43]** basically you can use tools like Line
**[18:45]** Smith, Line Fuse, and all these things
**[18:47]** that can track the entire agent run and
**[18:49]** some events that happened like tool
**[18:51]** calls, how many times did you call LLMs,
**[18:53]** did you use some cheaper models to
**[18:55]** summarize things into a semantic memory?
**[18:57]** Unfortunately, Hermes doesn't do that.
**[18:59]** I'm curious why, maybe because it's a
**[19:00]** local system, so you can just customize
**[19:03]** it yourself. It's under Hermes, you can
**[19:05]** click into logs, you can see all the
**[19:07]** logs here, can see the errors, can see
**[19:09]** the agent runs, gateway logs, too.
**[19:12]** Gateway is the entry point, which is
**[19:13]** WhatsApp or this desktop. I hope this
**[19:15]** was helpful. I think there's quite a
**[19:18]** huge amount of work that we covered
**[19:21]** today, which are exactly what Clawcode
**[19:23]** can already do or Open Claw can already
**[19:25]** do. I feel that what makes Hermes
**[19:26]** special, at least compared to Clawcode,
**[19:28]** is that it's self-updating all these
**[19:30]** things locally. And maybe this is good
**[19:33]** for privacy reasons, because I don't see
**[19:35]** why we should not save it on the cloud.
**[19:37]** Other than that, everything else should
**[19:38]** be very similar, right? It runs the loop
**[19:40]** every time when the agent needs to do
**[19:41]** some task, kind of call all these tools,
**[19:44]** and you can even schedule cron job. And
**[19:45]** then the memories and the skills are
**[19:47]** getting auto-updated into the procedure
**[19:50]** memory, semantic memory, and the state
**[19:52]** data will be saved into the episodic
**[19:54]** memory. So, I would say this is a pretty
**[19:55]** standard harness for an agent
**[19:57]** implementation. Nothing too fancy, but
**[20:00]** I'm sure they did a ton of work. But I
**[20:02]** feel like this is a good example of for
**[20:03]** how builder these days should be
**[20:05]** building products, because this is
**[20:07]** becoming a standard, right? Every AI
**[20:09]** agent tool should be self-improving and
**[20:12]** self-evolving. And depending on the user
**[20:14]** request, you can either keep it local,
**[20:16]** you can keep it on the cloud. That's up
**[20:18]** to you. I feel like the skill and memory
**[20:20]** accumulation is probably the most
**[20:22]** valuable thing in this, because the user
**[20:24]** kind of just over time get locked in.
**[20:27]** And it remembers who I am, which is why
**[20:30]** like recently I don't switch to other AI
**[20:31]** anymore. I just use Clawcode. It has a
**[20:33]** semantic memory about who I am, my
**[20:35]** company information, Automata's, and
**[20:38]** what my style of building YouTube
**[20:40]** videos. But yeah, I think it's a cool
**[20:41]** framework. You guys should try it out.
**[20:43]** It's really fun. Cool. I hope this video
**[20:45]** was helpful. If you have any questions,
**[20:46]** please leave down a comment. And if you
**[20:49]** enjoyed it, please give me a like and
**[20:50]** subscribe. Let me know what else you
**[20:51]** would like to watch. I will see you next
**[20:53]** time. Thanks.
