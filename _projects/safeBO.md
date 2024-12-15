---
layout: page
title: Tuning Legged Locomotion Controllers via Safe Bayesian Optimization
img: /assets/img/publication_preview/go1gosafeopt.gif
importance: 1
category: work
layout: distill
published: true
date: 2023-07-01 13:58:00
tags: [Reinforcement Learning, publication]
authors:
  - name: Daniel Widmer
  - name: Dong Ho Kang
    affiliations:
      name: CRL<d-footnote>Computational Robotics Lab</d-footnote>, ETH Zurich
  - name: Bhavya Sukhija
    url: "https://sukhijab.github.io"
    affiliations:
      name: LAS<d-footnote>Learning & Adaptive Systems Group</d-footnote> & CRL, ETH Zurich
  - name: Jonas Hübotter
    affiliations:
      name: LAS, ETH Zurich
  - name: Andreas Krause
    url: "https://las.inf.ethz.ch/krausea"
    affiliations:
      name: LAS, ETH Zurich
  - name: Stelian Coros
    url: "http://crl.ethz.ch/people/coros/index.html"
    affiliations:
      name: CRL, ETH Zurich
---

In this paper, we present a data-driven strategy to simplify the deployment of
model-based controllers in legged robotic hardware platforms. Our approach
leverages a model-free safe learning algorithm to automate the tuning of control
gains, addressing the mismatch between the simplified model used in the control
formulation and the real system. This method substantially mitigates the risk of
hazardous interactions with the robot by sample-efficiently optimizing parameters
within a probably safe region. Additionally, we extend the applicability of our
approach to incorporate the different gait parameters as contexts, leading to a safe,
sample-efficient exploration algorithm capable of tuning a motion controller for
diverse gait patterns. We validate our method through simulation and hardware
experiments, where we demonstrate that the algorithm obtains superior performance
on tuning a model-based motion controller for multiple gaits safely.


The paper is available <a href="https://arxiv.org/pdf/2306.07092.pdf"> here, </a> and below is a video demonstration.

<iframe width="560" height="315" src="https://www.youtube.com/embed/pceHWpFr3ng" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>



