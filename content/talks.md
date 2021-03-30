---
title: "Talks I have given"
---

## Monte Carlo Markov Chains and PyMC3

The talks given at Myntra starts with an introduction to Bayesian Linear Regression. I explain analytic solution and also introduce PyMC3 based solution. Then I proceed to explain Markov Chains that were used by PyMC internally. In the process Metropolis-Hastings and Gibbs chain were explained. The notebook is available [here](https://github.com/DhruvPatel01/myntra_talks/blob/master/bayesian_intro_with_pymc.ipynb). For proofs there is [supplementary pdf](https://github.com/DhruvPatel01/myntra_talks/blob/master/mcmc.pdf). 

## On Double precision floating points

In this talk, I introduced subtleties of using floating points to the audience. Talk starts with classic mistake done in Patriot Missile system, which caused life of 28 soldiers. Then I introduce naive/intuitive algorithm of computing variance online (in one pass), and dangers of it. While explaining what caused the issues in naive algorithm, I explain how different programming languages might give different results while working with floats. I then explain the Achilles' heel of floating point calculation called catastrophic calculation, and how to avoid it. Talks concludes with Welford's algorithm on computing variance online. Slides are available [here](/slides/floats.slides.html).

