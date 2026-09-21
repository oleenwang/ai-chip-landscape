# Inference Cost Analysis — The Real Cost of AI Features

> Breaking down the actual cost structure of AI features at the device and service level, and what it means for product pricing.

---

## The Cost Nobody Talks About

AI chip analysis focuses on performance per watt. Product economics focuses on margin. Neither talks about the actual cost structure that determines whether an AI feature is viable at a given retail price.

This analysis fills that gap.

---

## On-Device AI: The BOM Math

### The Cost of Adding NPU to a Mid-Range Phone

```
Scenario: Adding NPU capability to a $150 emerging market phone

Without NPU (MediaTek Helio G99):
- Chip cost: $12-14
- Total BOM: ~$65 (display, camera, battery, etc.)
- Margin at 35% gross: $52.5
- Retail: $149

With NPU (MediaTek Dimensity 6080):
- Chip cost: $18-22 (+$6-8)
- Total BOM: ~$71-73 (+$6-8)
- Margin at 35% gross: $52.5-56
- Retail: $149-159

Net delta: +$6-8 BOM = +$10-13 retail to preserve margin

User willingness to pay at $150: Maybe $5-10 for visible AI features
→ This means the AI feature delta must create >$6-8 of perceived value per unit
```

### When Does NPU Make Sense at $150?

```
The math works when:
1. The AI feature enables a meaningful price premium
   → Camera AI that wins camera comparisons: $5-10 value
   → Voice assistant that works offline: $5-10 value

2. The AI feature reduces other BOM costs
   → Software-based noise reduction vs. hardware DSP: saves $1-2

3. The AI feature enables a new product category
   → "Works offline" as a category differentiator: worth $5-10

The math breaks when:
1. AI features are invisible to users (no premium)
2. Competition forces price to $130-140 (margin disappears)
3. Users don't perceive AI as worth extra cost
```

---

## Cloud AI: The API Cost Math

### LLM API Costs (2025)

```
OpenAI GPT-4o:
- Input: $2.50 / 1M tokens
- Output: $10 / 1M tokens
- Typical 7B chat: ~500 tokens input, 200 tokens output = $0.0035 per conversation

Anthropic Claude 3.5:
- Input: $3 / 1M tokens
- Output: $15 / 1M tokens

Google Gemini 1.5:
- $1.25 / 1M tokens (flash), $3.50 / 1M tokens (pro)

WhatsApp voice message equivalent (cloud AI):
- 30-second voice note → ~150 tokens → $0.0005 per message
- If user sends 10 voice notes/day → $0.005/day → $1.50/month
- At $0.50-2/MB data cost: $1.50/month data + $1.50/month API = $3/month total
```

### Why Cloud AI is Unsustainable for Emerging Markets

```
Data cost comparison:
- Voice note via cloud AI: ~$0.0005 per message, requires data
- Voice note offline transcription: $0 per message, no data

At 10 voice notes/day:
- Cloud AI cost: $1.50/month in API + $1.50/month in data = $3/month
- Typical emerging market user data budget: $3-5/month
→ AI features cost as much as 60-100% of data budget

This is fundamentally why cloud AI features fail in emerging markets.
The data cost makes the AI feature unaffordable at scale.
```

### The Offline-First Economics

```
Offline AI costs:
- Model storage: 2-4GB extra flash → $0.50-1.00 per unit BOM
- NPU cost delta: $6-8 per unit BOM
- One-time engineering investment: $500K-2M (localization, optimization)
- Model updates: ~$50K per language pair per year

At 1M units/year:
- NPU delta: $6-8M/year
- Engineering amortized: $0.50-2/year per unit
- Model updates: $0.05/year per unit

Total per unit cost: ~$7-10 BOM + $0.55/year

vs. Cloud AI:
- $3/month per active user = $36/year
- At 30% monthly active users: $10.80/year per device

Break-even: Offline AI becomes cheaper than cloud AI at:
$10 / $10.80 per device-year = ~11 months of usage

For a 2-year device lifecycle: Offline AI is 2x cheaper than cloud AI.
```

---

## The Infrastructure Cost of AI Features

### What Vendors Don't Tell You

```
AI features require infrastructure:

1. Model hosting (for cloud-assisted features):
   - Even "offline-first" devices need occasional model updates
   - Need server infrastructure for delta updates: $50-200K/year

2. Model evaluation and testing:
   - Every language pair requires user testing: $100K per language
   - 20 languages: $2M testing budget

3. A/B testing infrastructure:
   - Which model version performs better?
   - Server costs for experiment management: $30-100K/year

4. Monitoring and alerting:
   - Model quality degrades over time
   - Need to monitor accuracy metrics: $20-50K/year

5. User feedback systems:
   - Users flag incorrect outputs: $30-80K/year to manage

Total annual infrastructure: $200K-500K for a serious AI feature program
```

### The Hidden Engineering Cost

```
SDK integration:
- NPU SDK integration: 2-4 engineers × 6 months = $300-600K
- Camera AI integration: 2-4 engineers × 4 months = $200-400K
- Voice AI integration: 3-5 engineers × 8 months = $500-800K
- Localization: 1-2 engineers × 12 months per language × 20 languages = $1-2M

Total engineering investment: $2-4M per AI feature area
Amortized over 1M units: $2-4 per device
```

---

## Realistic AI Feature Economics

### The Viable Feature Set at $150

```
Economically viable AI features at $150 MSRP:

✅ Viable (BOM + engineering amortized < $5/device):
- Camera AI (low-light enhancement): $1-2 BOM + $0.50 engineering
- Voice noise reduction: $0.50 BOM + $0.50 engineering
- Basic predictive text: $0 engineering (OS-level)

⚠️ Viable with caveats (BOM + engineering = $5-10/device):
- On-device ASR for Tier 1 languages: $1-2 BOM + $1-2 engineering
- On-device LLM (3B, 4-bit): $2-3 BOM + $2-3 engineering
- Local language OCR: $0.50 BOM + $1-2 engineering

❌ Not viable at $150 (BOM + engineering > $10/device):
- Full on-device translation (20+ languages): BOM $5 + engineering $5+
- Real-time video AI: NPU insufficient, BOM delta too high
- Full agentic AI: Requires flagship-level compute

The path to viability for Tier 2+ features:
→ Ship in $200-250 segment first
→ Engineering amortization improves at 5M+ units
→ Technology cost curves reduce BOM at 2-year intervals
```

---

## The Pricing Strategy Math

### How to Price an AI Feature

```
The correct question: What is the value of this AI feature to the user?

Not viable: "How much does it cost?" → leads to commoditization
Viable: "How much is this worth to users who need it?" → leads to value pricing

Example: Offline voice transcription

Cost-based: $0.50 BOM → price at $2-3 feature premium
Value-based: User saves $3-5/month data cost → feature worth $20-40 over 2 years
           → Can price feature at $5-10 premium with clear value communication

The key: Users must perceive the value transfer happening.
"Works offline without eating data" = $3-5/month = $36-60/year
This is worth a $10-20 device premium if communicated clearly.
```

---

*Analysis based on public BOM data and market research. Not employer-confidential.*
