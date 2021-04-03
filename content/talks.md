---
title: "Talks I have given"
---

## Monte Carlo Markov Chains and PyMC3

The talk given at Myntra starts with an introduction to the Bayesian Linear Regression. I explain analytic solution and also introduce PyMC3 based solution. Then I proceed to explain Markov Chains that were used by PyMC internally. In the process Metropolis-Hastings and Gibbs chain are explained. The notebook is available [here](https://github.com/DhruvPatel01/myntra_talks/blob/master/bayesian_intro_with_pymc.ipynb). For proofs there is a [supplementary pdf](https://github.com/DhruvPatel01/myntra_talks/blob/master/mcmc.pdf). 

## On Double Precision Floating Points

In this talk, I introduced subtleties of using floating points to the audience. Talk starts with a classic mistake done in the Patriot Missile system, which caused the lives of 28 soldiers. Then I introduce a naive/intuitive algorithm of computing variance online (i.e. in one pass) and dangers of it. While explaining what caused the issues in the naive algorithm, I explain how different programming languages might give different results while working with floats(doubles). I then explain the Achilles' heel of floating point arithmetic called catastrophic calculation, and how to avoid it. Talk concludes with Welford's algorithm on computing variance online. Slides are available [here](/slides/floats.slides.html).

