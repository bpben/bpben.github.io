---
layout: post
title: Some thoughts on job searches
author: ben
image: assets/images/20240610.png
tags: []
categories: [ updates, articles ]
---

I recently had a very successful end to a particularly stressful job search and I thought it might be useful to share some of my experiences.

I don't need to tell you all that we're pretty up there in hype cycle land (from Gartner):

[![]({{site.url}}/assets/20240528_hype_23.png){:height="75%" width="75%"}]({{site.url}}/assets/20240528_hype_23.png)

Which of course has come along with declarations that both [all jobs will be AI](https://edisonandblack.com/pages/over-97-million-jobs-set-to-be-created-by-ai.html) and [all jobs will be replaced by AI](https://www.bbc.com/news/technology-65102150).  But this comes at a kind of strange time when many major tech companies have been [laying off large portions of their staff](https://techcrunch.com/2024/05/28/tech-layoffs-2023-list/).  

So which is it? Is this boom or bust times?

### The landscape of AI jobs
Long gone are the years of [data scientists being sexy](https://www.hiringlab.org/2019/01/17/data-scientist-job-outlook/), as Vicki Boykis [has lamented](https://vickiboykis.com/2019/02/13/data-science-is-different-now/).  A proliferation of bootcamps and certificate programs has churned out waves of candidates with AI, writ large, credentials.  This matched [the rising demand that peaked in 2022](https://www.hiringlab.org/2024/03/14/march-2024-us-labor-market-update/), but since then there have been fewer jobs available in the field.  And technology hasn't exactly stood still.

Data science has [become more focused on implementation](https://medium.com/@emmanuelameisen/most-impactful-a-i-trends-of-2018-the-rise-of-ml-engineering-4b1c704f263c), leading to a [rise in the the number of postings for "machine learning engineers"](https://www.linkedin.com/pulse/humans-only-rising-demand-machine-learning-engineers-michiel-klompen/).  As with Data Scientists, this position is also vaguely defined, but I've seen it best described as a kind of ["bridge" between the DS and Software Engineer worlds](https://moldstud.com/articles/p-machine-learning-engineering-impacts-on-the-job-market-and-economy).  It also happens to be, on average, the highest paying position in tech.

Why this change? It likely comes from many things, but what I've noticed is an increasing focus on [how much of a ML system exists outside of the model development itself](https://proceedings.neurips.cc/paper_files/paper/2015/file/86df7dcfd896fcaf2674f757a2463eba-Paper.pdf).  When a system moves out of the lab, considerations like scalability, consistency and security become the determining factors for success.  I always think of the [Netflix prize](https://www.wired.com/2012/04/netflix-prize-costs/) story here - where the company paid $1 million for an algorithm it couldn't use due to its complexity.  Today, recommendation engines are usually a combination of many different systems with [multiple layers of failsafes](https://netflixtechblog.medium.com/recsysops-best-practices-for-operating-a-large-scale-recommender-system-95bbe195a841).  

Some of the technologies I see in many ML Engineer and Data Science roles:
- Experience with cloud architecture (e.g. AWS, GCP)
- DS workflow development (e.g. Airflow, Kubeflow)
- General familiarity with containerization and CI/CD workflows

This goes along with the usual experience with machine learning, statistics and coding (e.g. python, SQL).

### What you can (and cannot) do

One of the main inspirations for this post came from [Eric Ma's discussion about what a candidate can control in about the interview process](https://ericmjl.github.io/blog/2021/11/28/what-candidates-can-and-cannot-control-in-their-job-hunt/).  To the extent budget considerations or pre-existing preferences impact the process, the candidate has very little control or insight.  I know at least one of the opportunities I was most excited about ended up having to be put on pause because of budget.  I'm sure there were others that had similar issues which took the form of delays or rejections.  

Eric puts the portion of the process that _is_ in the candidate's control at 30-40%.  This is not a small portion and he encourages candidates to focus on building out a portfolio of interesting applications that employ sensible engineering practices.  I feel this links back to what I said in the previous section; hiring managers (like Eric) are looking for engineering skills along with methods chops.  

I ensured that, as a candidate, I had a set of projects to point to that demonstrate my experience dealing with the thorniness of implementation.  This is because I know that when I've been in the hiring manager position, the focus of my questions is around the goals of the projects, the issues encountered and how the final approach was built around these obstacles.  

If a candidate has mostly worked with clean datasets and a simple set of requirements (e.g. improving performance on standard benchmarks), it puts them in a particular category of practitioner, in my mind.  For some positions, that's fine.  But having no engineering exposure is likely not going to make a candidate particularly appealing.

### Final thoughts
Personally, I found this search one of the hardest yet.  I imagine there was a lot of competition for a narrow set of opportunities, but I also imagine hiring managers struggling under a set of urgent but poorly-specified demands around generative AI.  I found it helpful to outline what, specifically, I was looking for in a new role and assign each of those criteria a weight.  If an opportunity was above a particular score - it's worth pursuing.  If not - well, I had the luxury of not being in a particular rush.

I want to note that my experience is different from a lot of other candidates out there.  As mentioned, I have a lot of privilege in this process.  So as with all of my advice - YMMV.

More to come!