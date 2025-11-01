---
layout: page
title: MaxInfoRL - Boosting exploration in reinforcement learning through information gain maximization
img: /assets/img/publication_preview/humanoid_walk_learning.gif
importance: 1
category: work
layout: distill
published: true
date: 2025-02-14 13:58:00
tags: [Reinforcement Learning, publication]
authors:
  - name: Bhavya Sukhija
    url: "https://sukhijab.github.io"
    affiliations:
      name: LAS<d-footnote>Learning & Adaptive Systems Group</d-footnote> & CRL<d-footnote>Computational Robotics Lab</d-footnote>, ETH Zurich
  - name: Stelian Coros
    url: "http://crl.ethz.ch/people/coros/index.html"
    affiliations:
      name: CRL, ETH Zurich
  - name: Andreas Krause
    url: "https://las.inf.ethz.ch/krausea"
    affiliations:
      name: LAS, ETH Zurich
  - name: Pieter Abbeel
    url: "https://people.eecs.berkeley.edu/~pabbeel/"
    affiliations:
      name: RLL<d-footnote>Robot Learning Lab</d-footnote>, UC Berkeley
  - name: Carlo Sferrazza
    url: "https://sferrazza.cc"
    affiliations:
      name: RLL, UC Berkeley
---

Paper: <a href="https://proceedings.iclr.cc/paper_files/paper/2025/file/bd996108ed57d388866ca6deb7acf6cb-Paper-Conference.pdf"> ICLR 2025.  

Implementation: [Jax][maxinfo_jax], [PyTorch][maxinforl_sb3].

<img src="/assets/slides/maxinforl/teaser.gif" width="720"/>


## Abstract

Reinforcement learning (RL) algorithms aim to balance exploiting the current best strategy with exploring new options that could lead to higher rewards. Most common RL algorithms use undirected exploration, i.e., select random sequences of actions. Exploration can also be directed using intrinsic rewards, such as curiosity or model epistemic uncertainty. However, effectively balancing task and intrinsic rewards is challenging and often task-dependent. In this work, we introduce a framework, MaxInfoRL, for balancing intrinsic and extrinsic exploration. MaxInfoRL steers exploration towards informative transitions, by maximizing intrinsic rewards such as the information gain about the underlying task. When combined with Boltzmann exploration, this approach naturally trades off maximization of the value function with that of the entropy over states, rewards, and actions. We show that our approach achieves sublinear regret in the simplified setting of multi-armed bandits. We then apply this general formulation to a variety of off-policy model-free RL methods for continuous state-action spaces, yielding novel algorithms that achieve superior performance across hard exploration problems and complex scenarios such as visual control tasks.

## Problem Setting

We study the problem of online reinforcement learning (RL), where the agent interacts with the environment and uses the data collected from these interactions to improve itself.

<img src="/assets/slides/maxinforl/intro.gif" width="720"/>

A core challenge in this setting is deciding whether the agent should leverage its current knowledge to maximize performance or try new actions in pursuit of better solutions. Striking this balance between exploration–exploitation is critical.

Most widely applied online RL algorithms, such as SAC, explore naively. They fail to account for the agent's lack of knowledge; instead, the agent explores in an undirected fashion by sampling random action sequences. This leads to suboptimal performance, particularly in challenging exploration tasks with continuous state-action spaces. Nonetheless, such algorithms are ubiquitous in RL research due to their simplicity. In this work, we boost these algorithms with directed exploration derived from information gain. Thereby, we maintain the simplicity of the naive exploration methods but obtain better and directed exploration.

## MaxInfoRL

<!---
The basis of many RL algorithms is Boltzmann exploration, where the policy $\pi: \mathcal{A} \times \mathcal{S} \to \mathbb{R}_{+}$ has the following distribution:

$$
\pi(a \mid s) \propto \exp\left(\alpha^{-1} Q^{\pi}(s, a)\right),
$$

here $Q^{\pi}(s, a)$ is the soft-Q function that measures the performance of the policy with respect to the extrinsic rewards.

For small values of the temperature $\alpha$, the policy acts greedily with respect to the Q-function, and for large values of $\alpha$, it acts uniformly at random. To this end, the temperature is used to trade off exploration–exploitation.

The above distribution is the basis of several RL algorithms (SAC, REDQ, DrQ), where the policy is picked to maximize the following objective:

$$
\max_{\pi} \mathbb{E}_{a \sim \pi}\left[ Q^{\pi}(s, a) - \alpha \log(\pi(a \mid s)) \right].
$$

In MaxInfoRL, we augment the distribution above and propose:

$$
\pi(a \mid s) \propto \exp\left(\alpha^{-1} Q^{\pi}(s, a) + I(s^{\prime}; f^{*} \mid s, a)\right),
$$


here, $I(s^{\prime}; f^{*} \mid s, a)$ represents the information gain from observing the tuple $(s, a, s^{\prime})$. For small values of the temperature $\alpha$, the policy still remains greedy with respect to the Q-function, but for large values of $\alpha$, it focuses on collecting informative samples, i.e., explores in a directed fashion. The policy is picked to maximize the following objective:

$$
\max_{\pi} \mathbb{E}_{a \sim \pi}\left[ Q^{\pi}(s, a) - \alpha \log(\pi(a \mid s)) + \alpha I(s^{\prime}; f^{*} \mid s, a)\right].
$$
-->

We combine Boltzmann exploration based soft-actor critic algorithms ([SAC][sac], [REDQ][redq], [DrQ][drq] etc) with intrinsic rewards to obtain principled exploration. In particular, we use an ensemble of forward dynamics model to estimate the information gain of each transition tuple and incorporate it as an exploration bonus in addition to the policy entropy. 
This results in the policy update rule described below.
<img src="/assets/slides/maxinforl/info_gain_animation.gif" width="720"/>

The temperatures $(\alpha_1, \alpha_2)$ are automatically tuned as typically done for soft actor-critic algorithms. 

### MaxInfoRL maximizes state entropy
While the standard Boltzmann exploration focuses only on the entropy of actions, due to the introduction of the information gain, MaxInfoRL also maximizes the state entropy. This is depcited in the simple graphic below. Where we illustrate on the example of a pendulum that MaxInfoRL covers the state space much more.
<img src="/assets/slides/maxinforl/pendulum_animation.gif" width="720"/>

## Experiments

### MaxInfoRL is flexible! 

MaxInfoRL can be combined with different RL algorithms and intrinsic rewards. To illustrate this, we combine it with [SAC][sac], [REDQ][redq], [DrQ][drq], and [DrQv2][drqv2]. Furthermore, we also evaluate MaxInfoRL with RND as intrinsic reward. In all cases, the algorithm automatically trades-off extrinsic rewards with intrinsic exploration and outperforms the base algorithm.
<img src="/assets/slides/maxinforl/flexibility.png" width="720"/>

### MaxInfoRL is SOTA on hard visual control tasks!

We evaluate MaxInfoRL on hard visual control tasks from the deepmind control suite and show that it outperforms the SOTA: [DrM][drm]. 
<img src="/assets/slides/maxinforl/visual_control.gif" width="720"/>


##  Bibtex

<div class="code-container" style="position: relative;">
    <button id="copy-btn" onclick="copyToClipboard()" 
            style="position: absolute; top: 10px; right: 10px; background-color: #f0f0f0; border: none; padding: 5px 10px; cursor: pointer; border-radius: 5px;">
        <i id="copy-icon" class="fa fa-copy" style="font-size: 16px;"></i>
    </button>
    <pre id="bibtex-entry"><code>
@article{sukhija2024maxinforl,
  title={MaxInfoRL: Boosting exploration in reinforcement learning through information gain maximization},
  author={Sukhija, Bhavya and Coros, Stelian and Krause, Andreas and Abbeel, Pieter and Sferrazza, Carmelo},
  journal={ICLR},
  year={2025}
}
    </code></pre>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css"></script>

<script>
function copyToClipboard() {
    var codeText = document.getElementById('bibtex-entry').innerText;
    var textArea = document.createElement('textarea');
    textArea.value = codeText;
    document.body.appendChild(textArea);
    textArea.select();
    document.execCommand('copy');
    document.body.removeChild(textArea);

    // Change the icon to the checkmark
    var copyIcon = document.getElementById('copy-icon');
    copyIcon.classList.remove('fa-copy');
    copyIcon.classList.add('fa-check');  // Switch to checkmark icon

    // Change it back to the copy icon after 2 seconds
    setTimeout(function() {
        copyIcon.classList.remove('fa-check');
        copyIcon.classList.add('fa-copy');  // Switch back to copy icon
    }, 350);
}
</script>



[sac]: https://arxiv.org/pdf/1812.05905
[redq]: https://arxiv.org/pdf/2101.05982
[drq]: https://arxiv.org/pdf/2004.13649
[drqv2]: https://arxiv.org/pdf/2107.09645
[drm]: https://arxiv.org/pdf/2310.19668
[maxinfo_jax]: https://github.com/sukhijab/maxinforl_jax
[maxinforl_sb3]: https://github.com/sukhijab/maxinforl_torch



