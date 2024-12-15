---
layout: page
title: Gradient-based trajectory optimization with learned dynamics
img: /assets/img/publication_preview/spot_gradientbased.gif
importance: 1
category: work
layout: distill
published: true
date: 2023-2-21 13:58:00
tags: [Robotics, publication]
authors:
  - name: Bhavya Sukhija
    url: "https://sukhijab.github.io"
    affiliations:
      name: LAS<d-footnote>Learning & Adaptive Systems Group</d-footnote> & CRL<d-footnote>Computational Robotics Lab</d-footnote>, ETH Zurich
  - name: Nathanael Köhler
  - name: Miguel Zamora
    affiliations:
      name: CRL, ETH Zurich
  - name: Simon Zimmermann
    affiliations:
      name: CRL, ETH Zurich
  - name: Sebastian Curi
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

Trajectory optimization methods have achieved an exceptional level of performance on real-world robots in recent years. These methods heavily rely on accurate analytical models of the dynamics, yet some aspects of the physical world can only be captured to a limited extent. An alternative approach is to leverage machine learning techniques to learn a differentiable dynamics model of the system from data. In this work, we use trajectory optimization and model learning for performing highly dynamic and complex tasks with robotic systems in absence of accurate analytical models of the dynamics. We show that a neural network can model highly nonlinear behaviors accurately for large time horizons, from data collected in only 25 minutes of interactions on two distinct robots: (i) the Boston Dynamics Spot and an (ii) RC car. Furthermore, we use the gradients of the neural network to perform gradient-based trajectory optimization. In our hardware experiments, we demonstrate that our learned model can represent complex dynamics for both the Spot and Radio-controlled (RC) car, and gives good performance in combination with trajectory optimization methods.

See video  <a href="http://crl.ethz.ch/videos/spot_icra_compressed_final.mp4"> here.</a> The paper is available <a href="https://arxiv.org/pdf/2204.04558.pdf"> here.</a>


