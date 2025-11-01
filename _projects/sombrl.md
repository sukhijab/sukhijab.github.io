---
layout: page
title: Scalable and Optimistic Model-Based RL maximization
img: /assets/img/publication_preview/rccar_montage.gif
importance: 1
category: work
layout: distill
published: true
date: 2025-05-08 13:58:00
tags: [Reinforcement Learning, publication]
authors:
  - name: Bhavya Sukhija
    url: "https://sukhijab.github.io"
    affiliations:
      name: LAS<d-footnote>Learning & Adaptive Systems Group</d-footnote> & CRL<d-footnote>Computational Robotics Lab</d-footnote>, ETH Zurich
  - name: Lenart Treven
    url: "https://lenarttreven.github.io/"
    affiliations:
      name: LAS, ETH Zurich
  - name: Carlo Sferrazza
    url: "https://sferrazza.cc"
    affiliations:
      name: RLL<d-footnote>Robot Learning Lab</d-footnote>, UC Berkeley
  - name: Florian Dörfler
    url: "https://dorfler.ethz.ch/"
    affiliations:
      name: ACL (IfA)<d-footnote>Automatic Control Laboratory</d-footnote> , ETH Zurich
  - name: Pieter Abbeel
    url: "https://people.eecs.berkeley.edu/~pabbeel/"
    affiliations:
      name: RLL, UC Berkeley
  - name: Andreas Krause
    url: "https://las.inf.ethz.ch/krausea"
    affiliations:
      name: LAS, ETH Zurich
---

Paper: <a href="https://openreview.net/pdf?id=eGfi5k7RP6"> NeurIPS2025.  
Implementation: [MBPO][sombrl]


## Abstract

We address the challenge of efficient exploration in model-based reinforcement learning (MBRL), where the system dynamics are unknown and the RL agent must learn directly from online interactions. We propose Scalable and Optimistic MBRL (SOMBRL), an approach based on the principle of optimism in the face of uncertainty. SOMBRL learns an uncertainty-aware dynamics model and greedily maximizes a weighted sum of the extrinsic reward and the agent's epistemic uncertainty. SOMBRL is compatible with any policy optimizers or planners, and under common regularity assumptions on the system, we show that SOMBRL has sublinear regret for nonlinear dynamics in the (i) finite-horizon, (ii) discounted infinite-horizon, and (iii) non-episodic setting. Additionally, SOMBRL offers a flexible and scalable solution for principled exploration. We evaluate SOMBRL on state-based and visual-control environments, where it displays strong performance across all tasks and baselines. We also evaluate SOMBRL on a dynamic RC car hardware and show SOMBRL outperforms the state-of-the-art, illustrating the benefits of principled exploration for MBRL.

## Problem Setting

We study the problem of online reinforcement learning (RL), where the agent interacts with the environment and uses the data collected from these interactions to improve itself.

<div style="text-align: center;">
<img src="/assets/slides/sombrl/online_rl_loop.gif" width="720"/>
</div>

Exploration--Exploitation trade-off plays a crucial role in this setting: 
Should the agent leverage its current knowledge to maximize performance or try new actions in pursuit of better solutions?

Most widely applied online RL algorithms explore naively and accordingly yield suboptimal performance. On the other hand, principled RL methods, despite their strong theoretical foundations, do not scale to real-world settings and therefore are rarely applied. 
In this work, we bridge the gap between theory and practice and propose a principled yet scalable algorithm for online RL.

## SOMBRL

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

We combine greedy exploration methods with intrinsic rewards obtained from the epistemic uncertainty of a learned dynamics model. We use an ensemble of forward dynamics model to estimate the model uncertainty of each transition tuple and incorporate it as an exploration bonus. The learned model is then also used for planning yielding additional gains in sample-efficiency. 
This results in the policy update rule described below.

$$\pi_n = \underset{\pi \in \Pi}{\arg\max}\; \mathbb{E}_{\pi} \left[ \sum^{T-1}_{t=0} r(x'_t, u_t) + \lambda_n ||\sigma_n(x'_t, u_t)|| \right],
\; 

x'_{t+1} = \mu_n(x'_t, u_t) + w_t,$$

### SOMBRL has sublinear regret for most common RL settings
We theoretically investigate SOMBRL and show that it represents a scalable approach for optimistic exploration in model-based RL. Moreover, we show under regularlity assumptions of the underlying system, that SOMBRL enjoys sublinear regret for the most common RL settings.

**Main Theorem**: Under regularlity assumptions on the system, SOMBRL has sublinear regret $R_N = \sum^N_{n=1} r_n$ for (i) finite-horizon, (ii) discounted infinite horizon, and (iii) non-episodic average reward settings. Here $r_n$ measures the performance gap between the optimal and current policy.

## Experiments

### SOMBRL is more scalable than other principled exploration methods! 

We compare SOMBRL with other principled exploration algorithms in the episodic [HUCRL][hucrl] and nonepisodic setting [NeORL][neorl]. Due to the simplified optimization of SOMBRL, it outperfroms these principled methods and is also computationally cheaper! 
<div style="text-align: center;">
<img src="/assets/slides/sombrl/sombrl_optimism_comparison.png" width="720"/>
</div>

### SOMBRL performs well across the board!

We compare SOMBRL with other deep RL model-based methods on state-based ([MBPO][mbpo]) and visual control tasks ([Dreamerv3][dreamer]). 
Principled exploration methods such as [HUCRL][hucrl], do not scale to these settings. 
Whereas scalable methods such as [MBPO][mbpo] and [Dreamerv3][dreamer] explore naively, i.e., are not principled.  
However, due to SOMBRL's practical approach to optimistic exploration, it can be seamlessly applied to high-dimensional settings. In addition, SOMBRL is also principled and enjoys theoretical guarantees across several common RL settings. Finally, across all our experiments, SOMBRL performs the best or on-par than the SOTA deep RL baselines, while also having negligible difference in computational cost.
<div style="text-align: center;">
<img src="/assets/slides/sombrl/main_results_sombrl.png" width="720"/>
</div>


<p></p> 
**Computational Cost**

| Algorithm              | Training time                                                                                          |
|------------------------|--------------------------------------------------------------------------------------------------------|
| HUCRL (GPs)            | 90 +/- 3 min (Pendulum), 31.5 +/- 2.5 min (MountainCar)                                                |
| SOMBRL (GPs)           | 30 +/- 0.6 min (Pendulum), 13.8 +/- 0.25 min (MountainCar)                                             |
| MBPO-Mean              | 9.6 +/- 0.2 min (Time per 100k steps, 1 ensemble, GPU: NVIDIA GeForce RTX 2080 Ti)                     |
| MBPO-Optimistic        | 13.7 +/- 0.35 min (Time per 100k steps, 5 ensembles, GPU: NVIDIA GeForce RTX 2080 Ti)                  |
| Dreamer                | 42.24 +/- 0.95 min (Time per 100k steps, GPU: NVIDIA GeForce RTX 4090)                                 |
| Dreamer-Optimistic     | 46.32 +/- 0.34 min (Time per 100k steps, 5 ensembles, GPU: NVIDIA GeForce RTX 4090)                    |

### SOMBRL enables sample-efficient online learning on HW!
We also apply SOMBRL on a real-world HW experiment. Here the task for the agent is to perform a drifting manneuver and park the highly dynamic RC car. The reward for this task is sparse. We compare SOMBRL to the SOTA model-based RL baseline: [SimFSVGD][simfsvgd]. Due to its naive exploration [SimFSVGD][simfsvgd] gets stuck at a local optima whereas SOMBRL finds the optimal solution.
<div style="text-align: center;">
<img src="/assets/img/publication_preview/rccar_montage.gif" width="720"/>
</div>

##  Bibtex

<div class="code-container" style="position: relative;">
    <button id="copy-btn" onclick="copyToClipboard()" 
            style="position: absolute; top: 10px; right: 10px; background-color: #f0f0f0; border: none; padding: 5px 10px; cursor: pointer; border-radius: 5px;">
        <i id="copy-icon" class="fa fa-copy" style="font-size: 16px;"></i>
    </button>
    <pre id="bibtex-entry"><code>
@article{sukhija2025somrbl,
  title={SOMBRL: Scalable and Optimistic Model-Based RL},
  author={Sukhija, Bhavya and Treven, Lenart and Sferrazza, Carmelo and Dörfler, Florian and Abbeel, Pieter and Krause, Andreas},
  journal={NeurIPS},
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



[mbpo]: https://arxiv.org/abs/1906.08253
[dreamer]: https://arxiv.org/abs/2301.04104
[hucrl]: https://arxiv.org/abs/2006.08684
[neorl]: https://arxiv.org/abs/2406.01175
[simfsvgd]: https://arxiv.org/abs/2403.16644
[sombrl]: https://github.com/lasgroup/ombrl



