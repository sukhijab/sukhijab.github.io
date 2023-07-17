---
layout: page
title: Optimistic Active Exploration of Dynamical Systems
img: /assets/img/publication_preview/opax_intro.png
importance: 1
category: work
layout: distill
published: true
date: 2023-06-21 13:58:00
tags: [Reinforcement Learning, publication]
authors:
  - name: Bhavya Sukhija
    url: "https://sukhijab.github.io"
    affiliations:
      name: LAS<d-footnote>Learning & Adaptive Systems Group</d-footnote> & CRL<d-footnote>Computational Robotics Lab</d-footnote>, ETH Zurich
  - name: Lenart Treven
    affiliations:
      name: LAS, ETH Zurich
  - name: Cansu Sancaktar
    affiliations: 
      name: Max Planck Institute for Intelligent Systems, Tübingen
  - name: Sebastian Blaes
    affiliations:
      name: Max Planck Institute for Intelligent Systems, Tübingen
  - name: Stelian Coros
    url: "http://crl.ethz.ch/people/coros/index.html"
    affiliations:
      name: CRL, ETH Zurich
  - name: Andreas Krause
    url: "https://las.inf.ethz.ch/krausea"
    affiliations:
      name: LAS, ETH Zurich
---

Reinforcement learning algorithms commonly seek to optimize policies for solving one particular task. How should we explore an unknown dynamical system such that the estimated model allows us to solve multiple downstream tasks in a zero-shot manner? In this paper, we address this challenge, by developing an algorithm -- OPAX -- for active exploration. OPAX uses well-calibrated probabilistic models to quantify the epistemic uncertainty about the unknown dynamics. It optimistically -- w.r.t. to plausible dynamics -- maximizes the information gain between the unknown dynamics and state observations. We show how the resulting optimization problem can be reduced to an optimal control problem that can be solved at each episode using standard approaches. We analyze our algorithm for general models, and, in the case of Gaussian process dynamics, we give a sample complexity bound and show that the epistemic uncertainty converges to zero. In our experiments, we compare OPAX with other heuristic active exploration approaches on several environments. Our experiments show that OPAX is not only theoretically sound but also performs well for zero-shot planning on novel downstream tasks.


The paper is available <a href="https://arxiv.org/pdf/2306.12371.pdf"> here </a> and below is a small video demonstration of our simulation results.

<div class="row mt-3">
        {% include video.html path="assets/video/opax_videos.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
</div>
<div class="caption">
    Video demonstration of OPAX.
</div>



