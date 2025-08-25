## Phase A – Basis sanity and micro‑benchmarking

This phase checks that the chosen operations basis (B1–B12) is complete and captures the real runtime costs of the model’s building blocks. It answers two questions: *Are we missing any important primitive?* and *Which primitives are compute‑bound versus bandwidth‑bound?*

### A1 – Micro‑benchmark each basis op
For a range of tensor sizes and shapes, run isolated kernels for each basis element (e.g., GEMM, convolution, attention, elementwise activation) and record FLOPs, latency, and memory traffic. Plot FLOPs against latency and bytes to build roofline curves. These curves reveal whether an op is limited by compute or memory bandwidth.

### A2 – Roofline analysis
Use the micro‑benchmark data to construct roofline plots for each basis op on the target hardware. Operations that lie on the horizontal part of the roofline are compute‑bound; those on the sloped part are bandwidth‑bound. This helps prioritise optimisation efforts and motivates fusing or restructuring kernels to improve intensity.

### A3 – Equivalence checks
Replace an expensive primitive with a cheaper equivalent at the same FLOPs (e.g., substitute global attention with local convolution or linearised attention) and measure quality loss on diagnostic tasks. If performance degrades significantly, the basis element is essential; if not, it may be redundant or can be approximated by other ops at lower cost.
