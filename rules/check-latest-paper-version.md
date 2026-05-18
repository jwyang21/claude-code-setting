---
name: verify-paper-metadata
description: Whenever stating any information about a specific paper — venue, year, authors, title, arXiv ID, URL, GitHub link, content summary, numerical results, or any other field — verify ALL fields before asserting. Trust no cached impression. Includes the latest-version check for arXiv content.
---

# Instruction

Whenever you reference a specific paper, you are making multiple **independent claims** — title, authors, arXiv ID, venue, year, GitHub URL, content summary, specific numerical results, etc. Each one is a separate factual claim that must be verified. A "mostly-right" entry with one fabricated field is still misinformation, and the user will catch it.

This is the highest-friction failure mode in survey work: a single fabricated venue ("ACL 2026 Findings") or a single misattributed score ("F1=0.42 on DialSim") destroys trust in the entire entry.

## Rules

### 1. Verify each field independently
Before writing any of these for a paper, confirm each one against the source:
- **arXiv ID** — fetch `arxiv.org/abs/{id}` and confirm the page resolves to the paper you intend
- **Title** — must match arXiv exactly (whitespace/punctuation OK)
- **Authors** — at minimum, first author must match arXiv
- **Year** — match the *latest* arXiv version's submission date
- **Venue** — read the arXiv "Comments" field; for ACL/EMNLP/NAACL also cross-check the ACL Anthology; for ICLR cross-check OpenReview. If neither source confirms, downgrade to "arXiv only".
- **GitHub link** — fetch the URL and confirm the repo exists; do not assume `github.com/{author}/{paper-name}`.
- **Content summary** — must reflect the abstract / paper, not paraphrase from your prior beliefs.
- **Numerical claims** (scores, +X% improvements, dataset sizes) — must come from the abstract, paper body, or an explicit table you've inspected. Don't round, don't transpose, don't invent.

### 2. Latest version first (subsumes the old version-checking rule)
- For arXiv papers, visit `arxiv.org/abs/{id}` to read the version list (e.g., v1 ... v11) before fetching content. Then fetch the highest version's HTML (`arxiv.org/html/{id}v{N}`).
- Later versions may add/remove tables, change numbers, change titles, or add a venue claim that v1 didn't have.
- Cite version for non-trivial claims: *"In v11 Table 2..."*, especially when the answer could change across versions.
- When the user says "it's in the paper" and you don't find it, suspect version mismatch FIRST — re-fetch the latest version before claiming absence.

### 3. Trust the source over your impression
If you "remember" a paper's venue/score/method, that memory is unreliable cache. Treat it as a hypothesis, then verify against arXiv / Anthology / OpenReview / GitHub before stating.

### 4. Conservative downgrade when unverified
When a field cannot be confirmed:
- ❌ Don't make it up.
- ✅ Mark it explicitly: "venue unverified", "(unverified — claimed by .md author)", "(score not stated in abstract; unverified)".
- ✅ For papers with arXiv "Accepted to X" comments but no Anthology entry yet (e.g., during pre-conference window), state both: "ACL 2026 Findings (per arXiv comment; Anthology entry pending)".

### 5. ACL/conference timing awareness
- ACL Anthology entries appear AFTER the conference proceedings publish, not at acceptance time. A paper accepted in April with conference in July won't have an Anthology link yet.
- Workshop papers are NOT main conference papers — distinguish "NeurIPS 2025" from "NeurIPS 2025 SEA Workshop". A workshop accept is a real result but a different claim.
- "Outstanding Paper" / "Best Paper" awards: only a tiny number of papers per conference receive these. Verify on the conference's official awards page before claiming.

### 5a. arXiv "Comments" field is author-supplied — not authoritative

The arXiv Comments field is a **free-text claim by the author**. Authors can write "Accepted to ACL 2026 Findings" without independent verification. Treat this as ONE piece of evidence, not proof. Authoritative venue confirmation requires:
1. **ACL Anthology entry** (post-conference) — for ACL/EMNLP/NAACL papers
2. **OpenReview forum/PDF with decision** — for ICLR/NeurIPS papers
3. **Official conference accepted-papers list** — published by the conference itself

If only the arXiv Comments field claims the venue (and no Anthology / OpenReview / official list confirms), record it as: `arXiv (author claims X — not independently verified)`. Do not promote a self-claim to "verified".

A corollary: a paper with NO venue in Comments may still be at a venue (e.g., GAM had only "18 pages, 6 figures" but had an OpenReview PDF confirming ICLR 2026). Always check OpenReview / Anthology even when Comments is silent.

### 6. When in doubt, don't write it
Better to omit the venue field than to invent one. Better to write "arXiv preprint" than fabricate "ICLR 2026 Workshop MemAgents".

## Failure modes to avoid

- **Asserting a venue from training-data prior** (e.g., "this looks like an ACL paper") instead of checking arXiv comments.
- **Trusting an earlier-version fetch** and confidently saying "this isn't in the paper" when v11 has it.
- **Conflating a workshop with main track** (NeurIPS Workshop ≠ NeurIPS).
- **Promoting "accepted" to "Outstanding Paper"** without verifying the awards list.
- **Inventing GitHub URLs** based on author/paper name patterns.
- **Reusing a score from one paper as if it's another's** (cross-table contamination).
- **Mixing up two papers with similar titles** — e.g., HiGMem (arXiv 2604.18349) ≠ H-MEM (EACL 2026, arXiv 2507.22925). Always anchor on arXiv ID, not title resemblance.

## Operational checklist before writing a paper entry

```
[ ] Fetched arxiv.org/abs/{id} — title matches my intended paper
[ ] Latest version identified; content claims tied to that version
[ ] arXiv "Comments" field read — venue claim sourced from there or downgraded
[ ] If venue claims a published proceeding, cross-checked Anthology/OpenReview
[ ] Authors list checked (at least first author)
[ ] GitHub URL (if cited) actually fetched and exists
[ ] Every numerical claim sourced — abstract, table number, or marked unverified
[ ] No field left as "looks plausible from prior knowledge"
```

If any box is unchecked, either verify now or write "(unverified)" — never leave a confident-sounding but unverified claim.
