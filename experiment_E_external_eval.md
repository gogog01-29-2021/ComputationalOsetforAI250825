## Phase E – External evaluation suites

After validating the basis and training motifs on controlled experiments, evaluate models on comprehensive, real-world benchmark suites. Each benchmark is mapped to a task-demand vector that weights different operations and motifs. Comparing measured capability vectors with task demands highlights missing primitives and guides improvements.

### GAIA – General AI assistants
GAIA comprises tasks requiring multi-step reasoning, tool use, web browsing, and multimodal understanding. Measure a model’s success rate on GAIA tasks and regress scores against capability vectors. High GAIA demand may correspond to strong B3 content-read/write and B12 communication coefficients.

### GPQA – Graduate-level question answering
The GPQA dataset contains challenging STEM questions validated by experts. It tests deep reasoning and specialised knowledge. Analyse which basis operations contribute most to GPQA performance, such as B1 linear algebra for maths or B3 attention for long-range reasoning.

### SWE-bench – Code generation and bug-fixing
SWE-bench evaluates models on real repository bug-fixing tasks. Success depends on understanding context, generating correct code, and interacting with tools. Map SWE-bench requirements onto basis ops (B1 for code embedding, B3 for retrieval) and training motifs (beta optimiser and schedule for robust fine-tuning).

### ARC-AGI – Systematic generalisation
ARC-AGI contains tasks designed to require systematic generalisation to novel instructions. It stresses compositional reasoning and algorithmic skill. Compare models with different basis balances (e.g., attention vs convolution) to see which primitives support better generalisation.

### MMLU-Pro – Knowledge and reasoning exam
MMLU-Pro extends the Massive Multitask Language Understanding benchmark with harder questions combining knowledge and reasoning. Use it to calibrate the weight vectors for language and reasoning tasks and test the effect of beta motifs like precision and optimisation.
