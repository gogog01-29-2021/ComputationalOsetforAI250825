## Phase D – Substitution and change-of-basis studies

In this phase, systematically replace one primitive or architectural pattern with another while keeping the overall FLOPs or parameter budget constant. The goal is to see how sensitive different tasks are to the choice of operator and whether cheaper approximations suffice.

### D1 – Attention variants
Swap global attention (B3) with block-sparse attention, linearised attention, or local convolution at identical compute budgets. Measure performance on long-sequence tasks such as language modelling and retrieval. A small drop indicates that the cheaper variant captures the essential behaviour; a large drop suggests global attention is necessary.

### D2 – Mixture-of-experts vs dense networks
At fixed FLOPs and parameter count, compare mixture-of-experts models (with B7 routing) to dense models. Evaluate generalisation and tool-use reliability on benchmarks requiring reasoning and tool usage. Determine whether routing provides a better compute-accuracy trade-off.

### D3 – MLP vs KAN modules
Replace standard MLP blocks (B1 heavy) with Kolmogorov–Arnold Network (KAN) blocks (B4 heavy) in a given architecture. Compare throughput, sample efficiency, and interpretability on regression and small-data tasks. KANs may offer smoother function approximation at the cost of lower arithmetic intensity; this experiment quantifies that trade-off.
