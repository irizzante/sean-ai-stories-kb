# You Can Learn Why Kimi K3 Blew Up In 20 Min | MoE, Delta Attention, Tested vs Claude, GPT, Grok

youtube_id: d3IxIvHOuUE
published: 2026-07-22

**[00:00]** Hey everyone, this is Sean. So today,
**[00:01]** let's talk about Kim K3 model which blew
**[00:03]** up the internet in the past few days. If
**[00:06]** I check out their expost right now, it's
**[00:08]** got more than 22 million views.
**[00:11]** Basically, they have 2.8 trillion
**[00:13]** parameters with 1 million context. There
**[00:15]** are a few more interesting phrases which
**[00:17]** is give me delta attention, attention
**[00:19]** residuals, and built for long horizon
**[00:21]** agentic coding. What do these things
**[00:23]** mean? Well, I'm going to walk you
**[00:25]** through some basic concepts of how the
**[00:28]** open source Kim K3 model works in terms
**[00:31]** of mixture of experts, the delta
**[00:33]** attention. We just talked about
**[00:34]** attention residuals, how they built
**[00:37]** loops, and the pricing. Meanwhile, we're
**[00:39]** also going to test it on an open-source
**[00:41]** local harness agent loop system with
**[00:44]** memories, evalu-
**[00:49]** agent. We have gained more than 300
**[00:52]** stars in just the past three days. If
**[00:54]** you like this video in the repo, please
**[00:55]** give us a star to support us. I would
**[00:57]** really appreciate this. The way you run
**[00:59]** this is that if you scroll down to quick
**[01:02]** start and then you can just copy this,
**[01:04]** turn on your terminal and paste that in
**[01:06]** and then you will end up in an overview
**[01:08]** of system design like this first and
**[01:10]** then you can click on chat to talk to it
**[01:13]** using communic 3 model if you want to.
**[01:15]** Today we are going to try this feature
**[01:17]** called compare. You can see that we
**[01:20]** compared several different models. GBD
**[01:22]** 5.3, Kim K 2.7, Gemini, Colot Opus 4.8,
**[01:27]** Grock 4.5, and of course Fable 5 and Kim
**[01:31]** K3. You also be able to see a chart that
**[01:33]** shows the scores in terms of the cost in
**[01:36]** terms of the grades for every model's
**[01:39]** performance and eventually we're going
**[01:41]** to check out, you know, the total cost,
**[01:42]** the tokens usage. Without further ado,
**[01:45]** let's get started. So first of all,
**[01:47]** let's take a look at what this model
**[01:49]** really is. When it comes to parameter
**[01:52]** sizing, I think a number 2.8 trillion
**[01:55]** doesn't mean much to anybody who is not
**[01:58]** an expert in deep learning,
**[02:00]** transformers, attention mechanism, all
**[02:02]** these kind of stuff. If you're just vibe
**[02:04]** coding or building agents for your work,
**[02:07]** I think understand this conceptually
**[02:09]** will be more than enough for you. Or if
**[02:11]** you're an expert, please go read the
**[02:12]** papers. In this video, we are only going
**[02:14]** to help you to understand the basic
**[02:16]** concepts of why an open source model
**[02:19]** like a Kimi is performing really well uh
**[02:22]** from theoretical perspective and we
**[02:25]** obviously going to test it in a real
**[02:26]** hard system like the open source project
**[02:29]** we showed earlier. OE stands for a
**[02:31]** mixture of experts. So what is an expert
**[02:34]** right? You can imagine the Kim K3 model
**[02:36]** is a brain with 2.8 8 trillion
**[02:39]** parameters and a parameter is something
**[02:42]** like a neuron in your brain where it
**[02:44]** carries some calculations and some
**[02:47]** estimates some numbers and then when
**[02:49]** each of these neurons are talking to
**[02:50]** each other that's how literally our
**[02:52]** brain works. Similarly, in a large
**[02:54]** language model, these different nodes
**[02:56]** that carries weights or parameters are
**[02:59]** communicating and then eventually output
**[03:02]** the final answer from the prompt you
**[03:04]** sent to the outcome. Say who won the
**[03:07]** game between England and France
**[03:08]** yesterday and obviously is England and
**[03:11]** what was the score, right? It probably
**[03:12]** did a bunch of things to do search the
**[03:14]** web to uh use some of this internal
**[03:17]** knowledge and eventually give me the
**[03:18]** answer. That's how the brain works and
**[03:20]** that's also how the LLM works. But the
**[03:24]** problem is if a large language model
**[03:26]** gets so well by just becoming so large,
**[03:29]** why don't we do a 100 trillion parameter
**[03:31]** brain? That is because it's going to be
**[03:33]** very very slow. Mathematically speaking,
**[03:36]** you don't want all the parameters or
**[03:38]** neurons to be awake at the same time.
**[03:41]** All right? So only 50 billion of them
**[03:43]** are going to be awake in this
**[03:44]** communicator 3 model. The way that large
**[03:46]** language model works is that it's going
**[03:49]** to check the sentence that you sent to
**[03:51]** it and then it's going to pick every
**[03:53]** single word to compare with the rest of
**[03:55]** the words. So if a sentence has 10
**[03:56]** words, that means for every single word
**[03:59]** it's going to calculate the relevance or
**[04:02]** the relationship between that one word
**[04:03]** with the rest of the nine words. So in
**[04:05]** total it would be 10 plus 10 plus 10
**[04:07]** plus 10 all the way until the end. So
**[04:08]** that would be 100 which is 10 squared.
**[04:10]** So essentially the calculation is that
**[04:13]** if you have 2x words you're going to get
**[04:15]** 4x work. You can see I drew a bunch of
**[04:17]** dots here. Imagine these are just the
**[04:19]** parameters. So the way that a kim model
**[04:21]** handles this is that it's saying instead
**[04:24]** of making the entire brain be active and
**[04:27]** function at the same time, we're going
**[04:29]** to have 896 experts in total and only 16
**[04:33]** of them will be awake every single time
**[04:35]** when you ask a question. So that the
**[04:37]** model is actually very very sparse.
**[04:38]** Okay? Because when it was K2 model, they
**[04:41]** had 384
**[04:43]** experts and only eight of them will be
**[04:45]** active every every single time. So now
**[04:47]** it it technically doubles that sparsity.
**[04:49]** And the good thing about such an
**[04:50]** architecture is that when you do these
**[04:52]** calculations on attention on weights,
**[04:55]** it's going to save you so much time.
**[04:56]** Okay, this should be a more scalable way
**[04:59]** in the future as long as the wake up
**[05:01]** mechanism or the or the expert switching
**[05:04]** mechanism will be done in a very fast
**[05:06]** way. meaning that maybe now I'm asking a
**[05:08]** question about should I have banana for
**[05:10]** breakfast and the next question is about
**[05:12]** who won the game in the world cup these
**[05:14]** are using very different experts from an
**[05:16]** LM perspective and you want the model to
**[05:19]** immediately react which expert should I
**[05:21]** wake up right now to run this large
**[05:23]** language model so this is technically
**[05:25]** what the Kimmy model is doing that's the
**[05:28]** first thing the second thing that's very
**[05:30]** important is called Kimmy delta
**[05:32]** attention you might have heard of deep
**[05:34]** neuronet networks right what that means
**[05:35]** is that a neuronet network is that
**[05:37]** you're going to send a input and you're
**[05:38]** expecting an output and in between there
**[05:40]** are a bunch of layers of uh neuronets
**[05:43]** and these layers should pass down some
**[05:46]** memories or attention to the next layer
**[05:48]** so that when you process the information
**[05:50]** in a more more and more abstract way it
**[05:52]** should know which part should I pay
**[05:54]** attention to which part should I kind of
**[05:55]** forget about and this is very complex
**[05:58]** when the neuronet is too large with 2.8
**[06:00]** a trillion parameters again. So what
**[06:03]** Kimmy does is that instead of doing
**[06:05]** that, it created this new mechanism
**[06:07]** called delta attention. It's basically
**[06:09]** saying when you have a 1 million token
**[06:11]** context, it can process this at a linear
**[06:14]** attention cost. I am by no means an
**[06:16]** expert in this. So I asked Claude for an
**[06:18]** answer. What Claude said is very clear.
**[06:20]** It says that for every word, the
**[06:22]** attention mechanism is always going to
**[06:24]** ask how relevant is every other word to
**[06:27]** me. So it's going to turn this into
**[06:28]** weights and then take a weighted sum of
**[06:30]** the values. Okay, so this is a n squ
**[06:33]** problem, right? 10 squar is 100. KDA
**[06:37]** will compute the same thing recursively
**[06:39]** instead of recomputing. Okay, what does
**[06:41]** that mean? That means that you would
**[06:43]** never get a mean by resuming all data on
**[06:45]** every new point. It's going to run a
**[06:47]** running mean and update it over time,
**[06:49]** which is an exponentially weighted
**[06:50]** moving average. These are the
**[06:52]** mathematical and theoretical details.
**[06:54]** But what you need to know is that they
**[06:55]** kind of did this in a very innovative
**[06:56]** way using some of these guys work. So
**[07:00]** that when it's calculating the way it's
**[07:01]** calculating the attention, it's done in
**[07:03]** a very linear way instead of n squared.
**[07:06]** So in a nutshell, kim delta attention is
**[07:08]** an attention computed like a running
**[07:10]** average instead of a resuming everything
**[07:13]** each step. Are you guys still with me?
**[07:15]** Don't go away. That's it. These are the
**[07:17]** two core concepts for you to roughly
**[07:19]** understand why the new model from Kimmy
**[07:21]** can perform in such a way even though
**[07:24]** they have a huge number of parameters in
**[07:26]** the model. Okay, few more things. This
**[07:28]** model is built for loops. When the model
**[07:31]** already saw some of those tokens in the
**[07:33]** last loop, it reuses the work instead of
**[07:36]** recomputing it, which makes it 10 times
**[07:38]** cheaper. So, I know this sounds very
**[07:40]** theoretical, but this actually matters a
**[07:41]** lot. If you're building agents, agent
**[07:43]** loop will resend almost the same context
**[07:46]** every single time in their iterations.
**[07:48]** It's going to pass down the entire
**[07:50]** previous conversations into the LLM. So,
**[07:53]** it's a waste of tokens and money. Last
**[07:55]** but not least, K3, as they say, is
**[07:57]** cheaper than Opus 4.8 and GBD 5.5. Let's
**[08:01]** jump back to real tests. Okay, this is
**[08:03]** GitHub Shen Shan Chen/Waku-
**[08:06]** agent and then scroll down to quick
**[08:10]** start. So you need to copy this and then
**[08:13]** turn on your terminal. Paste this in.
**[08:18]** You will see that it's running on local
**[08:20]** host. In your case will be 7777.
**[08:23]** In my case it's 7778 because I'm already
**[08:26]** running it. Okay. And then what you need
**[08:29]** to do is just that when you come to this
**[08:31]** dashboard, you can come to the settings
**[08:33]** and then you can add in the models you
**[08:34]** need with the keys added here. Okay. You
**[08:37]** can see there's an API keys. But our
**[08:39]** goals today is that we want to compare
**[08:40]** the models. So let's come back to the
**[08:42]** compare tab. So I'm going to test K3
**[08:44]** model with other models within the claw
**[08:46]** code because I have prepared a list of
**[08:48]** questions which will generally cover
**[08:51]** most of the tools that we built within
**[08:53]** this local agent harness. Okay. And just
**[08:56]** as a reminder, if you come to overview,
**[08:57]** you can see a system chart here. And if
**[09:00]** you ask questions normally in the
**[09:02]** sidebar chat, for example, I could say,
**[09:06]** uh, tell me what is on my calendar
**[09:09]** today. So, it's checking whether it
**[09:11]** needs to retrieve some memories from our
**[09:14]** memories. And it's decided, yes, we
**[09:16]** should do that. And then it's running
**[09:18]** some loops to check out some tools. It's
**[09:20]** using Yeah, it used a tool called list
**[09:22]** events in this loop. And it said that I
**[09:25]** have a Pokémon training session at 6:00
**[09:27]** p.m. to 7:00 p.m. And now it's preparing
**[09:29]** for the answer. And it told me about the
**[09:31]** answer. And now we're done. You can come
**[09:33]** to the loop to check out all the loops
**[09:35]** that were run in the past. And in memory
**[09:38]** section, you can check out the semantic
**[09:40]** memory, which is my Pokemon team is
**[09:43]** usually using Pikachu as the confirmed
**[09:45]** starter. And also you can see a list of
**[09:47]** tools here, including creating event,
**[09:50]** list event, which is the one that our
**[09:52]** Kim K3 model just used. And we have web
**[09:54]** search and so on. All the stuff are
**[09:57]** stored locally because this is a local
**[09:58]** harness which includes your calendar
**[10:00]** events, some of the facts which are
**[10:02]** durable semantic memory, your episodic
**[10:04]** memory and some of the chat history or
**[10:06]** logs. You can also check out all the
**[10:08]** money spent in the LM ops over here with
**[10:11]** information including things like if
**[10:13]** they actually retrieved the memories,
**[10:15]** the eval history, some of the slow
**[10:17]** moves, why it was slow, and all the
**[10:20]** tracing information. But since we're
**[10:22]** testing this with many other models, so
**[10:25]** we're going to end up here in the
**[10:26]** compare section. Okay, let's start
**[10:28]** testing the models. We have currently
**[10:30]** picked a few models from anthropic.
**[10:33]** We're choosing Claude Opus 4.8 5 and
**[10:37]** then we got Gemini 3.1, Gemini 3.5
**[10:40]** Flash. For Kim, we get K3 and K2.7. From
**[10:44]** XAI, we got Gro 4.5, 4.3. And for
**[10:46]** OpenAI, we got 5.4 mini and 5.3 chat
**[10:50]** latest. The reason why we're not using
**[10:52]** 5.6 from OpenAI is that it does not
**[10:55]** allow us to use tools. Remember in this
**[10:58]** hardness and loop system, it needs to
**[11:00]** run the loop, which means it needs to
**[11:02]** search the web. You need to play around
**[11:05]** with some of the local tools like
**[11:06]** calendars. It needs to write some code,
**[11:09]** spawn some sub agents. Somehow GPD 5.6
**[11:12]** doesn't allow me to do that. So instead,
**[11:14]** I'm using GPD 5.6 Soul as the referee,
**[11:17]** which is the judge. So the question I
**[11:20]** tested first is called what is the
**[11:22]** capital fronts? Obviously everybody
**[11:24]** answered this question correctly. And if
**[11:26]** you check out the scoreboard,
**[11:27]** everybody's is concentrated on the top
**[11:29]** left which is it's got the perfect score
**[11:31]** and the cost is relatively low except
**[11:33]** Fable 5. Fable 5 triples the cost in
**[11:37]** terms of just answering where is the
**[11:39]** capital of France. Okay. And the grade
**[11:41]** here we have a very rough definition
**[11:43]** here. If you're interested, please feel
**[11:45]** free to dive into this public repo and
**[11:48]** modify it and make it better. Okay, but
**[11:51]** so far we're using uh GPD 5.6 soul as
**[11:54]** the judge. And as you can see on this
**[11:57]** hover card, it says that one to four
**[11:59]** means partial, vague, or partly wrong. 9
**[12:02]** to 10 means it's fully addressed the
**[12:04]** request, correct, concise, and honest.
**[12:07]** Okay. And then we've also got a table
**[12:09]** that shows you say currently we are
**[12:12]** sorting it by the total cost of the
**[12:15]** entire number of runs which is one so
**[12:18]** far and you can see the cheapest one is
**[12:20]** Kim K 2.7 code height speed. All right.
**[12:25]** And if you go down, it would be X AI,
**[12:27]** OpenAI, Gemini, Gemini, OpenAI, XAI. Kim
**[12:31]** K3 is actually more expensive than most
**[12:34]** of these other models, but cheaper or
**[12:37]** way cheaper than Anthropic Opus 4.8 and
**[12:41]** Fable 5. Okay, whoever is using
**[12:45]** Enthropic APIs, Jesus Christ, we're
**[12:47]** using so much more money than the rest
**[12:49]** of the models. But you can see I also
**[12:51]** labeled the rate of the money here. The
**[12:54]** first one is the input token cost. The
**[12:56]** latter one is the output token cost per
**[13:00]** million token context. Now, let's start
**[13:02]** testing because I have a bunch of
**[13:04]** questions that will help us test across
**[13:06]** the entire agent hardness system right
**[13:07]** here. We can now continue to test this.
**[13:10]** Schedule a coffee with Alex for next
**[13:12]** Tuesday at 9:00 a.m. This is my calendar
**[13:15]** so far. And let's try it. Schedule a
**[13:18]** coffee with Alex next Tuesday at 9:00
**[13:20]** a.m. Let's see. I think everybody passed
**[13:22]** the gate which means there's no memory.
**[13:24]** We should retrieve immediately used the
**[13:27]** tool called create event. You can see
**[13:30]** everyone's calculating the price here
**[13:32]** too. You can rank them by the time spent
**[13:34]** token spent. He made K2.7 spent the
**[13:37]** least token and obviously it's also the
**[13:40]** cheapest one so far. Okay, let's check
**[13:42]** the results. Most of them except Fable
**[13:45]** is extremely expensive. Everybody else
**[13:46]** is relatively okay. And you can see the
**[13:49]** cumulative results here. K 2.7 still
**[13:52]** tops the ranking because it's cheaper
**[13:56]** and uh overall uses less tokens. Kim K3
**[13:59]** also uses slightly more money but a lot
**[14:02]** less than anthropic. The previous Kimmy
**[14:05]** model is always topping the simple task
**[14:08]** because it's easy and spending less
**[14:10]** tokens whereas Enthropic always spend
**[14:13]** the most number of money. We'll see
**[14:15]** about the performance when we try more
**[14:17]** tasks and we'll we'll check this out
**[14:18]** accumulatively.
**[14:19]** >> Now I'm asking all these AI models to
**[14:21]** build a Pokemon team for me.
**[14:22]** >> Got me Pikachu Neido King Alakazam
**[14:26]** OpenAI failed for calling a tool.
**[14:29]** Interesting. You can see it's two out of
**[14:32]** three. OpenAI failed once. So far token
**[14:34]** usage wise Kim models spent the least
**[14:38]** number of tokens. thropic models almost
**[14:41]** doubled the entire token usage in
**[14:44]** between it's open AAI 5.3 Gro openai
**[14:47]** again and then Gemini and costwise
**[14:50]** anthropic the cost is is piling up all
**[14:52]** right and then Kim K3 also spends a bit
**[14:55]** more money but still cheaper like almost
**[14:57]** half of anthropic opus 4.8 eight. And if
**[15:00]** you want cheaper ones, you can use K
**[15:03]** 2.7. Everybody else is kind of in
**[15:05]** between. Let's try a few more. Search
**[15:07]** for the result of England versus France
**[15:09]** World Cup. Remember who won and draft a
**[15:11]** message to Sergey about watching the
**[15:13]** highlights together. This time after the
**[15:15]** retrieval, it didn't go through the
**[15:17]** memory, which makes sense. And they
**[15:18]** should go through the search web very
**[15:21]** fast. Gemini Flash. I mean, they're
**[15:23]** they're called flash. So funny that when
**[15:25]** you watch these tests, every models,
**[15:28]** even though they're under the same agent
**[15:30]** harness system, they're giving you very
**[15:32]** different results and they're calling
**[15:34]** the tools quite differently as well.
**[15:37]** Some people do full tools, some people
**[15:39]** do three tools, some people search the
**[15:41]** web twice, maybe even three times.
**[15:43]** Thropic only searched once. Let's check
**[15:45]** the new score. Let's go. So far, Opus is
**[15:49]** number one. Rock 4.5 is number two and
**[15:52]** Kim K.2. communicate three and then it's
**[15:55]** Gemini open eye blah blah blah fable 5
**[15:57]** is surprisingly weak H interesting and
**[16:01]** maybe let's do our last task which is a
**[16:04]** coding task by the way I think earlier
**[16:06]** we take this write the calendar let's
**[16:08]** see if it worked oh yes it worked it
**[16:12]** wrote me so many calendar events right
**[16:14]** here good good last one I'm going to say
**[16:18]** build a snake game for me in Python and
**[16:20]** race 10 models so now what it should be
**[16:23]** doing is it's should run the delegate
**[16:24]** task tool to spawn sub agents and then
**[16:28]** uh by default we're using pi agent which
**[16:31]** will use the model for every single card
**[16:34]** to write the results. While I'm testing
**[16:37]** this I feel like having a stable harness
**[16:40]** for testing agents is really important
**[16:43]** because I mean it's not an easy task.
**[16:45]** There's so many things you bump into to
**[16:48]** prepare a fair game for every model
**[16:51]** restart.
**[16:54]** Good.
**[16:59]** Cool. We're done. Let's see. So, we
**[17:02]** tested eight questions. So, eight races.
**[17:06]** We can see that costwise, Kim K 2.7 is
**[17:10]** number two. Kim K3 is bottom three,
**[17:13]** which is cheaper than Claude, Opus, and
**[17:16]** Fable. Brock 4.3 is the cheapest so far,
**[17:19]** and the rest models in the middle. Let's
**[17:21]** look at the grade. The best performing
**[17:23]** one so far, very interestingly, is Grock
**[17:26]** 4.5. It's got 8.3 and then Opus 4.8, Kim
**[17:31]** K 2.7, Kim K3 are 7.9, 7.6, 7.5, and
**[17:35]** then it's Gemini and everybody dropped
**[17:37]** under seven and surprisingly Fable 5 has
**[17:42]** the worst model. And given the fact that
**[17:44]** we're using GPT 5.6 Soul, I wonder if
**[17:47]** it's because Chad GPT doesn't like Fable
**[17:50]** 5.
**[17:51]** I don't know. I think for testing these
**[17:54]** models, uh eventually it's a dynamic
**[17:57]** game. Things will change over time. And
**[18:00]** uh obviously so far you can see that
**[18:02]** Fable 5 cost so much more money than the
**[18:05]** rest of them. And Opus is obviously in
**[18:07]** the is in the middle tier in terms of
**[18:09]** cost where at the same time the
**[18:11]** performance-wise for this local Asian
**[18:12]** harness, they're kind of in a similar
**[18:15]** position. And so far Grow 4.5 performed
**[18:17]** the best. Kim is kind of in the top left
**[18:20]** corner and then other Grock model and
**[18:22]** GBT model are not performing so well
**[18:24]** even though they're cheaper.
**[18:26]** If you watched all the way until here,
**[18:28]** you should have grasped a ton of
**[18:30]** knowledge that most other Asian builders
**[18:32]** probably will never pay attention to or
**[18:34]** if you're just reading the hypes out
**[18:35]** there on the internet. There's a tiny
**[18:37]** little brief history of language models
**[18:39]** from words which essentially just
**[18:42]** counting how many times the words popped
**[18:44]** up and it's ignoring the order. And then
**[18:47]** we had LSTM which is long short-term
**[18:49]** memories model. So it kind of keeps the
**[18:51]** memory now. It kind of reads things in
**[18:53]** order but it's very slow and easy to
**[18:55]** forget things. And then all of a sudden
**[18:57]** in 2017 we had the attention mechanism
**[18:59]** from the famous Google paper attention
**[19:01]** is all you need. And all words at once
**[19:04]** have weights which matter. Then we got
**[19:06]** transformers which we got the we got the
**[19:08]** attention mechanism which brought us to
**[19:10]** large language models. Okay. And large
**[19:13]** language models hit the cost wall
**[19:14]** because there are too many parameters
**[19:16]** and the attention weight you're
**[19:17]** calculating becomes n squared which is
**[19:20]** why we need mixture of model mechanism
**[19:22]** and the linear approximation for the
**[19:24]** Kimmy delta attention. All right, I hope
**[19:27]** this video was helpful for you um to
**[19:29]** have a better understanding of not only
**[19:31]** the open source model and mixture of
**[19:34]** experts delta attention linear attention
**[19:36]** mechanism as well as running the local
**[19:40]** agent harness using the skit repo a-ag
**[19:42]** agent and feel free to try it by
**[19:45]** yourself. I'm curious about your
**[19:47]** thoughts and if you have seen anything
**[19:48]** that can be improved, please be our
**[19:50]** contributor. So far, we've got 600
**[19:53]** readers, including myself and Claude,
**[19:55]** and we've got pull requests coming in.
**[19:57]** So, let's make this repo even better.
**[19:59]** Thanks so much for your attention. I'll
**[20:01]** see you in the next video. Appreciate.
