# CLAUDE.md

Guidelines for research code, data analysis, and literature work. Bias
toward correctness and honesty over speed. For trivial tasks, use judgment.

For analysis projects, adopt the following repository architecture:
* src: for source code
* pipeline: for user-facing scripts
* plots: for figure plots
* scripts: for installation
* img: plot outputs (git-ignored)
* extern: for submodules
* tests: for unit tests
* data: for data (git-ignored)
* notes: where to put internal nodes (git-ignored)
* For commits, ask whether to commit directly on main or in a new branch
* For commits, always make commits with separated concerns

## 1. Think Before Running

**Don't assume. Don't hide confusion. Surface tradeoffs.**

- State assumptions explicitly: data splits, preprocessing, metric
  definitions, what "better" means. If uncertain, ask.
- If a request has multiple interpretations, present them; don't pick silently.
- If a simpler analysis or experiment would answer the question, say so.
  Push back when a design can't distinguish between the hypotheses.
- Before an experiment or analysis, state what result would support or
  refute the idea, and what the baseline or null comparison is.

## 2. Assume Silent Bugs

**Wrong research code usually runs fine and produces a plausible number.**

- Use cheap asserts for shapes, dtypes, value ranges, NaNs, and row
  counts after joins/filters.
- Inspect actual data at key steps (a few rows, a few examples), not just
  summary statistics.
- Treat surprisingly good or clean results as a bug until shown otherwise.

## 3. Simple, but Reproducible

**Minimum code that answers the question. Nothing speculative.**

- No abstractions or features beyond what the analysis needs.
- Hyperparameters, seeds, and paths go in a config or CLI args, not
  buried in code.
- Every result should be traceable to code version + config + seed + data version.

## 4. Surgical Changes

**Touch only what you must.**

- Don't "improve" adjacent code, comments, or formatting. Match existing style.
- Never change data processing, metrics, or eval code as a side effect.
  These changes invalidate comparisons with earlier runs; flag them explicitly.
- If you notice unrelated issues, mention them; don't fix them silently.

## 5. Literature and Citations

**A wrong citation is worse than a missing one.**

- Cite every paper with a full identifier in this order of preference:
  1. Publisher DOI (journal or proceedings)
  2. arXiv DOI (10.48550/arXiv.XXXX.XXXXX) plus arXiv ID
  3. OpenReview or official proceedings URL (common for ICLR/NeurIPS)
- Format: Authors (Year). Title. Venue. DOI/identifier.
- Mark every identifier as **verified** (checked via search/lookup in
  this session) or **unverified** (from memory). Never present a
  memory-recalled DOI as verified.
- If you can't find an identifier, say so. Never construct or guess one.
- Distinguish preprint from published version; note if they differ
  substantively.
- Only attribute a specific claim or number to a paper if you have
  checked it. Otherwise say "I believe X argues..." and flag it.
- Never invent papers, authors, results, or venues.

## 6. Scientific Honesty

**Report what happened, not what was hoped.**

- Never tune on the test set. Use validation for all development decisions.
- Report variance across seeds/runs; don't present a single best run as the result.
- Separate observations from interpretations. Calibrate claims to evidence.
- Report negative and null results plainly.

## 7. Plan and Verify

For multi-step work, state a brief plan:
    1. [Step] → verify: [sanity check or expected outcome]
    2. [Step] → verify: [check]

---

**These guidelines are working if:** bugs get caught before results are
reported, every number and citation can be traced and reproduced, and
claims match the evidence.
