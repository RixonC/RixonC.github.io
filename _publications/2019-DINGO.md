---
title: "DINGO: Distributed Newton-Type Method for Gradient-Norm Optimization"
collection: publications
permalink: /publication/2019-DINGO
venue: 'Advances in Neural Information Processing Systems 32 (NIPS 2019)'
date: 2019-12-10
---
<img src='/files/neurips-logo-new.svg' height="60" href='/'>

## Abstract
For optimization of a large sum of functions in a distributed computing environment, we present a novel communication efficient Newton-type algorithm that enjoys a variety of advantages over similar existing methods. Our algorithm, DINGO, is derived by optimization of the gradient's norm as a surrogate function. DINGO does not impose any specific form on the underlying functions and its application range extends far beyond convexity and smoothness. The underlying sub-problems of DINGO are simple linear least-squares, for which a plethora of efficient algorithms exist. DINGO involves a few hyper-parameters that are easy to tune and we theoretically show that a strict reduction in the surrogate objective is guaranteed, regardless of the selected hyper-parameters.

<a href="https://papers.nips.cc/paper/9146-dingo-distributed-newton-type-method-for-gradient-norm-optimization" class="btn">Paper</a>
<a href="/DINGO_NeurIPS_Poster.pdf" class="btn">Poster</a>
<a href="https://github.com/RixonC/DINGO" class="btn">Code</a>
<a href="https://arxiv.org/abs/1901.05134" class="btn">arXiv</a>
