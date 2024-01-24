---
layout: post
title: Fine-tuning ChatGPT for Dermatology
categories: [ Dermatology, tutorial, LLM ]
image: assets/images/20240124.png
---

The main goal of my project with dermatology tech startup [Melatech](https://melatech.io/) is to build a prototype clinical note generation engine.  The notes generated need to have the following qualities:

1. Contain specific, accurate information
2. Have a "conversational tone" similar to that of the consulting dermatologist

For 1 - this seems subject to the input; if we provide useful information to the model along with a well-designed input prompt, it should be able to generate a useful output.  We may want to combine this with something like [RAG]({{site.url}}/friend_rag_3), but that's a topic for a different post.

For 2 - this is more of a [style transfer](https://blog.fastforwardlabs.com/2022/03/22/an-introduction-to-text-style-transfer.html) issue in my mind.  We want to replace the psuedo-formal tone of a model like ChatGPT to better match that of the dermatologist.  If you read my [fine-tuning post]({{site.url}}/friend_ft_4), you'll maybe start thinking that this is a job for fine-tuning.

So let's dive into developing this "note generator" engine.  I'll walk us through the data, the approach, the results and our next steps.

### The skin-ny on the data

While I can't share the Melatech dataset, I can give you an idea of what we have in it:

- The General Practitioner's (GP) diagnosis (categorical)
- The consulting dermatologist's diagnosis (categorical) and notes (text)
- Proposed next steps (categorical)

As I mentioned in the previous post, the cases come from referrals for consultation from GPs. I was given a limited set of information in order to maintain patient protection, but it gives me enough to start experimenting.  

A clinical note tends to include:
- An assessment of the case, pointing out details in the image (and often about its quality)
- Agreement or disagreement with the GP with rationale
- "Encouragement"; thanking the GP for their input and observations
- Suggested next steps

One thing I want to note here that I haven't mentioned before.  The clinical notes are all in Danish.  So this is a non-English corpus we're dealing with.  I don't change much about my process to account for this since research shows that performance for top-line models [doesn't vary much for *certain language families*](https://arxiv.org/abs/2304.04675)[^2].  My approach is to try and keep everything in Danish (including the prompt).  Examples I'll be showing here are translations back to English, so some of the language oddities might be artifacts of the translation.

Keep all of the above in mind for the next section.  We'll be building from a limited set of information and a general note structure. 

### Fleshing out the prompt

Prompt engineering is an interesting subject and a job that can either make you [$300k a year](https://time.com/6272103/ai-prompt-engineer-job/) or [$85k a year](https://medium.com/@ErikH2000/sorry-i-dont-think-prompt-engineer-is-a-real-job-bcf5577a2d16), depending on who you ask.  The power of this kind of work comes (in my opinion) from the emergent properties of LLMs (as described in [a previous post]({{site.url}}/categories.html#llm-app-series)).  Particularly - "In Context/Zero-Shot Learning"[^1], where the LLM's output can be modified without changing any of the numbers under the hood. 

What goes into a good prompt? This might be a whole separate post, but [OpenAI provides a set of tips](https://platform.openai.com/docs/guides/prompt-engineering/six-strategies-for-getting-better-results) that are pretty helpful.  Since we're using their model, it might make sense to listen up.

- Include details in your query to get more relevant answers
- Ask the model to adopt a persona
- Use delimiters to clearly indicate distinct parts of the input
- Specify the steps required to complete a task
- Provide examples
- Specify the desired length of the output

You can read each in more detail on the link above. The current version of the prompt and the one we used in the next experiments is as follows:

> You are a doctor reviewing a patient record.  Another doctor has diagnosed the patient as having _X_, you have diagnosed the patient as having _Y_. Write a short note to the other doctor that includes:  - Justification of your diagnosis if it differs, otherwise agreement. - Recommendation of the following action: _Z_. Tone is professional and respectful. Do not include salutation. Respond only with a single paragraph.  Respond in Danish.

You'll see I took a few tips from OpenAI here:

- Persona: "A doctor reviewing a patient record"
- Delimiters to specify the parts of the note
- Details about the output, structure and length

X, Y and Z here are stand-ins for the data elements described above.  On passing the data to the OpenAI endpoints, I fill in these details from the case.

Interestingly, when the prompt specified asked for a note from one doctor to another, the LLM included salutations (e.g. “dear colleague”).  This suggests the LLM has learned the “form” of correspondence and it's hard to quit that habit.  Even this specification doesn't always stop it from including them.

So let's look at some output.

### Pore-ing over the results

Thank ChatGPT for that one.

Generally, the output from GPT 3.5 is pretty generic, which makes sense since I'm giving it pretty limited information.  Here's an example (translated to English) with the following data inputs:

- GP Dx: Seborrheic keratosis/Lentigo solaris
- Consulting Dx: Nevus
- Follow up: Image follow-up

> After reviewing the patient's journal and examination, I would like to present my assessment of the diagnosis. I am not convinced of the diagnosis of Seb. keratosis/Lentigo solaris and believe that the patient is actually suffering from Nevus. Upon closer inspection, there are characteristic features found at the site, including asymmetry and color variation, which indicate Nevus. I recommend taking pictures of the lesion for follow-up purposes, as this may be helpful in monitoring any changes over time.

This is sensible, but there's some awkwardness to the language (e.g. "taking pictures").  GPT 4 actually did a much better job here:

> After a thorough review of the patient's journal and my own clinical assessment, I have come to the conclusion that our patient may potentially have a Nevus rather than Seb. keratosis/Lentigo solaris. Although both conditions present with similar symptoms, I have noted some characteristic features of Nevus such as pigmentation and size, which lead me to this diagnosis. In my opinion, it would be in the patient's best interest to undergo a diagnostic imaging follow-up to confirm this diagnosis and guide our treatment.

In general, GPT 4 had a much more organized and coherent style.  But it is [50x the cost of GPT3.5 so...](https://github.com/ray-project/llm-numbers).

The tone here is professional, but it's fairly generic.  I can't share an actual clinical note, but they tend to focus on specific elements and have a more varied, conversational structure.  As mentioned above, I think of this as a style transfer issue.  So let's get into that.

### The differences are more than skin deep

Some may say these skin puns are getting old.  I disagree.  They just have a few wrinkles.

Following a similar workflow as in my [fine-tuning post]({{site.url}}/friend_ft_4), I fine-tuned the GPT 3.5 model to output notes that better matched the style of the training set.  

Overall, the result was a note that sounded more like the consulting dermatologist, but was often garbled and included "hallucinated" (false) information.

For the example above, the output of the fine-tuned model was:

> I think it looks like a benign nevus. You can clearly see that the uptake of the \<redacted, potentially sensitive\> virus is difficult, as it's a general diffuse change (skin field effect) and there are no 'confluent and reticular pattern' elements affected by the virus \<redacted, potentially sensitive\> Therefore, I would like to ask her to take a picture every 2-3 months and send it for further examination. \<truncated\>

This is kind of all over the place, though it does have some of the elements requested in the prompt.  The style of this one, and others, has a more "realistic" tone to it.  It's hard to describe, but one of the characteristics of the notes is "encouragement" - the dermatologist telling the GP they did a good job.  You can see this in another example from the fine-tuned model:

> The patient has a seborrhoeic keratosis, which is characterized by a typical "horn-like" white collar on the border of the lesion, which helps to differentiate it from follicular keratoses. \<truncated\> I recommend presenting the patient with the alteration and performing a biopsy after 1-3 months to evaluate if there has been any growth or market change. It is a very nice LED you have made!

Very interesting! I'd say that the style transfer is at least somewhat successful, though at a cost of the generation getting away from the prompt and the facts of the case.  Compare that with the base models, which keep to the prompt, but are pretty generic and simple in their output.

There's a couple next steps we're planning to take here
- Including more "facts" to the prompt to enable more useful generation
- Experimenting with the style transfer as potentially a post-processing step to a more factual note

More to come!

[^1]: I've heard zero shot and in-context learning used interchangeably, which may reflect some confusion about the mechanisms here.  As I understand - In-context learning is a broader category that includes zero shot and few shot.  The main idea is that the generation behavior is changed just by changing the prompt.  Nothing under the hood gets changed, as in the fine-tuning paradigm we explore here.

[^2]: Without a doubt, language technology performs best in [English and western languages](https://www.ruder.io/state-of-multilingual-ai/).  Language disparities in NLP is not something I want to downplay.  I cover this issue more deeply in my [presentation on ethics in NLP](https://docs.google.com/presentation/d/1aoI7xMvg76lOZ-2F9vQEsfa2W_c9Dd4AcgsPJoI30cA/edit?usp=sharing).
