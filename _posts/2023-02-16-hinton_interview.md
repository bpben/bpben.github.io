---
layout: post
title: Geoffrey Hinton Interview with On the Media
---

I recently listened to [a really interesting](https://www.wnycstudios.org/podcasts/otm/segments/how-neural-networks-revolutionized-ai-on-the-media) interview with Geoffrey Hinton, one of the major figures in the deep learning space.  The main focus of the conversation was around ChatGPT and whether AI has the capacity to understand language or even "think".

Hinton, in describing how his and his fellow researchers changed the field of AI talked about the difference between "symbolic" AI and the modern focus on neural networks.  Symbolic AI focused on rules and logic that could be coded in a somewhat human-readable way.  Neural networks are designed to "learn" rules in the form of huge arrays of parameters.

This sort of calls into question which of these approaches is closer to "thinking".  Hinton (from what I understand) seems to propose that thought is a product of a "brain state".  We try to convey that with language, but it's a sort of "lossy" format.  

I had a bit of an issue with his statement here about Noam Chomsky suggesting that thought and language are close.  I've definitely heard [Chomsky propose ideas](https://www.youtube.com/watch?v=5YXXGHwmogU) that sound very similar to what Hinton is describing here.

Hinton does come around to the idea that machines like ChatGPT perform a sort of "intuitive" thinking based on analogies.  His example is ChatGPT generating a passage about a lost sock in the style of the Declaration of Independence.  In the passage, ChatGPT says "all socks are endowed with inalienable rights by their manufacturer".  Essentially, ChatGPT has made the analogy that God is to man as manufacturer is to sock.

I struggle with the idea of calling this "thinking", or even really understanding. Understanding words in relation to one another I don't feel is sufficient to say you understand language.  

There was an example I saw before with BERT that it completes the sentence "A robin is a" with "bird" and "A robin is not a" with "bird" as well.  The explanation was that the machine understood it needed a noun strongly associated with "robin", so it put in "bird".  It didn't really understand the context or have ready access to a list of things not like a robin.  

Of course, this is a hard problem for the machines; "negation" has been a thorny issue for a while.  ChatGPT seems to be confused when I ask it to complete "A robin is not a", but is ready with an answer to "A robin is a"

![ChatGPT robin problem]({{site.url}}/assets/chatgpt_robin.png){:height="50%" width="50%"}

This isn't a new idea - [general consensus](https://www.technologyreview.com/2020/07/20/1005454/openai-machine-learning-language-generator-gpt-3-nlp/) says these models don't "understand" language.  I can't find the article at the moment, but there was an interesting argument that the way these models communicate is intrinsically different from the way humans communicate.  And that makes sense to me.  These models "thinking" isn't the same as ours.  And why would we want it to be?  