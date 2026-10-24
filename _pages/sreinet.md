---
layout: page
title: "SREINet: Interpretable Discovery of High-Dimensional Dynamics"
permalink: /research/sreinet/
description: "Discovering explicit governing equations from data with sparse regression embedded interpretable networks."
nav: false
_styles: |
  .sreinet .lead { font-size: 1.2rem; line-height: 1.65; }
  .sreinet .paper-meta { color: var(--global-text-color-light); font-size: .95rem; }
  .sreinet .resource-links { display: flex; flex-wrap: wrap; gap: .65rem; margin: 1.4rem 0 2rem; }
  .sreinet .resource-links a { border: 1px solid var(--global-theme-color); border-radius: 4px; padding: .45rem .85rem; }
  .sreinet figure { margin: 2rem 0; }
  .sreinet figure img { display: block; width: 100%; height: auto; background: white; }
  .sreinet figcaption { font-size: .85rem; line-height: 1.6; margin-top: .7rem; color: var(--global-text-color-light); }
  .sreinet h2 { margin-top: 2.2rem; }
  .sreinet .results { border-left: 3px solid var(--global-theme-color); padding: .3rem 0 .3rem 1.2rem; margin: 1.6rem 0; }
  .sreinet .results p:last-child { margin-bottom: 0; }
  .sreinet pre { padding: 1rem; white-space: pre-wrap; overflow-wrap: anywhere; }
---

<div class="sreinet" markdown="1">

<p class="lead">Can we discover readable equations for a dynamical system with more than 100 state variables? SREINet combines sparse regression with an interpretable neural architecture to learn explicit governing equations from data.</p>

<p class="paper-meta">Siyuan Xing, Qingyu Han, Efstathios G. Charalampidis, and Ying-Cheng Lai<br>
<em>PRX Intelligence</em> 1, 013024 · Published September 29, 2026<br>
Featured on the official APS X account</p>

<div class="resource-links">
  <a href="https://doi.org/10.1103/pdkf-98zb">Read the paper</a>
  <a href="{{ '/assets/pdf/SREINet-PRX-Intelligence.pdf' | relative_url }}">Download PDF</a>
  <a href="https://github.com/siyuan-xing/SREINet">Code on GitHub</a>
  <a href="#citation">Cite this work</a>
</div>

## Why is high-dimensional equation discovery difficult?

In equation discovery, the goal is to recover the functions that govern how a system changes over time, rather than only predict its next state. Conventional library-based sparse regression constructs candidate terms and identifies a small subset that fits the observations. As the number of variables and the order of interactions increase, that candidate library can grow combinatorially.

SREINet addresses this representation bottleneck by embedding sparse regression in a neural network. It uses structured combinations of univariate candidate functions, avoiding explicit construction of the full multivariate library during training.

<figure>
  <img src="{{ '/assets/img/research/sreinet-workflow.png' | relative_url }}" width="1522" height="1008" alt="SREINet workflow: sample a dynamical system, train an interpretable network for each state derivative with periodic pruning, reconstruct coefficients, and simulate the identified equations.">
  <figcaption>From observations to explicit equations: dimensionwise training, periodic pruning, and coefficient reconstruction. Figure 3 from Xing et al., <em>PRX Intelligence</em> 1, 013024 (2026), <a href="https://doi.org/10.1103/pdkf-98zb">doi:10.1103/pdkf-98zb</a>. Reproduced under <a href="https://creativecommons.org/licenses/by/4.0/">CC BY 4.0</a>; cropped from the published page.</figcaption>
</figure>

## How does SREINet work?

1. **Represent the vector field.** A structured network learns one state derivative at a time using a user-selected set of atomic candidate functions.
2. **Train with periodic pruning.** A sparsity-promoting schedule removes weak weights and allows training to continue toward a compact representation.
3. **Recover explicit equations.** Network weights are converted into coefficients of multivariate functions, producing equations that can be inspected and simulated.

Interpretability comes from the architecture: its function combinations can be expanded into explicit expressions. Scalability comes from the implicit representation, minibatch optimization, and separate training of state derivatives. These are complementary features of the same approach.

A lifting-layer extension also allows selective inclusion of nonseparable candidate functions, such as sin(x₁x₂). The supplementary material demonstrates this extension on a modified Lorenz-96 system.

## What does the paper demonstrate?

<div class="results" markdown="1">

**Six numerical systems, with demonstrations up to 128 dimensions.** The paper studies Lorenz-96 (100 dimensions), a discrete φ⁴ model (100), discrete nonlinear Schrödinger dynamics (100), the Ablowitz–Ladik model (128), Hindmarsh–Rose networks (75), and Kuramoto networks (60).

**Dynamics beyond the training trajectories.** Discovered equations are tested for their ability to reproduce coherent structures from initial conditions not used for training.

**Experimental validation.** A triple-pendulum dataset provides a test using measured physical data alongside the numerical benchmarks.

</div>

The study also examines noise, incomplete data, equation-recovery accuracy, rollout errors, and memory and runtime scaling against representative baselines. Results depend on the system and experimental setting; the paper and supplementary material provide the detailed comparisons.

## When is it useful, and what are its limits?

SREINet is designed for problems where explicit governing equations are valuable and a large candidate library makes conventional regression costly. It requires suitable candidate functions, full-state observations, and derivative measurements or estimates. Training data must explore sufficiently informative regions of the state space.

Optimization is nonconvex, and training and pruning hyperparameters require care. The reported demonstrations reach 128 dimensions; extension to systems with thousands of dimensions is a prospect discussed in the paper, rather than an experimental result reported here.

## Citation

**Data-driven discovery of high-dimensional dynamical systems with sparse interpretable neural networks**<br>
Siyuan Xing, Qingyu Han, Efstathios G. Charalampidis, and Ying-Cheng Lai. *PRX Intelligence* **1**, 013024 (2026). [DOI: 10.1103/pdkf-98zb](https://doi.org/10.1103/pdkf-98zb).

```bibtex
@article{Xing2026SREINet,
  title = {Data-driven discovery of high-dimensional dynamical systems
           with sparse interpretable neural networks},
  author = {Xing, Siyuan and Han, Qingyu and Charalampidis, Efstathios G.
            and Lai, Ying-Cheng},
  journal = {PRX Intelligence},
  volume = {1},
  pages = {013024},
  year = {2026},
  doi = {10.1103/pdkf-98zb}
}
```

Questions or potential collaborations? [Contact Siyuan Xing](mailto:sixing@calpoly.edu).

</div>
