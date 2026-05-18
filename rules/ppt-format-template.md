# Instruction

Whenever creating any `.pptx` file, apply the following design specs.

## Visual design

- **Slide size**: 10 × 5.63 inches (widescreen 16:9)
- **Background**: white (#FFFFFF)
- **Header bar**: black (#000000) rectangle at top with white (#FFFFFF) text
- **Font**: Calibri for all text
- **Emphasis in body**: use **bold**, underline, red, or blue — choose appropriately per context
- **Page numbers**: NEVER create page numbers unless the user explicitly requests them
- Avoid other styling unless explicitly requested

## Paper survey slide requirements (apply whenever creating/editing paper survey slides)

### Content flow — always structure each paper in this order:
1. **What** — what the authors built/proposed (task formulation, input/output)
2. **Why** — motivation (existing challenges, limitations of prior work)
3. **How** — method overview (architecture, key mechanisms)
4. **Did it really work?** — results (benchmarks, key numbers)
5. **So what?** — contribution and implications for our work

### Slide count and time budget
- Total presentation ≤ 1 hour.
- Allocate ~4–5 slides per paper; ~2–3 min per slide.
- Create additional slides beyond the requested range if needed — always report the final slide range (e.g., "slides 3–17").

### Verbosity
- Be concise: audience can read the slide. One idea per bullet. No full sentences where a fragment suffices.
- Detailed enough that a cold reader grasps the what/why/how without reading the paper.
- Never pad — if a section fits in 3 bullets, don't stretch to 6.

### Presenter persona
- The presenter is a **graduate student in AI** researching long-term dialogue-based QA.
- Current focus: designing a novel **agentic memory system + retrieval method** for long-term conversational QA, novel enough for a conference/journal paper.
- Frame content from this perspective: what can we learn or reuse? What are the gaps?
- Include a brief "Our perspective" or "Takeaway" section per paper noting relevance to this research.

### Audience
- Primary: AI-majoring graduate student colleagues and/or an advisor.
- Assume ML background — no need to explain standard concepts (attention, embeddings, etc.).
- Advisor expects: clear What/Why/How, honest assessment of results, and your own critical perspective.

### Cross-paper summary
- When presenting 2+ papers in one session, include a comparison slide (table: memory structure, retrieval method, benchmark, key advantage) and a takeaways slide.
