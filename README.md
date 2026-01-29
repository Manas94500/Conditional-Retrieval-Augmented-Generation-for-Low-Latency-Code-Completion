# Conditional Retrieval-Augmented Generation for Low-Latency Code Completion

Retrieval-Augmented Generation (RAG) is widely used in code completion systems to improve correctness by incorporating external context such as documentation or code examples. While effective, unconditional retrieval introduces additional inference overhead and increases tail latency, which can negatively impact interactive developer workflows.

This project explores a **Conditional Retrieval-Augmented Generation (CRAG)** framework that enables retrieval only when it is likely to improve generation quality, with the goal of reducing inference latency while preserving accuracy.

---

## Motivation

In many code completion scenarios, the base language model already contains sufficient knowledge to generate correct outputs. However, standard RAG pipelines perform retrieval for every prompt, leading to:
- Increased inference time
- Higher worst-case (p95) latency
- Reduced responsiveness in real-time settings

This work treats retrieval as a conditional operation rather than a mandatory component of the generation process.

---

## Approach

The proposed framework introduces a **conditional retrieval gate** that decides whether retrieval should be performed for a given input.

The pipeline consists of:
1. Prompt analysis using the base code language model
2. Estimation of prompt complexity or model uncertainty
3. Conditional activation of the retrieval module
4. Final code generation with or without retrieved context

By skipping retrieval for low-complexity or high-confidence prompts, the system reduces unnecessary context expansion and improves end-to-end latency.

---

## Evaluation

The approach is evaluated using standard code generation benchmarks:

- HumanEval  
- MBPP (Mostly Basic Programming Problems)

### Metrics
- Functional correctness
- End-to-end inference latency
- Tail latency (p95)

### Observations
- Conditional retrieval significantly reduces tail latency compared to unconditional RAG
- Accuracy remains largely comparable across tasks
- Latency improvements primarily stem from eliminating retrieval-dominated execution paths

---

## Implementation

- Language: Python  
- Frameworks: PyTorch, Hugging Face Transformers  
- Retrieval: Configurable sparse or dense retrievers  
- Benchmarks: HumanEval, MBPP  
- Analysis: End-to-end and component-level latency profiling  

---

## Intended Use

This repository is intended for:
- Research and academic experimentation
- Exploration of latency-aware RAG systems
- Reference implementations for conditional retrieval strategies

---

## Ownership and Usage

This project is an original work created by the author.  
No license is currently specified. All rights are reserved unless stated otherwise.

---

## Contact

For questions, discussions, or collaboration, please open an issue in the repository.
