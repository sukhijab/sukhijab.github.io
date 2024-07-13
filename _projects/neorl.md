---
layout: page
title: NEORL
img: /assets/img/publication_preview/nonepisodic_rl.jpeg
importance: 1
category: work
layout: distill
published: true
date: 2024-07-12 13:58:00
tags: [Reinforcement Learning]
authors:
  - name: Bhavya Sukhija
    url: "https://sukhijab.github.io"
    affiliations:
      name: LAS<d-footnote>Learning & Adaptive Systems Group</d-footnote> & CRL<d-footnote>Computational Robotics Lab</d-footnote>, ETH Zurich
  - name: Lenart Treven
    affiliations:
      name: LAS<d-footnote>Learning & Adaptive Systems Group</d-footnote> & ACL<d-footnote>Automatic Control Laboratory</d-footnote>, ETH Zurich
  - name: Florian Dörfler
    url: "https://people.ee.ethz.ch/~floriand/"
    affiliations:
      name: ACL<d-footnote>Automatic Control Laboratory</d-footnote>, ETH Zurich
  - name: Stelian Coros
    url: "http://crl.ethz.ch/people/coros/index.html"
    affiliations:
      name: CRL, ETH Zurich
  - name: Andreas Krause
    url: "https://las.inf.ethz.ch/krausea"
    affiliations:
      name: LAS, ETH Zurich
---

In this paper, we study the problem of nonepisodic reinforcement learning (RL) for nonlinear
dynamical systems, where the system dynamics are unknown and the RL agent
has to learn from a single trajectory, i.e., without resets. We propose Nonepisodic
Optimistic RL (NEORL), an approach based on the principle of optimism in
the face of uncertainty. NEORL uses well-calibrated probabilistic models and
plans optimistically w.r.t. the epistemic uncertainty about the unknown dynamics.
Under continuity and bounded energy assumptions on the system, we provide a
first-of-its-kind regret bound of $\mathcal{O}(\beta_T \sqrt{\Gamma_T T})$ for general nonlinear systems with
Gaussian process dynamics. We compare NEORL to other baselines on several
deep RL environments and empirically demonstrate that NEORL achieves the
optimal average cost while incurring the least regret.


The paper is available <a href="https://arxiv.org/pdf/2406.01175"> here.</a>



