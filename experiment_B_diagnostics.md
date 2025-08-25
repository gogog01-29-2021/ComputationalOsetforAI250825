## Phase B – Controlled diagnostic tasks

This phase designs simple tasks that isolate the contribution of each basis element. By testing models on these diagnostics after ablating or scaling certain primitives, we can measure each op’s unique value for learning and generalisation.

### B-Attn – Content-based operations
Create tasks that require long-range retrieval or copying, such as copying sequences, sorting numbers, in-context retrieval, and passkey tasks. Compare performance with full attention, sparse attention, and no attention. Sensitivity to attention sparsity reveals the importance of content-based read/write (B3).

### B-Conv – Local structure and equivariance
Train models on local texture classification and translation-equivariant tasks. Compare convolutional layers (B2), local MLPs, and shifted linear layers. The drop in accuracy when removing convolution quantifies the benefit of translation equivariance.

### B-Norm/Reductions
Evaluate robustness to scale and shift perturbations by training models with or without normalisation layers (B5). Measure sensitivity to distributional shift on held-out data with different statistics. This gauges the role of normalisation in stabilising training.

### B-Routing
Investigate mixture-of-experts (B7) by varying the fraction of tokens routed to experts at fixed total FLOPs. Analyse sample efficiency and final accuracy as routing sparsity increases. Token routing tasks highlight how gating improves representational capacity.

### B-Spectral
Test spectral transforms (B10) on tasks with periodic structure, such as classifying sine-wave patterns or predicting audio pitch. Compare FFT-based layers to time-domain convolutions to see when spectral methods are advantageous.
