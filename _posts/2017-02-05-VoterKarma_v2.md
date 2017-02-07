---
layout: post
title: VoterKarma app now with more boost
---

The team and I from [Debug Politics](https://www.facebook.com/debugpolitics/) are still working on updating the [VoterKarma app](http://voter-karma.herokuapp.com/score/new).

For my part, I did some testing of different classifiers (i.e. Logistic Regression, Random Forest and XGBoost).  That code is [here](https://github.com/DerekKaknes/voter_karma/blob/master/voterkarma_testing.ipynb).  

XGBoost I hadn't used before, but it's easy to incorporate it into the CV process in sklearn.  XGBoost definitely outperformed Random Forest and Logistic Regression, so we'll be using it for our scoring going forward.

An interesting thing I learned looking at the NYC voterfile is how stark the difference is in ages between those who vote and those who don't.  Check it out:

![](https://raw.githubusercontent.com/bpben/bpben.github.io/master/resources/vote_by_age.png)

For the presidential, it's not so stark, but for local elections, the distribution of ages among voters is much more top-heavy than non-voters.  It's [not a new finding](https://www.census.gov/prod/2014pubs/p20-573.pdf) but I found the difference between local and national elections pretty surprising.  
