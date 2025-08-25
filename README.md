# Measuring AI Capability via an Operations Basis

This repository proposes a way to evaluate and compare neural‑network architectures by decomposing them into a small set of universal operations (B1–B12) and training motifs rather than relying on high‑level modules. By logging per‑primitive coefficients (α) and per‑motif coefficients (β), each model is represented as a capability vector that can be compared across architectures and used to predict performance on downstream tasks.

## Overview

Modern deep‑learning frameworks hide computational cost behind `nn.Module` wrappers, but real runtime and energy costs arise from low‑level kernels. The basis used here enumerates primitives such as matrix multiplication (B1), convolution (B2), content‑based read/write (B3) and elementwise nonlinearity (B4)【X88963086174487†screenZshot】. Logging α coefficients captures the compute, memory, intensity and selectivity associated with each primitive, while β coefficients capture training motifs such as the optimiser, numerical precision, parallelism plan and checkpointing【363081928824787†screenshot】. This yields apples‑to‑apples comparisons across disparate models.

## Learnable task weights

To relate capability vectors to benchmark scores, we learn a task‑demand vector \(w_t\) from data. Rather than guessing what matters for a given benchmark, we regress scores on the measured α and β coefficients. High values in \(w_t\) highlight the primitives and motifs most important for that task and expose missing capacity—for example, a benchmark that stresses long‑range retrieval will assign a high weight to B3 (attention)【853032267107336†screenshot】. The schema for specifying these weight vectors lives in [`task_weights.json`](task_weights.json)【425297883626†screenshot】.

## Experimentation phases

The framework’s validity and the learned weight vectors are refined through five experimental stages:

* **Phase A – Basis sanity and micro‑benchmarks.** Isolate each basis primitive on synthetic tensors, measure FLOPs, latency and bytes, and build roofline plots to identify compute‑bound vs bandwidth‑bound operations【88963086174487†screenshot】.
* **Phase B – Controlled diagnostic tasks.** Design simple tasks that each depend strongly on one primitive (e.g., copying for attention, local texture for convolution, scale perturbations for normalisation) and measure the effect of ablating or scaling that primitive【129873369054265†screenshot】.
* **Phase C – Training‑loop motif sweeps.** Keep the architecture fixed and vary optimisers, learning‑rate schedules, numeric precision and parallelism strategies to see how β motifs affect wall‑clock efficiency and convergence【521018449251231†screenshot】.
* **Phase D – Substitution and change‑of‑basis studies.** Replace expensive primitives with cheaper approximations at equal FLOPs (e.g., block‑sparse attention instead of global attention, mixture‑of‑experts vs dense networks, or MLP blocks vs KAN blocks) to quantify the trade‑offs between speed, sample efficiency and interpretability【998631908132748†screenshot】.
* **Phase E – External evaluation suites.** Apply the framework to comprehensive benchmarks like GAIA, GPQA, SWE‑bench, ARC‑AGI and MMLU‑Pro. Map each benchmark to a task‑demand vector and compare measured capability vectors against these demands to identify gaps【853032267107336†screenshot】.

## Practical use

Because the operations basis is objective‑agnostic, this framework accommodates different architectural paradigms and training objectives. Attention is just one form of content‑based read/write (B3); mixing or replacing it with convolution or other primitives becomes an empirical question. Similarly, standard MLP blocks are B1‑heavy, whereas Kolmogorov–Arnold Network (KAN) blocks are B4‑heavy【998631908132748†screenshot】. By combining measured α/β vectors with learned task weights, practitioners can diagnose missing capacity (e.g., insufficient attention, poor bandwidth utilisation or suboptimal optimiser) and make principled architectural or training adjustments.
