---
layout: post
title:  Safe Exploration for Dynamical Systems
date: 2022-05-08 10:25:00
description: A quick summary of my work about globally safe exploration.
tags: [safe-learning, robotics, reinforcement-learning]
categories: research-post
---

Learning optimal control policies directly on physical systems is challenging.
Even a single failure can lead to costly hardware damage. Most existing
model-free learning methods that guarantee safety, i.e., no failures, during
exploration are limited to local optima. This work proposes GoSafeOpt as the
first provably safe and optimal algorithm that can safely discover globally
optimal policies for systems with high-dimensional state space. We demonstrate
the superiority of GoSafeOpt over competing model-free safe learning methods in
simulation and hardware experiments on a robot arm.

Access hardware results <a href="{{ "/GoSafeOpt/main_project.html" | relative_url }}"> here</a> and software results <a href="{{ "/GoSafeOpt/software_experiments.html" | relative_url }}"> here</a>. The paper is available <a href="https://www.sciencedirect.com/science/article/pii/S0004370223000681"> here</a>.
