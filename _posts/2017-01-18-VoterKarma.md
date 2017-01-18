---
layout: post
title: VoterKarma app
---

Hello adoring public.  This past weekend I attended the [Debug Politics Hackathon](https://www.facebook.com/debugpolitics/), a hackathon dedicated to addressing issues with politics, voting and the rhetoric around both.  It was a really fascinating experience and I definitely recommend it to anyone interested in these issues.

An awesome team and I aimed to address the issue of voters being left by the wayside by political campaigns.  One of the troubling outcomes of [increasingly data-driven politics](http://www.motherjones.com/politics/2012/10/sasha-issenberg-goes-inside-21st-century-campaign) is that certain voters receive little attention from campaigns if models predict they're not likely to vote.  This is particularly problematic as voter turnout varies by [age, race and income](http://www.fairvote.org/what_affects_voter_turnout_rates).  This targeting is going on without voter knowledge.  The only evidence they'd get is that they see very little communication from their elected officials.

To attempt to address this information gap, we developed an application called [VoterKarma](http://voterkarma.herokuapp.com/), which allows NY voters to see a predicted probability that they will participate in upcoming elections.  Our aim is to inform, but also motivate people that might be unhappy with their scores to go out and get more involved.

The plan is to expand this into an API that voters and campaigns can utilize.  I'm also doing some work improving the model to reflect more of the modern ML techniques that a lot of campaigns are making use of.

Feel free to check out [the code](https://github.com/DerekKaknes/voter_karma).  And keep up to date with the [API](https://github.com/DerekKaknes/nycvoterfile)!