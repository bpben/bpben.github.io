---
layout: post
title: Adventures in spatial analysis
---

Related to my [project](https://github.com/Data4Democracy/boston-crash-modeling) with [Data 4 Democracy](https://medium.com/data-for-democracy), I've started compiling some scripts for spatial analysis.  Particulary interesting (at least to me) is a bit of TSPLIB I adapted for use with the awesome [osmnx library](http://geoffboeing.com/2016/11/osmnx-python-street-networks/).  

[Check it out](https://github.com/bpben/spatial_tools).

This is actually some synergy between the D4D project and the health violation prediction model I worked on.  The idea here is to maximize "risk" coverage and minimize distance.  Ideally, a reinforcement learning project.  For now, though, to maintain my sanity, I'm having it as a single-agent problem.