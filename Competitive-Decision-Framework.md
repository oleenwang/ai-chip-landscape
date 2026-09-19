# Competitive Decision Framework — AI Hardware PM Evaluation

> A practical framework I use to evaluate AI chips and platforms for product roadmaps. Built from 14+ years of hardware PM experience, applied to the AI era.

---

## The Standard RFP Process is Wrong for AI Hardware

Most hardware PMs evaluate AI chips using a vendor-provided RFP:

```
Vendor responds with:
→ Benchmark TOPS numbers ✅
→ Power consumption specs ✅  
→ Development board availability ✅
→ SDK documentation ✅

What the RFP doesn't tell you:
→ Will developers actually use this chip? (framework support)
→ What's the real sustained performance under product form factor? (not fan-cooled bench)
→ What's the support burden on our engineering team? (undocument bugs, broken SDKs)
→ Will this chip exist in 2 years? (vendor financial stability)
```

The standard RFP tells you if a chip can theoretically do the job. It doesn't tell you if the chip will actually ship in a product on time without your engineering team burning out fighting the SDK.

---

## My 4-Layer Evaluation Framework

### Layer 1: Product Fit (Elimination Filter)

```
Does this chip enable our specific product requirements?

Questions:
1. Can it run our target AI model at our target use case?
   (7B LLM for 30 tokens/sec? Whisper for real-time transcription? SD for < 5 sec generation?)

2. Can it do so within our power budget?
   (Phone: < 3W sustained. Stick/edge device: < 10W. PC: < 30W.)

3. Can it do so within our cost envelope?
   (BOM delta vs non-AI version must fit in our retail price strategy)

4. Does it support offline inference?
   (Some chips require cloud connectivity — eliminates for many emerging market products)

If ANY of these is NO: eliminate this chip. Don't pass go.
```

### Layer 2: Engineering Feasibility (Time/Risk Filter)

```
Can our engineering team actually build this, and how long will it take?

Questions:
1. What's the maturity of the SDK?
   → Are there documented bugs that block common use cases?
   → How active is the developer community? (GitHub issues, response time)
   → Is there a reference implementation we can learn from?

2. What's the framework support story?
   → Can our team use tools they already know? (PyTorch, TensorFlow, llama.cpp)
   → Or do they need to learn a custom development environment?

3. What's the driver/software maintenance burden?
   → How often do drivers break with OS updates?
   → How much engineering time per quarter is needed to maintain AI features?

4. What's the silicon reliability track record?
   → Has this chip been in mass production for > 6 months?
   → What's the field failure rate vs. bench reliability?
   → Does the vendor have a history of EOL-ing chips quickly?

Time estimates I use:
- Native SDK + mature framework support: 2-4 months to production
- Custom kernel development required: 6-12 months
- Vendor SDK with known issues: add 2-3 months buffer
```

### Layer 3: Ecosystem Viability (Go-to-Market Filter)

```
Will this chip actually reach the users we want to reach?

Questions:
1. What's the developer ecosystem around this chip?
   → GitHub stars on official repos (rough adoption signal)
   → Are there pre-trained models available in the vendor's format?
   → Is there a model zoo or model hub with popular models?

2. What's the distribution strategy for our product?
   → If we're selling direct to consumers: does the chip vendor help with marketing?
   → If we're an OEM/ODM: does the chip vendor's brand help or hurt our positioning?
   → Are there co-marketing funds available?

3. What's the competitive situation?
   → How many other brands are using this chip for similar products?
   → Can we differentiate, or are we in a spec-sheet race to the bottom?

4. Is this vendor a long-term partner?
   → Financial stability (for continued support and roadmap visibility)
   → Roadmap alignment (is their next-gen chip aligned with our product direction?)
   → Strategic commitment (are they investing in the software ecosystem or just the silicon?)
```

### Layer 4: Strategic Alignment (Final Decision Filter)

```
Even if a chip passes all other layers, does it fit our strategy?

Questions:
1. Does using this chip advance our platform strategy?
   → If we're building a device family, does this chip fit the platform architecture?
   → Or does it require a completely different development stack?

2. Does it create strategic lock-in we want?
   → Some chips have attractive pricing but proprietary SDKs that make migration painful
   → Others are more open but cost more in the long run

3. Does it give us optionality?
   → Can we swap to a different chip vendor without rebuilding everything?
   → Or is our product roadmapped around this specific chip?

4. Is the vendor's success aligned with ours?
   → A vendor that succeeds and grows with us is better than a vendor that sells us chips
     but views us as a small customer
```

---

## Weighting by Product Type

This framework is not one-size-fits-all. Weight the layers differently based on what you're building:

| Product Type | Layer 1 Weight | Layer 2 Weight | Layer 3 Weight | Layer 4 Weight |
|-------------|---------------|---------------|---------------|----------------|
| **Flagship consumer ($500+)** | 30% | 20% | 30% | 20% |
| **Mid-range consumer ($200-400)** | 35% | 25% | 25% | 15% |
| **Emerging market ($100-200)** | 40% | 25% | 20% | 15% |
| **Enterprise edge device** | 25% | 30% | 20% | 25% |
| **Developer prototyping** | 20% | 40% | 25% | 15% |

**Key insight:** For emerging market products, Layer 1 (product fit) gets the highest weight because the cost/power constraints are the hardest. For developer prototyping, Layer 2 (engineering feasibility) matters most because the goal is velocity.

---

## My Standard Evaluation Criteria (Quantitative)

For each chip I evaluate, I score these dimensions 1-5:

| Dimension | What I'm Measuring | Why It Matters |
|-----------|------------------|----------------|
| **Inference Performance** | Real-world throughput for our target model | Will users experience acceptable latency? |
| **Power Efficiency** | TOPS per Watt sustained | Determines battery life and thermal design |
| **SDK Maturity** | Documentation quality, bug frequency, support responsiveness | Engineering time is the real cost |
| **Framework Support** | How many popular frameworks run natively | Developer adoption is the moat |
| **Cost Structure** | BOM delta vs non-AI version | Determines retail price viability |
| **Vendor Stability** | Financial health, roadmap commitment, EOL history | Long-term product support |
| **Differentiation** | How unique is this chip's position | Avoid spec-sheet races |

A chip must score ≥ 3.5/5 on the weighted average to proceed.

---

## Common Mistakes I See in AI Hardware Evaluation

```
Mistake 1: Chasing benchmark leaders
→ The chip with the highest MLPerf score is often not the chip that delivers
   the best user experience in your form factor
→ Fix: Always test with your actual model, in your actual form factor, running
   your actual product software

Mistake 2: Ignoring SDK maturity
→ A chip with great silicon but buggy SDK will cost you 6+ months of engineering
   time and ship late
→ Fix: Talk to other companies that have shipped products on this chip.
   Engineers share honest SDK quality assessments.

Mistake 3: Treating AI features as independent
→ AI features compete for the same NPU, memory bandwidth, and power budget
→ Fix: Test all AI features running simultaneously before committing to a chip

Mistake 4: Optimizing for peak performance
→ Peak TOPS is what the chip does when fans are running and power limits are removed
→ Real product: sustained performance with thermal constraints
→ Fix: Always measure sustained performance, not peak

Mistake 5: Treating framework support as a checkbox
→ "Supports PyTorch" means different things in different contexts
→ Fix: Actually try to compile and run your target model before committing
```

---

## The Decision Output Template

For every AI chip I evaluate, I produce this output:

```
Chip: [Name]
Product Fit: [PASS/FAIL] — [Key reason]
Engineering Time: [X months] — [Key risk]
Ecosystem Score: [X/5] — [Key gap]
Strategic Fit: [X/5] — [Key concern]
Weighted Score: [X/5]

Go/No-Go: [GO/NO-GO/RE-EVALUATE in X months]

Notes:
- [Key technical finding]
- [Key business finding]
- [The one thing that would change my decision]
```

This template keeps evaluation consistent across chips and products, and creates a paper trail for future review.

---

*Framework developed from hardware PM experience 2010-2025. Not employer-confidential.*
