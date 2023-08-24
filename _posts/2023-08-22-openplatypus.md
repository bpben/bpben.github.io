---
layout: post
title: Platypus - Quick, Cheap, and Powerful Refinement of LLMs
---

Hi all! In the interest of keeping up with the latest and greatest in LLMs, I've been collecting some articles and will hopefully have time to work through each.  Typically my process is to take notes as I read a paper and then summarize as a blog post.  I decided to take a page from...basically everyone else's book and start using ChatGPT to help me out here.

So for any post I'm using ChatGPT, i'll mention up front.  To be clear - I'm not wholesale copy-pasting from ChatGPT, I just haven't seen it produce anything ready for prime time without substantial editing.  But ChatGPT gives me the bones, which is pretty useful.

My prompt to generate this:
>Turn the following outline into a blog post.  The sub-bullets are relevant to the higher level information.  The top-level bullets should be the headings of the different sections, with relevant information below.  Try not to be too wordy

**Platypus: Quick, Cheap, and Powerful Refinement of LLMs**

[Paper link](https://arxiv.org/pdf/2308.07317.pdf)

This paper provides an overview of the process for generating the [Open-Platypus dataset](https://huggingface.co/datasets/garage-bAInd/Open-Platypus) and training the [Platypus series of models](https://huggingface.co/garage-bAInd) on top of the LLaMa-2 model.

#### Main Contributions of this Paper

1. **Open-Platypus Dataset**: This dataset is curated from public sources, with primarily human-generated content. This approach enables impressive model performance even with limited training time.

2. **Data Curation Process**: The Open-Platypus dataset is the product of data selection, where similar and duplicate entries are weeded out.

3. **Contamination Detection**: To prevent inclusion of test data in training data, a cosine-similarity-based tagging system has been used.

4. **Specialized LoRA Modules**: The Platypus model is based on Low Rank Adapters (LoRA) on top of LLaMa-2 and other LLMs.  This paper outlines details of that training.

#### Data Curation Process

The curation process is characterized by the following steps:

- **Cosine Similarity Filter**: Duplicates and similar entries are tagged by cosine similarity metric on the vectors resulting from SentenceTransformers.  Exact duplicates have been removed.

- **Emphasis on Verbosity**: In cases of non-exact duplicates, Open-Platypus leans towards verbose versions of answers.

- **Contamination Checks**: The process detects three distinct types of potential contamination between the test and training sets. These are flagged as part of the dataset.

    - **Exact Duplicate**: Identical entries.

    - **Gray Area**: Entries that might not be exact duplicates but cover similar knowledge.

    - **Similar but Different**: Entries that appear similar according to cosine similarity but are actually dissimilar.

#### Model Experiments

Open-Platypus employs the LLaMA-2 model as a foundation, fine-tuning it using LoRA adapters. This approach minimizes the number of parameters under adjustment.

The 70B parameter model outperforms other open-source models. Both the 13B and 70B parameter models surpass the base LLaMA-2 models.

#### Some thoughts (not GPT'd)
I found this paper interesting, but not particularly informative.  It seems like some performance hacking was being done.  I enjoy their attention to the underlying data, but their approach is fairly simplistic.  Cosine similarity + SentenceTransformers is not particularly new.  I would have been interested to see some experiments with their flagging and removal strategies, to really dig down into why, exactly, their model is doing better.

I'd be interested what people think of this article! I felt that I needed to do A LOT of editing to GPT's output.  Not sure if the end result is more useful than just the outline itself.