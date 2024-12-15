---
layout: page
title: Sim-FSVGD
img: /assets/img/publication_preview/racecar_simfsvgd.gif
importance: 1
category: work
layout: distill
published: true
date: 2024-07-12 13:58:00
tags: [Reinforcement Learning, Robotics, publication]
authors:
  - name: Jonas Rothfuss*
    affiliations:
      name: LAS<d-footnote>Learning & Adaptive Systems Group</d-footnote>, ETH Zurich
  - name: Bhavya Sukhija*
    url: "https://sukhijab.github.io"
    affiliations:
      name: LAS & CRL<d-footnote>Computational Robotics Lab</d-footnote>, ETH Zurich
  - name: Lenart Treven*
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

We present SIM-FSVGD for learning robot dynamics from data. As opposed to traditional methods, SIM-FSVGD leverages low-fidelity physical priors, e.g., in the form of simulators, to regularize the training of neural network models. While learning accurate dynamics already in the low data regime, SIM-FSVGD scales and excels also when more data is available. We empirically show that learning with implicit physical priors results in accurate mean model estimation as well as precise uncertainty quantification. We demonstrate the effectiveness of SIM-FSVGD in bridging the sim-to-real gap on a high-performance RC racecar system. Using model-based RL, we demonstrate a highly dynamic parking maneuver with drifting, using less than half the data compared to the state of the art.


The paper is available <a href="https://arxiv.org/pdf/2306.07092.pdf"> here, </a> and below is a video demonstration.

<iframe width="560" height="315" src="https://crl.ethz.ch/videos/draft_iros_low_res.mp4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

\*equal contribution, listed in alphabetical orders.


