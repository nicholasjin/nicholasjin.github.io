---
title: 'On the subjective nature of $p$-values'
date: 2020-03-27
permalink: /posts/subjective-pvalues/
tags:
  - statistics
---

Welcome back to Esoteria! Today we'll be discussing whether or not frequentist $p$-values encode subjective information. We'll be following an example from Chapter 37 of [Information Theory, Inference, and Learning Algorithms](http://www.inference.org.uk/itprnn/book.pdf) by David J.C. MacKay.

# Coin Flipping
Consider the following scenario. Bob, a frequentist, observes Alice flip the same coin  $N=12$ times, and records the result:

`HHHTHHHHTHHT`

Is this coin biased in favor of heads?

## Naive approach
Bob declares the number of heads $N_H$ to be the random variable of interest. He assumes the null hypothesis that the coin is fair: $\mathcal H_0: p_H = p_T = 0.5$. Then the probability that Alice flipped 3 or fewer heads is
\begin{align}
P(N_H \le 3 | N=12, \mathcal H_0) =& \sum_{N=0}^3 C(N, N_H) \left(\frac 12\right)^{N} = 0.07
\end{align}
where $C(n,k)$ denotes "$n$ choose $k$". Bob concludes that at a 5% significance level, there is no significant evidence that our coin is biased towards $H$. All of this is fairly standard frequentist treatment on the fairness of flipped coins.

## But wait there's more!
Alice quickly looks over Bob's calculation and tells him that the random variable in the experiment was not in fact $N_H$. Her experimental setup was to flip the coin until she arrived at a third tails, counting the number of flips $N$. Given this information, Bob needs to compute a different likelihood, namely: what is the likelihood that the first $N-1$ tosses contained exactly $N_H - 1$ heads, and then Alice flipped a heads:
\begin{align}
P(N | \mathcal H_0, N_H) = C(N-1, N_H - 1) \left(\frac 12\right)^{N}
\end{align}
In our case, with $N = 12$ and $N_H = 3$, Bob gets:
\begin{align}
P(N \ge 12 | \mathcal H_0, N_H=3) = 0.03
\end{align}
So Bob concludes: at the 5% significance level, given that he now knows the experimental setup in more detail, he can reject the possibility that the coin was fair and conclude that the coin was biased in favor of heads.

How can Bob arrive at two different conclusions given that he observed the same data? We might believe one of two things:
1. Alice's stopping rule (stop on the third tails) biased the experiment in some manner, and is relevant to our beliefs about the fairness of the coin.
2. We should perhaps use a more coherent method of assessing significance, one that doesn't depend on the stopping rule.

# The first view is, frankly, arrant nonsense
There is *no reason* that Bob's belief in the fairness of this coin should depend on irrelevant information, such as when Alice arbitrarily decided to stop the experiment.

Consider the following. Eve is surreptitiously watching the experiment as it proceeds, updating on a flip-by-flip basis the number of flips $N$ and the number of heads $N_H$. Each time the coin is flipped, Eve does the inference in her head about whether the coin is fair or not. Should Eve's belief in the coin's fairness depend on whether or not Alice is going to flip the coin again?

We can go further: consider that as this is all happening, after the twelfth flip, Mallory drops by and confiscates the coin. She announces that in no universe would she ever have allowed the 13th flip, and smugly tells Bob to recompute his $p$-value.

# Conclusion
Sequential analysis (frequentist analysis with variable sample size) is very real, and there is no shortage of literature expanding upon it. It is applied in a number of real world contexts, such as in clinical trials and signal processing. I don't know enough statistics to resolve this conundrum, but I do believe that all the observers should ultimately agree on the likelihood of observing an event, and I definitely don't believe that the choice to stop an experiment should affect our inference. More things to read about in the future, I suppose!

Thanks for reading!
