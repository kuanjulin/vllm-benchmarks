# vllm-benchmarks

## Introduction
This project benchmarks the inference performance of the [TinyLlama-1.1B-Chat-v1.0](https://huggingface.co/TinyLlama/TinyLlama-1.1B-Chat-v1.0) model using two backends:
- [vLLM](https://github.com/vllm-project/vllm): a high-throughput inference engine for LLMs using PagedAttention.
- Hugging Face Transformers: the standard PyTorch-based inference backend.

We evaluate both FP16 and FP32 precision modes and compare throughput, model load time, and answer accuracy on the GSM8K test set.

## Summary
- **vLLM FP16** offers the **best inference throughput**, **2.88× faster** than Hugging Face FP16.
- vLLM models take longer to load due to internal graph optimizations and engine setup.
- Accuracy remains high (99.7%) across all setups, with Hugging Face slightly ahead on exact match.

## Environment/Benchmark Setup
- **Hardware**: Google Colab Pro with NVIDIA T4 GPU
- **Model**: [`TinyLlama/TinyLlama-1.1B-Chat-v1.0`](https://huggingface.co/TinyLlama/TinyLlama-1.1B-Chat-v1.0)
- **Dataset**: [`gsm8k`](https://huggingface.co/datasets/gsm8k) (`test` split)
- **Task**: Math word problem answering
- **Prompt Format**: Used original `question` field directly
- **Answer Evaluation**: Regex extraction from `"The answer is X"` pattern


## Benchmark Results: TinyLlama-1.1B on GSM8K (Test Set)

We compared inference performance between [vLLM](https://github.com/vllm-project/vllm) and Hugging Face Transformers using the TinyLlama-1.1B model on the GSM8K dataset.

| Model Variant             | Inference Speed (tokens/sec) | Load Time (s) | Accuracy |
|--------------------------|------------------------------:|--------------:|---------:|
| **vLLM FP16**            | **1109.08**                   | 119.62        | 99.7%    |
| vLLM FP32                | 365.46                        | 71.31         | 99.7%    |
| Hugging Face FP16        | 384.89                        | **6.43**      | **99.9%**|
| Hugging Face FP32        | 314.19                        | 14.06         | 99.9%    |

**TODO:** Placeholder for graphs
