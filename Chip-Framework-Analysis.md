# Chip-Framework Analysis: AI Hardware meets Open Source

> Which AI chips actually work with the open-source frameworks developers use — and why that determines product success, not benchmark numbers.

---

## The Framework Question Hardware Vendors Get Wrong

Most AI chip analysis focuses on TOPS,功耗, and benchmark scores. **These are the wrong metrics for product decision-making.**

The question that actually determines whether a chip wins in the market is:

> *"Can developers build and deploy models using the frameworks they already know?"*

A chip with excellent benchmark numbers but poor PyTorch support will lose to a chip with decent numbers and native llama.cpp support. Because **developers vote with their time**, and retraining for a new framework is expensive.

---

## Open Source Framework Landscape (2025)

### llama.cpp — The Edge Inference Standard

**What it is:** George Hotz's group repo, now the de facto standard for running quantized LLMs on consumer hardware.

**Why it matters for PMs:** If your chip runs llama.cpp well, developers will port models to it. The gguf format is becoming a universal model distribution format.

**Chip support tier list for llama.cpp:**

| Tier | Chips | Why |
|------|-------|-----|
| 🥇 Native | Qualcomm (Hexagon), Apple (Neural Engine), Intel (iGPU Arc) | Hardware-accelerated matrix math, low memory bandwidth |
| 🥈 Good | MediaTek NPU, NVIDIA (all), AMD ROCm | Software fallbacks work, memory bandwidth sufficient |
| 🥉 Usable | RISC-V + NPU (曦算Xien, SpacemiT) | Needs more software investment |
| ❌ Poor | Ascend 910 (驱动问题), 寒武纪 (custom only) | Framework support is an afterthought |

**PM Insight:** For emerging market AI devices, llama.cpp compatibility is the single most important developer ecosystem indicator. A chip that developers can run 7B models on at 30 tokens/sec will win more mindshare than a chip that benchmarks at 2x the TOPS but requires custom kernel development.

---

### PyTorch — The Training & Research Standard

**What it is:** Meta's open-source ML framework, the dominant choice for AI research and production training.

**The XLA Problem:** PyTorch's native execution path doesn't automatically map to accelerators. Hardware vendors need either:
- PyTorch Native execution (vendor-specific kernels)
- PyTorch XLA (Google's compiler for accelerators)
- PyTorch 2.0 `torch.compile()` with custom backends

**Chip support status:**

```
Qualcomm:     ✅ PyTorch Native (QNN backend) + 🚧 XLA (ongoing)
Apple MPS:   ✅ PyTorch Native (Metal Performance Shaders)
NVIDIA:      ✅ PyTorch Native (CUDA) — dominant
AMD:         ✅ PyTorch Native (ROCm) + ✅ XLA
Intel Arc:   ✅ PyTorch Native (IPEX) + ✅ XLA
MediaTek:    ⚠️ Partial (MTK AI SDK, limited PyTorch integration)
Ascend:      ⚠️ Custom PyTorch (MindSpore conversion required)
RISC-V NPU:  ❌ No native support yet (2026 target)
```

**PM Insight:** If you're building a product that requires custom model training or fine-tuning (not just inference), PyTorch native support is non-negotiable. For inference-only edge devices, llama.cpp compatibility matters more.

---

### ONNX & ONNX Runtime — The Interoperability Layer

**What it is:** Microsoft's model format designed to solve "model portability" — train once, deploy anywhere.

**ONNX Runtime (ORT):** The inference engine that actually runs ONNX models on hardware.

**Why it matters:** For hardware vendors trying to capture the enterprise market, ONNX Runtime support is table stakes. Enterprise customers don't want to retrain models — they want to deploy existing models on new hardware.

**ORT acceleration backends by chip:**

| Chip | ORT Execution Provider | Status |
|------|----------------------|--------|
| NVIDIA GPU | ✅ CUDA EP | Production stable |
| Qualcomm | ✅ QNN EP | Production stable |
| Intel CPU/GPU | ✅ CPU EP + ⭐ DirectML EP | Best Windows story |
| AMD | ✅ ROCm EP + DirectML | Improving |
| Apple | ✅ CoreML EP | Good for on-device |
| MediaTek | ⚠️ Basic ORT support | Limited |
| Ascend | ⚠️ Custom ORT build | Isolated ecosystem |

**PM Insight:** If you're targeting enterprise customers in China (who often use PaddlePaddle or MindSpore alongside PyTorch), ONNX Runtime support becomes a political question as much as a technical one.

---

### exo — The New Contender for Edge

**What it is:** A new open-source framework for running AI models on edge devices, gaining traction for its simplicity and broad hardware support.

**Status:** Early stage (2025), but the "no-driver-install" story is compelling for consumer products.

**PM Relevance:** Worth watching. If exo gains adoption, it could become the next llama.cpp — the easiest path to running open models on new hardware. Consider exo compatibility when evaluating chips for 2026+ products.

---

## The Practical Decision Matrix

### For AI Smartphone / Consumer Edge Device PM

```
Priority order:
  1. llama.cpp compatibility (what developers actually use)
  2. ONNX Runtime QNN/CPUEP support
  3. Power consumption at sustained inference load
  4. MediaTek vs Qualcomm ecosystem maturity
  
Skip: PyTorch native training support (consumer devices don't train)
Skip: Benchmark TOPS (marketing numbers, not real-world)
```

### For AI Server / Enterprise Hardware PM

```
Priority order:
  1. PyTorch native + CUDA/ROCm (research ecosystem)
  2. ONNX Runtime enterprise EPs
  3. Kubernetes / container deployment support
  4. Multi-chip cluster management software
  
Skip: llama.cpp (server inference uses vLLM/TGI, not llama.cpp)
```

---

## What This Means for Hardware PM Decisions

When I'm evaluating an AI chip for a product roadmap, I ask these questions in order:

1. **What's the target inference workload?** (7B chat model? Whisper? Stable Diffusion? This determines the memory bandwidth requirement.)
2. **Which frameworks does the engineering team already know?** (Forcing a team to learn a new framework adds 3-6 months to timeline.)
3. **What's the sustained inference power consumption at product form factor?** (Peak TOPS is meaningless if the device overheats in 10 minutes.)
4. **Is there a developer ecosystem already using this chip?** (GitHub stars on the vendor's framework repo = real adoption signal.)

These four questions cut through the marketing noise faster than any benchmark comparison.

---

*Last updated: based on public data as of 2025. Not an endorsement of any vendor.*
