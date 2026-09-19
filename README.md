# AI Chip & Edge AI Hardware Landscape 2025

> A product manager's analysis of AI inference hardware, open-source framework adaptation, and emerging market opportunities.
> 
> *Perspective: Hardware PM with 14+ years mobile device experience, focused on emerging markets (Africa/South Asia/Southeast Asia).*

---

## Why This Repo

AI hardware is not just about compute — it's about the **full stack from silicon to user-facing AI features**. As a hardware PM who has shipped 100M+ units to emerging markets, I analyze AI chips through a specific lens:

- Can this chip enable AI features that users in price-sensitive markets actually care about?
- What's the real cost/performance tradeoff at the product level, not just benchmark level?
- How does the open-source ecosystem around this chip affect developer adoption?

This repo is my ongoing analysis, not a marketing deck.

---

## Sections

- **[Chip-Framework-Analysis.md](Chip-Framework-Analysis.md)** — How each major AI chip maps to open-source framework support (PyTorch XLA, llama.cpp, ONNX, exo, etc.)
- **[Edge-AI-Device-Market.md](Edge-AI-Device-Market.md)** — AI smartphones, AI PCs, NPU-enabled devices — what's actually shipping and where
- **[Emerging-Market-AI-Demand.md](Emerging-Market-AI-Demand.md)** — What AI features matter in Africa/Southeast Asia/South Asia, and which chips can deliver them at the right price point
- **[Competitive-Decision-Framework.md](Competitive-Decision-Framework.md)** — How I evaluate AI chips for product roadmaps, with real criteria weightings

---

## Key Findings (Last Updated)

### The Real Bottleneck for AI Hardware in Emerging Markets

```
Emerging market constraint hierarchy:
  1. Power consumption (battery life matters more than peak TOPS)
  2. Cost per device (AI features must fit in $80-200 retail price)
  3. Thermal design (tropical climates, no active cooling)
  4. Connectivity (AI on-device matters more when 4G is unreliable)
  5. Local language support (ASR/TTS for 50+ African languages)
```

### Chip-Framework Readiness (2025)

| Chip | PyTorch Native | llama.cpp | ONNX | Edge Runtime | Verdict |
|------|----------------|-----------|------|-------------|---------|
| Qualcomm NPU (8s Gen 3) | ✅ | ✅ | ✅ | ✅ QRN | Best edge AI story |
| MediaTek NPU (9300) | ✅ | ✅ | ✅ | ✅ | Strong, cost-effective |
| Apple Neural Engine | ⚠️ Limited | ✅ | ⚠️ | ❌ | Closed ecosystem |
| Intel iGPU (Arc) | ✅ | ✅ | ✅ | ⚠️ | PC-centric |
| NVIDIA (边缘/嵌入式) | ✅ | ✅ | ✅ | ✅ | Enterprise only |
| RISC-V + NPU (开源) | ⚠️ | ✅ | ⚠️ | ⚠️ | 2026-2027 story |

---

## About Me

```
14+ years hardware PM
- 5 years Transsion (Africa/South Asia market leader)
- Built products from $30 feature phones to $200 smartphones
- 30B+ RMB single product revenue
- 1KK+ monthly unit sales on flagship

Now exploring: AI hardware PM roles
Target companies: AI chip companies with emerging market presence
```

---

## Contact

GitHub: [@oleenwang](https://github.com/oleenwang)
LinkedIn: (add your LinkedIn URL)
Email: oleen@vip.qq.com

---

*This analysis is based on public information and product experience. Not affiliated with any employer or chip vendor.*
