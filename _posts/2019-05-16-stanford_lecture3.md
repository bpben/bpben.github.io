---
layout: post
title: Stanford CS230 Lecture 3 - Full-cycle deep learning projects
---


So we’re back with [Andrew Ng](https://twitter.com/AndrewYNg) in this lecture to go over, at a pretty high level, the steps and considerations of a complete Deep Learning project.  Again, all of the materials come from the course unless otherwise noted

[Video](http://onlinehub.stanford.edu/cs230/181010-cs230-720)

Andrew starts by outlining the steps of a Deep Learning (or ML generally) project or application:
- Get data
- Design model
- Train model
- Test model
- Deploy
- Maintain
- QA process (not really a step in itself)

He specifically mentions that a lot of this is not sequential.  A lot of the time it’s about iterating on any of the steps to get to a really good final product.  An example he gives is when you’re thinking about what is involved in getting data for the project, it makes sense to just go with the minimal set as even that start will give you some idea what kind of models are appropriate and what other data might be necessary.

The example he keeps going back to is the concept of a voice-activated device.  In gathering data, you might want a perfect, representative audio dataset, but sometimes it might make sense to get a convenience sample and then use the issues you find fitting a model to that to guide the expansion of the data gathering effort.

Andrew also offers some advice for thinking about what makes a good project:
Interest: Pretty obvious, you should be interested in what you’re doing
Data availability: DL projects work best with large datasets, so it’s a major consideration
Domain knowledge: Andrew points out that people with domain knowledge tend to have a lot to offer to any DL project targeting that domain.  For example, someone with a background in biology would definitely have an advantage in applying DL to a biology-related problem
Utility: How useful would the solution be?
Feasibility: Is it even possible?

The rest of the lecture focuses on the Deploy and Maintain part of the project.  His reasoning is that the other parts are covered by a lot of other lectures/courses/etc.  He focuses on the voice-activated device again, explaining that deploying a voice activation system typically involves two technologies; A Voice Activity Detection (VAD) model and a model to detect what the user’s request is.  The reason is because the devices themselves tend to not have much in the way of computational power, most of that capacity is housed in the Cloud.  The only purpose of the VAD is to detect if there’s something worth sending to the model in the Cloud.

For the purposes of VAD, sometimes a non-ML approach works best (e.g. a hardcoded volume threshold).  These approaches are sometimes even more robust than a model, as models are fit to the data they’re trained on.  So, for example, if a device gets deployed in another country, it may not be able to detect voice activation in another language or another accent.

This leads into the “Maintain” step.  A model’s performance needs to be continuously tracked, especially if it’s going to be deployed in a new setting.  Just because you have a model that works great in the US doesn’t mean that performance is going to transfer over to the UK, for example.

This lecture was a bit light in my view, but I do appreciate the attention Andrew gives to the broad view of a project.  I find the iterative approach a really valuable one, as I often find issues with the data, the model of choice and, very frequently, the output.  For example, one project I worked on aimed to estimate Click-through Rate (CTR) from past campaign performance data.  After a lot of data munging and model iteration, we came out with a pretty performant model that was, on average, only off by a fraction of a percent.  When we presented this model that could predict campaign performance, the stakeholders were not as excited as we hoped.

The reason? CTR was an important measure for the business.  But more important was the actual number of leads (i.e. potential customers) generated.

It wasn’t a waste, we had done a lot of work with the data to generate informative features for the lead-prediction effort.  But imagine if we had spent another few weeks training a full-on Neural Network to estimate CTR? So I’m definitely on board with Andrew’s idea of iterating between the steps and checkpointing progress.

Till next time!