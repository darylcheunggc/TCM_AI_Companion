# TCM_AI_Companion 
--------------------------------------------------------------------------------------------------------------------------------------------------
2026-8-14
# GB10 Migration Plan: Ollama/GGUF → vLLM

**Problem:** Ollama/GGUF setup isn't using NVFP4, NIM, or TensorRT-LLM — leaving GB10's Blackwell hardware underutilized and token speed slow.

**Goal:** Move to a vLLM-served stack with the right model + embedding swaps.

---

## 1. Model Swap
- [ ] Drop qwen2.5:72b for reasoning → use **32B Distill** (e.g. DeepSeek-R1-Distill-Qwen-32B) instead
- [ ] Confirm exact checkpoint/quant to pull (HF repo, FP8/NVFP4 weights if available)
- [ ] Decide if a lightweight retrieval-side model is still needed alongside it (per two-model RAG setup)

## 2. Embedding Swap
- [ ] Replace **nomic-embed-text** with **bge-m3**
- [ ] Re-embed/re-index any existing textbook RAG vector store (embedding change invalidates old vectors)
- [ ] Confirm bge-m3 served via vLLM's embeddings endpoint (or separate lightweight server if vLLM embedding support is limited)

## 3. Engine Migration: Ollama → vLLM
- [ ] Install vLLM on GB10 (Ubuntu 24.04 aarch64) — check ARM64/Blackwell (GB10 Grace Blackwell) wheel or build-from-source support
- [ ] Verify CUDA/driver version compatibility with vLLM's Blackwell support
- [ ] Stand up vLLM OpenAI-compatible server for the 32B Distill model
- [ ] Point Continue (VS Code) and/or OpenWebUI at the vLLM endpoint instead of Ollama's

## 4. Enable NVFP4 / TensorRT-LLM / NIM Path
- [ ] Check if vLLM on GB10 supports NVFP4 quantization directly, or if TensorRT-LLM engine build is required for that speedup
- [ ] If pursuing NIM: check NVIDIA NIM container availability/support for GB10 (Grace Blackwell Superchip)
- [ ] Benchmark tokens/sec: Ollama/GGUF baseline vs. vLLM (+ NVFP4/TensorRT-LLM if enabled)

## 5. Cleanup
- [ ] Decommission unused Ollama models (qwen2.5:72b, nomic-embed-text, deepseek if replaced)
- [ ] Update JupyterLab/scratchpad references and any scripts pointing to Ollama API

---
*Send follow-up prompts for any step above and I'll go deeper (install commands, config files, benchmarking scripts, etc.)*
