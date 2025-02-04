---
layout: post
title: Discussing AI tech with the PyData community
author: ben
image: assets/images/20250203.png
tags: []
categories: [ articles ]
---

Wowee! Just wrapped up an excellent session with [PyData Boston](https://www.meetup.com/pydata-boston-cambridge/), a local meetup group that I, incidentally, co-lead. It's always an inspiration to get together with the local tech community. 

In this session, we had the excellent [Eric Ma](https://ericmjl.github.io/) leading us off with an exploration of what really is an AI Agent, anyway? Turns out it's not so simple! 

The audience largely agreed that just having a single workflow (e.g. a prompt and a response) does not an agent make, but once we provided tools (e.g. a web search) to the LLM, it became a bit more complicated deciding whether the workflow could now be considered "agentic".  (Yeah, that word drives me nuts, too.)

[Check out Eric's write-up of the discussion and his work](https://ericmjl.github.io/blog/2025/1/31/pydata-bostoncambridge-talk-moderna-what-makes-an-agent/)

The other half of the session was a set of discussion groups, focused on various AI-related topics. This was a bit of an experiment, but I think it turned out very well.  The topics were:

1. Open source vs closed source AI - Opportunities and risks posed by open vs closed AI technology?
2. Exciting open source AI technologies - What are you using now? What upcoming tools are you excited to see? What would you like to see more of?

3. How AI is reshaping industries - What is the future of work in the AI era?

Big topics, big discussions! Here's a bit of a reportback from the groups:

### Open source vs closed source AI
I led this session so I have a bit more detail here.  My intention was to discuss definitions of open source and see how that is being applied to AI.  From there, I aimed to discuss the benefits and risks of open source _and_ closed source, since each come with their own positives and negatives.

In discussing definitions, we came up with two "types" of open source:

- Functional - one can actually replicate the function of the software with the available resources
- Resource - the resources used to develop the software are made available

This breakdown is interesting, because I think it reflects the "open weight" vs "open source" difference.  Open weight enables us to use the product of the training (the model itself), while open source would allow us to actually build our own version of the model.  We can "use" the model under both definitions, but we can only really roll our own with "true" open source.

This distinction I think is essential and it is missing from a lot of the media coverage of AI. [Open-washing](https://www.theregister.com/2024/10/25/opinion_open_washing/) is a thing.

I then introduced the [Open Source Initiative's definition](https://opensource.org/ai/open-source-ai-definition).  This prompted a discussion of which LLMs actually adhered to this model. (Spoiler, [not many](https://opening-up-chatgpt.github.io/))

The bulk of the discussion after this point centered around what, exactly, private companies contributed to the open source technologies or open data they use.  One point we landed on was that the "profit motive" was one method for ensuring a technology continues to be maintained.  Where an open source project is liable to shift priorities or lose maintainers all together, private industry might be better equipped to maintain consistency in software.

Of course, it's not like private industry has never abandoned a project.  Several participants had examples where a company cut a team or went out of business and any technology they worked on went with them.

The conversation was very interesting and took some unexpected directions (at least to me!)

### Exciting open source AI technologies
Co-organizer [Aditya](https://www.linkedin.com/in/aditya2312/) ran this discussion group and picked out two major topics in the discussion:

1. Evolving AI Agents: AI agents are advancing with capabilities like reasoning, planning, and handling complex tasks autonomously. However, the field is still maturing, with challenges in transparency, decision traceability, and defining what truly constitutes an AI agent.
2. Shift Toward Efficient Models: Alongside large-scale models, there is a growing focus on smaller, energy-efficient models and systems-centric approaches. These innovations aim to enhance accessibility while addressing the complexity of building reliable, autonomous multi-agent systems.

### AI is reshaping industries
This group was run by [Arshman Khalid](https://www.linkedin.com/in/arshmankhalid/) who very bravely stepped up to lead it.  

The group discussed how AI has impacted the workforce and how it will continue to shape the future. One trend they discussed was that there are more mid to senior roles available, likely due to AI automating many entry-level tasks. 

They also discussed some AI applications that they tended to use.  ChatGPT, unsurprisingly, was the most popular, followed closely by Cursor, Copilot and Midjourney.

Some individuals mentioned they were using technologies like Recal.ai and Bland.ai.  

One major theme was the importance of learning to use AI effectively rather than wholly depending on it.  

This makes sense to me - I find I'm getting better and better at seeing where this technology fits into my workflow. There are definitely places where AI falls on its face - and knowing when to stop arguing with the chatbots is a pretty tricky line to draw.

All in all and excellent, exciting set of conversations.

Join us next month!