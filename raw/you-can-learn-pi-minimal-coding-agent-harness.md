# You Can Learn Pi Minimal Coding Agent Harness In 22 Min | Skills, Extensions, Packages, Bash

youtube_id: 0sI0MbCt4f4
published: 2026-07-25

**[00:00]** Everyone's Sean. So, today let's talk
**[00:01]** about Pi Agent Harness. It's a really
**[00:04]** interesting agent harness that I come
**[00:05]** across recently. They basically claim
**[00:08]** that they don't do any MCPs, no sub
**[00:10]** agents, and no plan mode, no to-do's, no
**[00:13]** permission pop-ups, none of those. And
**[00:15]** if you read their official website,
**[00:16]** pi.dev,
**[00:17]** and you scroll down to this current
**[00:18]** page, what we did not build, you will
**[00:21]** see exactly what I said, none of these
**[00:23]** things.
**[00:25]** This got me really interested because I
**[00:26]** feel like in history, some of the
**[00:28]** greatest projects are always built on
**[00:30]** top of some very simple, minimalistic
**[00:33]** building block, which is why I wanted
**[00:35]** you to walk you through the system
**[00:37]** design of this Pi Agent Harness.
**[00:39]** And we're going to go through their
**[00:42]** public repo on GitHub. They've got 77.3
**[00:45]** thousand stars already.
**[00:47]** And they've got really good, clean
**[00:48]** documentations online, as well. Also, at
**[00:51]** the same time, we're going to test it in
**[00:53]** another agent harness and loop system
**[00:55]** called Waku-Agent.
**[00:57]** It's a harness system that I built for
**[01:00]** anybody who want to run a personal AI
**[01:02]** agent on your laptop to manage your own
**[01:04]** memories, eval, and loops. And the
**[01:07]** interesting part here is that if you
**[01:09]** have an agent harness system with a
**[01:13]** proper gateway, a working memory, a loop
**[01:15]** system, and an eval system, you can
**[01:18]** spawn up your own sub agents to finish
**[01:19]** some task, and your own sub agent can
**[01:21]** call Pi Agent as the coding agent to
**[01:24]** finish the task for you.
**[01:26]** I believe this is how Open Claw did the
**[01:28]** coding for themselves, too, because Pi
**[01:30]** Agent is sort of in the background
**[01:32]** writing the code for Open Claw requests
**[01:34]** on anything engineering-related. I'll
**[01:36]** show you a very quick example before we
**[01:38]** go back to the system design. So, I'm
**[01:40]** testing this prompt saying, "Write me a
**[01:41]** script that can tell me the Pokémon data
**[01:43]** if I input any Pokémon." So, what had
**[01:45]** happened is that it's now delegating
**[01:48]** this task to its coding specialist,
**[01:50]** which in our case is Pi Agent. And now
**[01:53]** it's sort of just spawning up a sub
**[01:55]** agent, and that sub agent is calling the
**[01:58]** CLI of Pi Agent in the back end to write
**[02:00]** up this code and later it's going to
**[02:02]** return the code back to us after you
**[02:05]** finished. I believe this is why Pi Agent
**[02:07]** is very extensible and people love to
**[02:09]** build an ecosystem around it because you
**[02:11]** can literally just plug in into any of
**[02:13]** these harness systems you build
**[02:14]** yourself.
**[02:16]** I found this really fascinating.
**[02:17]** And you can see now that Pi has finished
**[02:21]** because we use this tool called delegate
**[02:23]** task. Delegate task basically spun up
**[02:24]** the sub-agent called Pi Agent
**[02:26]** and then they write up this code for us.
**[02:30]** So that was the example of the end goal
**[02:32]** where when you have another agent
**[02:33]** harness system that can write code for
**[02:35]** you.
**[02:36]** Now we want to understand how the
**[02:38]** building block is actually constructed,
**[02:40]** right? Because that would be helpful for
**[02:41]** us to understand how do we master the
**[02:43]** best way to use Pi Agent as our coding
**[02:47]** agent by default. Later I'm going to I'm
**[02:49]** going to also going to show you some
**[02:50]** examples of how you can build up some of
**[02:53]** these tools to make your Pi Agent even
**[02:56]** stronger than just pure plain code.
**[02:58]** First of all, Pi Agent has a very simple
**[03:00]** interface or if we call it faces, it has
**[03:03]** only four main costumes. TUI, which is
**[03:06]** terminal user interface or you can run
**[03:09]** it as a CLI, run it once. You can even
**[03:11]** do event streaming, which means that it
**[03:13]** will spit out all those thinking steps
**[03:15]** for a question you ask and eventually
**[03:18]** you can have a live pipe, which is using
**[03:20]** RPC. I'll show you a quick example.
**[03:22]** First thing first, we should come to the
**[03:23]** Pi Agent website and we should copy this
**[03:25]** curl if you're on a MacBook or this
**[03:28]** PowerShell one if you're on a Windows.
**[03:30]** I'm using a MacBook so I'm going to copy
**[03:31]** this line. Then we're going to come to
**[03:32]** the terminal and paste that in. Then you
**[03:34]** will be now you're installing the Pi
**[03:36]** Agent and since I have already installed
**[03:38]** it so I won't reinstall it. So I'll just
**[03:40]** do nothing. Okay. And after that what
**[03:42]** you do is that we can just type in Pi to
**[03:44]** test out the terminal user interface.
**[03:46]** And if you have not set up any models,
**[03:49]** you can just do {slash} login. You can
**[03:51]** either sign in with an account or an API
**[03:53]** key. If you do an account in Anthropic,
**[03:56]** it will pop up this window for you to
**[03:58]** authorize your account. And it's going
**[03:59]** to say authentication successful. You
**[04:01]** come back here, and you can do /model to
**[04:04]** switch the model to Claude. Uh let's try
**[04:07]** Haiku 4.5. And we just say hello. Yeah,
**[04:10]** cool. It's in
**[04:11]** because it's in my directory in Waku
**[04:13]** Agent, it's telling me about do I do you
**[04:14]** want me to do something about it? We're
**[04:16]** not going to call anything else yet, but
**[04:18]** I'm just going to show you a few more
**[04:19]** things. If we do control C, and if I do
**[04:22]** pi {dash} p, and then give it a
**[04:24]** question, be like, "Who is Sam Altman?"
**[04:28]** Then, instead of turning on the terminal
**[04:30]** user interface, it's just going to
**[04:32]** return the answer back to me. And it's
**[04:35]** telling me about that he's a CEO of
**[04:36]** OpenAI, and he's one of the most
**[04:38]** prominent figures in the AI industry,
**[04:40]** which I'm sure Elon is not going to
**[04:42]** agree with.
**[04:43]** Uh next one is next one is pi mode JSON
**[04:47]** for testing the event stream. And I'll
**[04:49]** just say pi {dash} {dash} mode JSON,
**[04:51]** "Will Elon be happy with Sam Altman?"
**[04:52]** Eventually.
**[04:54]** And instead of just showing me that one
**[04:56]** answer, you see that it's showing me the
**[04:58]** entire thinking process.
**[05:00]** And eventually, I think the answer is
**[05:02]** probably somewhere.
**[05:03]** So, if you're curious about their
**[05:04]** current relationship status, recent
**[05:06]** public statements, I could search for
**[05:08]** that information. Otherwise, blah blah
**[05:09]** blah. Okay. So, you see this is showing
**[05:11]** me the thinking process, and it streamed
**[05:14]** the entire thinking process back to me.
**[05:16]** And obviously, you can try the RPC one
**[05:18]** as well if you're interested, but this
**[05:20]** is out of the scope for this video. So,
**[05:22]** earlier, the way we used pi agent was
**[05:24]** not through the terminal, remember? The
**[05:25]** way we used it was that we were testing
**[05:27]** the Waku Agent, and we asked the
**[05:29]** question, and our agent spun up this
**[05:33]** tool called delegate task, and spun up a
**[05:35]** sub agent to call pi agent to write the
**[05:38]** code for me. The way it did it is that
**[05:41]** our sub agent started a pi agent, and
**[05:44]** did exactly what we just tested on the
**[05:46]** terminal, like here. And then he got the
**[05:48]** answer and he returned it back to our
**[05:50]** agent. That's literally how
**[05:53]** This is literally how you either use Pi
**[05:56]** Agent by itself or you use a different
**[05:58]** harness, which will call Pi Agent to
**[06:00]** write task for you. Understand?
**[06:02]** Okay, let's move on. After a user or
**[06:05]** another agent harness ask the question
**[06:08]** through this interface, what he does
**[06:10]** next is that it's feeding the context of
**[06:12]** the whole state into the LLM. And he's
**[06:16]** preparing the context for us. The way
**[06:17]** that it prepares context is that it has
**[06:20]** a few things. It has number one,
**[06:21]** agents.md,
**[06:23]** which is a file within Pi Agent. I'm
**[06:25]** going to show you real quick. So, if you
**[06:27]** cloned your Pi Agent, you will have a
**[06:28]** folder here in your directory. And if we
**[06:31]** go down, you can see there's a file
**[06:33]** called agents.md.
**[06:36]** So, this agents.md is basically defining
**[06:38]** how exactly Pi Agent is responding to
**[06:40]** your questions. I really like how the
**[06:42]** author says specifically that no fluff
**[06:44]** or cheerful filter text. If you're
**[06:47]** saying thanks, just don't say thanks so
**[06:49]** much, which is the opposite of you're
**[06:51]** absolutely right from Clockwork. So, I
**[06:53]** can see that they have very different
**[06:55]** design philosophy here. And then it's
**[06:57]** also focusing on the code quality, also
**[06:59]** define how you should run commands,
**[07:01]** dependency and install security, how you
**[07:03]** should use GitHub, and issues and PRs,
**[07:06]** blah blah blah. Okay. So, this is a
**[07:08]** definition of how the Pi Agent should
**[07:11]** behave as an agent. And that agents.md
**[07:15]** is part of this context we're going to
**[07:17]** feed into the LLM later.
**[07:20]** And obviously we're going to have a
**[07:21]** system prompt as well. And in total,
**[07:24]** these two will be combined into a JSON
**[07:26]** file, which is forkable,
**[07:28]** and they'll be fed into the Pi Agent
**[07:31]** loop. The system prompt is within the Pi
**[07:33]** folder, packages,
**[07:36]** coding agent, source, core, finally
**[07:39]** system prompt.ts.
**[07:43]** There we go. This is its system prompt,
**[07:46]** which is very simple. Look at this. You
**[07:48]** are an expert coding assistant operating
**[07:51]** inside Pi
**[07:52]** a coding agent harness. Yadadadada.
**[07:55]** And it got tool list, it got the
**[07:57]** guidelines,
**[07:58]** and all the rest of the stuff. Then
**[08:00]** we're going to look at how the Pi agent
**[08:02]** was running the loop. How do you use
**[08:04]** tools and what kind of tools can you
**[08:06]** use, right? It doesn't even have MCPs.
**[08:08]** It doesn't pop up any permission calls.
**[08:10]** There's no plans. There's no sub agents.
**[08:12]** It's just its own very basic agent that
**[08:16]** does the coding. And now let's look into
**[08:18]** how the loop works here. Okay? So,
**[08:21]** after we provide this context,
**[08:24]** obviously, we're going to feed it into
**[08:26]** the LLM. And the LLM is, if you still
**[08:30]** remember, if you come back here and then
**[08:32]** type in Pi,
**[08:34]** and we, because we logged in to
**[08:36]** Anthropic, you can see that our current
**[08:38]** model is Claude Haiku 4.5. And you can
**[08:41]** always switch models by doing,
**[08:46]** you know,
**[08:47]** these selections. And the what the LLM
**[08:49]** does within this agent harness is that
**[08:51]** it's first going to check out
**[08:53]** what kind of tools are there.
**[08:55]** Are we going to use any tools? If not,
**[08:57]** send the reply.
**[08:59]** If yes, are we allowed to use that tool?
**[09:02]** And if yes,
**[09:04]** here comes the four only actions that Pi
**[09:08]** agent has. Read, write, edit, and bash.
**[09:12]** Bash means you're just typing into
**[09:14]** commands into command lines. I'm going
**[09:15]** to show you exactly where this is in
**[09:17]** their code. And I just think that this
**[09:20]** is absolutely beautiful. Come back to
**[09:22]** the Pi agent folder.
**[09:23]** It's within packages, coding agent,
**[09:27]** source, core, and tools.
**[09:30]** So, you can see that within this
**[09:31]** directory,
**[09:33]** they have bash.ts, they've got edits.ts,
**[09:36]** find, grep. I mean, these make sense
**[09:39]** because these are just checking things
**[09:40]** out. Uh
**[09:42]** it can read and write.
**[09:44]** Basically, four main tools: read, write,
**[09:45]** edit, bash.
**[09:47]** Super simple.
**[09:49]** And then after they finish this task,
**[09:51]** it's going to write some sessions
**[09:53]** into a tree,
**[09:55]** which means that it's a JSON file with
**[09:57]** some kind of tree structure, and you can
**[09:59]** check it out in your fork or {slash}
**[10:02]** tree. And these information will be
**[10:04]** stored in this structure. So, the
**[10:05]** sessions are not stored within this pi
**[10:08]** folder because this is the GitHub. This
**[10:11]** is the open-source code that they
**[10:13]** published right here. Okay? It's this
**[10:15]** repo. We're not going to change this
**[10:16]** repo. The sessions are your own data.
**[10:19]** It's on your own laptop. So, it's
**[10:20]** supposed to be in your home directory.
**[10:22]** It's If I scroll down, I will be able to
**[10:24]** see that there's a dot pi folder right
**[10:26]** here.
**[10:26]** And I can see there's a folder called
**[10:28]** sessions. Okay? And see a bunch of
**[10:30]** sessions right here.
**[10:31]** All right? Yeah, earlier I was asking
**[10:33]** about some colors and fruits. These were
**[10:35]** in my test. Okay? And I think this is
**[10:38]** probably the latest one. And you can
**[10:40]** also check out these sessions in your
**[10:41]** own terminal. Tell me
**[10:43]** a yellow Pokémon. Okay, it gave me
**[10:46]** Pikachu. And I'll say, "Tell me the type
**[10:51]** of Pikachu."
**[10:54]** It says electric type. And then now
**[10:56]** because we had some sessions, we just
**[10:58]** had literally use this terminal user
**[10:59]** interface, and it prepared this context
**[11:02]** with agents and system prompt. And then
**[11:05]** it fed into Claude 4.5 Haiku model. And
**[11:08]** then it decided that it used some tools
**[11:10]** to check out the Pokémon index online.
**[11:13]** And then it was allowed, and then it
**[11:16]** started writing something. And it gave
**[11:18]** me a session. So, the way we check
**[11:20]** sessions is either we go back to
**[11:23]** here. It's right here.
**[11:25]** It said that the user is asking about
**[11:27]** Pikachu's type. I already looked this up
**[11:29]** in the previous command. Pikachu's type
**[11:30]** is electric type. Okay? You can see that
**[11:32]** everything is in the local dot pi agent
**[11:34]** folder sessions. Okay, I will also check
**[11:36]** it out in the terminal by doing slash
**[11:39]** fork.
**[11:40]** Okay? You can fork any of these topic
**[11:43]** and command and then you can just
**[11:44]** continue it. Okay? And it must not be
**[11:47]** Pikachu. So, basically this is what it
**[11:49]** means by it's the session is a tree
**[11:52]** because you can just sort of trace back
**[11:54]** to where exactly the previous session or
**[11:56]** message was and you can follow up and
**[11:59]** continue to ask questions. I think this
**[12:01]** is very handy if you're building some
**[12:04]** code because it's technically version
**[12:05]** control, right? You can trace back to
**[12:08]** exactly what you wrote in the past and
**[12:10]** it can branch into different sessions
**[12:13]** later. Why is this so slow? What's wrong
**[12:15]** with Haiku? This is such a simple
**[12:17]** question.
**[12:18]** What's a yellow Pokémon that's not
**[12:20]** electric type?
**[12:22]** Wait, I actually Wait, I actually I need
**[12:24]** Google. Okay, it's taking too long. I'm
**[12:26]** just going to stop this. Sometimes tool
**[12:28]** may not work out, right? So, if it
**[12:29]** doesn't work out if it's blocked, it
**[12:30]** should return the results back to the
**[12:32]** LLM and the LLM is basically going to
**[12:34]** continue to run through the loop to
**[12:37]** determine if you have finished the goal.
**[12:39]** And you might be wondering where is the
**[12:41]** loop and what does it even look like?
**[12:42]** Okay, it's a agent-loop.ts
**[12:45]** file. It's got only 792 lines. Again,
**[12:48]** let's come back. It's this folder.
**[12:50]** Again, it's under packages/agent.
**[12:52]** So, it's within the pi agent folder that
**[12:54]** we cloned over here and packages agent
**[12:59]** source agent-loop.ts.
**[13:01]** And if you scroll down, that's exactly
**[13:04]** 792 rows. And what it does is that it's
**[13:08]** defining a bunch of functions related to
**[13:11]** agent loop and all the functionalities
**[13:14]** needed to finish up the loop. So, this
**[13:17]** entire loop is what was writing code for
**[13:20]** us in that agent harness
**[13:22]** because it was deciding if it should
**[13:24]** call certain tools. Okay? And the tools
**[13:26]** is basically as we said, read, write,
**[13:28]** edit, and bash.
**[13:30]** So simple.
**[13:31]** And then you might be wondering, but in
**[13:33]** that case, isn't this going to be very
**[13:35]** stupid because it's got nothing? And I
**[13:38]** guess the answer is yes. It's going to
**[13:39]** be not as good as Claude code. And the
**[13:43]** reason why I have not brought up Claude
**[13:44]** code is that Claude code is basically a
**[13:46]** a closed source uh coding agent harness
**[13:50]** by itself. You don't know what kind of
**[13:51]** tools Claude code is doing. And the
**[13:53]** Claude code has plugged in a ton of
**[13:55]** MCPs, sub-agents kind of
**[13:57]** functionalities. I'm sure you have come
**[13:59]** across situations where Claude code just
**[14:01]** you can do planning with it, you can can
**[14:03]** it's going to list to-dos for you,
**[14:05]** right? It's going to ask you permissions
**[14:06]** all the time.
**[14:08]** The reason why Pi Agent is not doing
**[14:09]** that is because sometimes one MCP can
**[14:13]** add tens of thousands of hundreds of
**[14:14]** thousands of contexts into your 1
**[14:17]** million token context window. And most
**[14:20]** of the time you probably won't even use
**[14:22]** it. Okay? For example, let's say you
**[14:24]** have an MCP about Notion. And you
**[14:27]** probably don't even write to Notion or
**[14:30]** read from Notion at all for maybe 90% of
**[14:33]** the times when you're using a Claude
**[14:35]** code. Then these MCP contexts will just
**[14:38]** be used for nothing. You don't want
**[14:40]** that. Uh so Pi Agent reduced that
**[14:42]** completely. What they did is that
**[14:44]** instead of saying, "Hey, by default, let
**[14:47]** me connect all these MCPs back to you."
**[14:49]** I'll let you decide. Okay? And the way
**[14:51]** they do that is the following. They make
**[14:54]** Pi Agent stronger
**[14:56]** by allowing the user to write their own
**[14:59]** skills,
**[15:00]** extensions,
**[15:02]** packages,
**[15:03]** and run your own bash with the readme
**[15:05]** file.
**[15:06]** What do we mean by that? So, a skill is
**[15:08]** basically you can tell an agent to
**[15:11]** behave in a way that you want, right?
**[15:13]** It's a procedural memory, basically. And
**[15:15]** these things normally live in your Pi
**[15:18]** Agent folder. Within the Waku Agent
**[15:20]** folder, I have a .agent skills file
**[15:23]** called pokedex, okay? With a skill right
**[15:26]** here, which is basically saying
**[15:28]** it should look up any Pokémon's types,
**[15:31]** their basic stats, and the abilities
**[15:33]** from the public Poké API out there on
**[15:35]** the market. And with the skills, Pi
**[15:38]** agent should be able to read and run the
**[15:40]** task for us, okay? Let's test it real
**[15:42]** quick. So, if I just paste that in, it
**[15:45]** knows it was using that skill, and it
**[15:47]** gave me the data of Charizard, which is
**[15:49]** a fire and flying type, and the basic
**[15:51]** stats is that its special attack is 109,
**[15:54]** speed is 100, and the ability is that it
**[15:57]** has got blaze, solar power, uh which are
**[16:00]** some basic information of Charizard. So,
**[16:03]** I typed that into the TUI, which is
**[16:05]** terminal user interface, but ideally,
**[16:07]** you should be able to type this in in a
**[16:10]** plain terminal. So, you just use say Pi
**[16:12]** with the skill of
**[16:15]** pokedex, and the provider is Anthropic
**[16:18]** using the model Haiku 4.5, and just hit
**[16:20]** start. Remember, if we come back here in
**[16:24]** the face,
**[16:25]** it's got the pi-p which is running once,
**[16:28]** okay? It's just going to give me the
**[16:29]** answer for uh the data. Oh, okay. I was
**[16:32]** asking Snor- Snorlax in this case, not
**[16:35]** Charizard. Yeah, that makes sense.
**[16:36]** Snorlax is much slower because it's fat
**[16:38]** and it ate a lot, and it slept a lot, so
**[16:41]** its HP is much higher, and it's got a
**[16:43]** strong special defense because it's got
**[16:45]** the very thick fat. Its ability is has
**[16:47]** thick fat, right? Which means that if
**[16:49]** you attack Snorlax with fire attacks or
**[16:51]** ice attacks, it's fine because it's got
**[16:53]** thick fat. Okay, pretty accurate. So,
**[16:56]** that was using the skill
**[16:57]** of my own folder. So, Pi agent was
**[17:00]** reading the skill from my own folder.
**[17:02]** Well, I was explicitly telling it to use
**[17:04]** it, right? But normally, you can just
**[17:06]** as long as it's in the agent folder for
**[17:08]** skills, Pi agent will go find out about
**[17:10]** these skills. That's the first way to
**[17:11]** make Pi agent stronger with skill.
**[17:14]** And you can also write something like
**[17:16]** extensions. Why do we need extensions if
**[17:18]** we have skills?
**[17:19]** Let's check out one example first, okay?
**[17:21]** So, the extension is not something for
**[17:24]** entire Git repo. So, it's not under the
**[17:27]** skills anymore, right? So, we create
**[17:29]** this new folder called pi/extensions.
**[17:33]** And you can create TypeScript here for
**[17:35]** Pokémon battle.
**[17:36]** So, what extension does is that it can
**[17:38]** think of it as, you know, some kind of
**[17:39]** MCP, which will sort of let you use some
**[17:42]** tools, and you can define more clearly
**[17:45]** what exactly uh in terms of
**[17:47]** functionalities, how, you know, this
**[17:49]** tool should perform. It's not as is not
**[17:51]** as simple as a skill anymore. It's got a
**[17:53]** proper thing that it's going to do. We
**[17:55]** can just load it for a quick test, okay?
**[17:57]** Let me just copy this, come back to the
**[17:59]** terminal, and paste that in. So, now
**[18:02]** it's got the extension called
**[18:03]** pokemon-battle.ts.
**[18:06]** Okay, let's see how we're going to use
**[18:07]** this. If we say anything about a type of
**[18:10]** a Pokémon, it's going to tell me the
**[18:11]** type. You can see that in this
**[18:13]** pokemon-battle.ts, we define what types
**[18:16]** are there, what types are super
**[18:17]** effective on another type, and stuff
**[18:19]** like that. Okay, so now I'm going to ask
**[18:21]** a question and be like, "If I want to
**[18:23]** defeat a Charizard, what Pokémon should
**[18:26]** I use?" Doing this reasoning, doing the
**[18:28]** event streaming, and you can see that it
**[18:30]** used the function called type match,
**[18:32]** which is right here within our
**[18:34]** extension.
**[18:35]** So, it says, "Defeat a Charizard, use
**[18:37]** best choices rock type Pokémon." Okay,
**[18:39]** because here we define that rock type is
**[18:42]** very effective
**[18:44]** on fire and flying. So, the effect
**[18:46]** becomes four times.
**[18:47]** And some good alternatives are water
**[18:49]** type and electricity type. So, that one
**[18:52]** was using the extension files. It was
**[18:54]** not using the skills, because skills
**[18:56]** cannot define more tools. This one was
**[18:58]** showing you some tools, okay? But again,
**[19:00]** this is a very simple example. In coding
**[19:02]** scenarios, this would be way more
**[19:03]** complex than this. And the next one is
**[19:06]** that we can even package it into a
**[19:08]** package, okay? So, you might have heard
**[19:10]** that
**[19:11]** the pi agent ecosystem has got more than
**[19:13]** 2000 packages and that's because people
**[19:16]** have just been like playing around with
**[19:17]** this and putting together some skills
**[19:19]** and extensions and wrap it up as a
**[19:21]** package.
**[19:22]** I have built up a package right here
**[19:24]** called pie-pokedex.
**[19:26]** So it's got the extensions, it's got the
**[19:28]** skills and it's got the package.json,
**[19:31]** it's got the readme. So you can just
**[19:33]** trigger pie agent to download that
**[19:35]** package
**[19:36]** and do the task for you. Okay? So you
**[19:38]** can see you can just do pie install the
**[19:40]** pokedex and pie list. Let's try it out.
**[19:45]** You see now it installed the pipe and
**[19:47]** then it listed what packages do we have.
**[19:49]** It told us that we had the package
**[19:50]** called pie pokedex and then we removed
**[19:52]** it. Okay? And then after you install it,
**[19:55]** you you basically do exactly what we
**[19:57]** just did. Okay? It's going to call the
**[19:58]** skills, it's going to call the extension
**[20:01]** and you see you're creating this
**[20:02]** completely local kind of harness system
**[20:05]** for your pie agent and then you can just
**[20:07]** continue to grow this, right? You can
**[20:09]** continue to pile it up. You can go to
**[20:10]** the discord, you can chat with the rest
**[20:12]** of people. We come to pie agent's
**[20:14]** discord, the shitty coders club. You can
**[20:17]** check out that people are sharing their
**[20:18]** extensions here.
**[20:20]** Okay? People are talking about these
**[20:21]** extensions that people built. So I think
**[20:24]** this is very cool. You can come here and
**[20:26]** talk to folks.
**[20:28]** I think there's a very strong energy out
**[20:30]** there where people want to just
**[20:31]** construct their own agent harness with
**[20:33]** their own skills, with their own
**[20:34]** extensions and this kind of passion
**[20:36]** always keeps going. That's why an open
**[20:39]** source project like pie agent is very
**[20:41]** popular. Last but not least, you can
**[20:43]** obviously use a bash and a readme file
**[20:44]** and the model will run any program on
**[20:46]** your machine and we basically have seen
**[20:48]** that which is that our waku waku agent
**[20:51]** was spawning spawning up some sub agents
**[20:55]** using delegate task and that's going to
**[20:57]** call the terminal using bash to run pie
**[21:00]** agent to write the task for us which is
**[21:02]** what we saw earlier in the video. And
**[21:04]** you can also test out the pie agent in
**[21:06]** the terminal with the waku agent. Just
**[21:09]** type this in.
**[21:12]** And now I can just be like, "Hello, who
**[21:15]** can defeat Charizard?" You saw exactly
**[21:17]** what it did. It It skipped the gate
**[21:19]** because it does not need to retrieve any
**[21:22]** memories from our own harness.
**[21:24]** It's a literally a question and it gave
**[21:26]** me the answer. Hope this is helpful.
**[21:29]** Uh I I have heard so many good comments
**[21:30]** about pie agent, which is why I decided
**[21:33]** to make this video.
**[21:34]** And I strongly recommend that everybody
**[21:36]** should go to the pie agent GitHub repo.
**[21:40]** If you're curious, read out some of
**[21:41]** those documentation, but I think I have
**[21:43]** covered some of the most important
**[21:45]** things for you.
**[21:46]** And you should go check out their
**[21:48]** official website and download it by
**[21:50]** copying this to install it on your
**[21:51]** laptop. And if you want to do something
**[21:53]** like me, which is checking the own files
**[21:54]** of stuff, what you should do is they
**[21:55]** come to code and then copy this and just
**[21:58]** get clone this to your own folder to
**[22:00]** check it out. Okay. Meanwhile, at the
**[22:02]** same time, if you want to test out pie
**[22:03]** agent on a more complete agent harness
**[22:07]** system with memories in valve
**[22:08]** engineering, you can always come to Shen
**[22:11]** Shun Chen Waku-Agent and give us a star
**[22:15]** if you find this helpful. Thanks so much
**[22:17]** for your attention. Give us a subscribe
**[22:19]** and give us a like. Give us a comment.
**[22:20]** Give us a star on the GitHub. I'm asking
**[22:22]** too much, but if you're really
**[22:24]** interested, join us in our Discord and
**[22:27]** I'm looking forward to see you next
**[22:28]** time. Thank you very much.
