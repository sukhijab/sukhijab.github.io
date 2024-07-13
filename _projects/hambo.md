---
layout: page
title: Hallucinated Adversarial Control for Conservative Offline Policy Evaluation
img: /assets/img/publication_preview/HAMBO.png
importance: 1
category: work
layout: distill
published: true
date: 2023-02-01 13:58:00
tags: [Reinforcement Learning, publication]
authors:
  - name: Jonas Rothfuss*
    affiliations:
      name: LAS, ETH Zurich
  - name: Bhavya Sukhija*
    url: "https://sukhijab.github.io"
    affiliations:
      name: LAS<d-footnote>Learning & Adaptive Systems Group</d-footnote> & CRL<d-footnote>Computational Robotics Lab</d-footnote>, ETH Zurich
  - name: Tobias Birchler*
  - name: Parnian Kassraie
    affiliations:
      name: LAS, ETH Zurich
  - name: Andreas Krause
    url: "https://las.inf.ethz.ch/krausea"
    affiliations:
      name: LAS, ETH Zurich
---

We study the problem of conservative off-policy evaluation (COPE) where given an offline dataset of environment interactions, collected by other agents, we seek to obtain a (tight) lower bound on a policy’s performance. This is crucial when deciding whether a given policy satisfies certain minimal performance/safety criteria before it can be deployed in the real world. To this end, we introduce HAMBO, which builds on an uncertainty-aware learned model of the transition dynamics. To form a conservative estimate of the policy’s performance, HAMBO hallucinates worst-case trajectories that the policy may take, within the margin of the models’ epistemic confidence regions. We prove that the resulting COPE estimates are valid lower bounds, and, under regularity conditions, show their convergence to the true expected return. Finally, we discuss scalable variants of our approach based on Bayesian Neural Networks and empirically demonstrate that they yield reliable and tight lower bounds in various continuous control environments.


The paper is available <a href="https://proceedings.mlr.press/v216/rothfuss23a/rothfuss23a.pdf"> here. </a> 


\*equal contribution.
