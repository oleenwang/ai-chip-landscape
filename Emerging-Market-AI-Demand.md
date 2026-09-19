# Emerging Market AI Demand — What Actually Matters

> Evidence-based analysis of AI feature demand in Africa, Southeast Asia, and South Asia, based on 5 years of field work and product experience in these markets.

---

## The Fundamental Mistake Western AI Companies Make

Most AI product planning starts from "what can AI do?" and then tries to find users for it.

For emerging markets, this is backwards.

**The right question is: "What are users already failing to do, and can AI fix it at the right cost?"**

This sounds obvious. But most Western AI products fail in emerging markets because they optimize for capability, not for the specific friction points that matter when:
- Your phone is the only computing device you own
- Mobile data costs $0.50-2/MB
- Electricity is unreliable
- You speak a language that has 50 million speakers but zero commercial AI support

---

## AI Feature Demand Hierarchy — Emerging Markets

Based on field research and product experience:

### Tier 1: Immediate Need (Mass Adoption Potential)

```
1. Offline ASR + TTS in local languages
   - WhatsApp voice messages are the dominant communication form
   - Currently: voice notes are text-to-voice only if you type
   - AI fix: voice-to-text in Hausa/Swahili/Yoruba/Amharic/etc.
   - Technical requirement: < 500MB model, runs on Helio G99 class chip
   - Market gap: NONE of the major ASR providers support these languages well

2. Camera AI for low-light + skin enhancement
   - Primary use: selfies and WhatsApp photos
   - Challenge: dark skin tones + indoor lighting + low-quality sensors
   - AI fix: computational photography adapted for local conditions
   - This is already being shipped by Transsion/OPPO/realme — but still gaps remain

3. Predictive text in local scripts
   - Many users in tier-2 cities type in transliterated text
   - Accurate script prediction (not just transliteration) is the gap
   - AI fix: language models fine-tuned on local script usage
```

### Tier 2: Significant Need (Medium Adoption)

```
4. Translation (English ↔ Local Languages)
   - Business users need to read English content
   - Government/municipal communication is often in the national language
   - Current: Google Translate works but not optimized for the dominant use cases
   - AI fix: domain-specific translation (not general-purpose)

5. Battery + Performance AI
   - Users actively manage battery (turn off data when not using)
   - AI that predicts app usage patterns and pre-loads/prevents drain
   - Already shipped by most OEMs — differentiation is in accuracy

6. Storage Management
   - 32-64GB phones with 90%+ storage used is normal
   - AI that intelligently compresses photos/videos without losing "feel" of the moment
   - Gap: lossy compression that users don't notice — this is an AI problem
```

### Tier 3: Aspirational (Small Market, High Value)

```
7. Voice-based search within the phone
8. Offline navigation with local POI data
9. Agricultural information (weather, crop prices) via voice
10. Simple document scanning + OCR in local scripts
```

---

## The Chip Requirements for Each Tier

### For Tier 1 features:

```
Required chip capabilities:
- NPU capable of 5-10 TOPS sustained (not peak)
- Power consumption < 3W at sustained inference
- Memory bandwidth > 50 GB/s (required for real-time processing)
- Cost envelope: must fit in $15-25 BOM for the chip at 1M+ unit volume

Candidates:
1. MediaTek Helio G99: ✅胜任，$12-18 in volume, 8 TOPS NPU, 17K DMIPS
2. MediaTek Dimensity 6080: ✅胜任 (successor to G99, similar cost)
3. Qualcomm QCM6490: ⚠️ too expensive ($35+), overqualified
4. UNISOC T760: ⚠️ emerging, ecosystem less mature

Verdict: MediaTek Helio G99 / Dimensity 6080 family is the sweet spot for Tier 1 AI features
```

### For Tier 2 features:

```
Required chip capabilities:
- NPU capable of 15-20 TOPS sustained
- Better memory bandwidth (60+ GB/s)
- Support for larger models (1-3B parameter models)
- Cost envelope: $20-35 BOM

Candidates:
1. MediaTek Dimensity 8300: ✅最佳选择，20 TOPS NPU, mainstream cost
2. Qualcomm Snapdragon 7s Gen 2: ✅胜任 but more expensive
3. Qualcomm Snapdragon 6s Gen 3: ✅新的6系列，balance cost/performance
```

### For Tier 3 features:

```
Required: Flagship-tier NPU (20+ TOPS) or cloud connectivity assumed
Not relevant for mainstream emerging market products until 2026+
```

---

## The Local Language AI Gap — A Specific Product Opportunity

**The problem in numbers:**
- Africa: 2000+ languages, but Google supports ~20 with speech recognition
- South Asia: 100s of languages, major gaps in low-resource languages
- Southeast Asia: Similar gaps (Bahasa Indonesia/Thai/Vietnamese have decent coverage, but minority languages don't)

**The product opportunity:**
An on-device ASR/TTS system that:
- Covers the top 20 African languages (by speaker count)
- Runs on Helio G99 class hardware (current generation mid-range phones)
- Costs $2-4 per device in chip/BOM (acceptable at $150 retail price)
- Works offline

This is a genuine product gap. The challenge is not technical feasibility — it's the economics of training data acquisition for low-resource languages.

**Who is working on this:** Transsion has internal projects. Google is doing work but focused on higher-resource languages. Some local startups (e.g., in Nigeria, Kenya) are building but don't have the distribution to compete with Transsion.

---

## PM Implications for AI Chip Selection

When I'm evaluating which chip to use for an emerging market AI product, I use this decision filter:

```
Question 1: Does the chip support the NPU operations required for our Tier 1 features?
           If NO → eliminate

Question 2: Can it do this at the power budget for our product form factor?
           (e.g., for a phone with 5000mAh battery, inference must use < 3% per hour)
           If NO → eliminate

Question 3: Does the SDK support offline model deployment?
           (Some chips require cloud connectivity for AI features)
           If NO → eliminate

Question 4: What's the cost delta vs. the non-AI version of this product?
           AI features must add < $8-12 BOM to be viable at $150-200 retail
           If delta is higher → either cut features or wait for silicon to mature
```

This filter eliminates most of the "exciting" AI chips on the market and leaves you with the MediaTek G99 family and Qualcomm 7-series as the realistic options for mainstream emerging market products.

---

*Field observations and product experience from 2020-2025. Not employer-confidential.*
