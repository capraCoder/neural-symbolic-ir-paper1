# Comparison Report: Manuscript Versions

**Document:** The Authority of Neural Scale
**Versions Compared:** Original → v1 → v2 → v3
**Report Date:** 2025-12-10

---

## Executive Summary

This report compares four versions of the manuscript across key dimensions. Each version builds incrementally on the previous, with specific improvements:

| Version | Focus | Key Changes |
|---------|-------|-------------|
| **Original** | Initial submission | Contains TiDAR error, unsourced claims |
| **v1** | Evidence & Hedging | TiDAR removed, claims softened, economic figures removed |
| **v2** | CACM Calibration | Added background section, limitations, "Why Now?" |
| **v3** | Technical Rigor | Formal equations, complexity justification, implementable framework |

**Recommendation:** Submit **v3** for CACM review. It combines the strongest evidence base (v1), audience accessibility (v2), and technical credibility (v3).

---

## Comparison Matrix

### Structural Changes

| Dimension | Original | v1 | v2 | v3 |
|-----------|----------|----|----|-----|
| **Sections** | 7 | 7 | 9 | 9 |
| **Word Count** | ~3,500 | ~3,350 | ~4,400 | ~5,000 |
| **Tables** | 1 (8 systems) | 1 (7 systems) | 1 (7 systems) | 1 (7 systems) |
| **Equations** | 3 inline | 3 inline | 3 inline | 10 numbered |
| **Sidebars** | 2 | 2 | 2 | 2 |

### Content Comparison

| Section | Original | v1 | v2 | v3 |
|---------|----------|----|----|-----|
| Introduction | Standard | Hedged | + "Why Now?" subsection | Same as v2 |
| Background | None | None | **NEW:** CDS/ISIS context | Same as v2 |
| Two-Level Theory | Present | Present | Present | + Complexity Decomposition subsection |
| Convergence Evidence | 8 systems | 7 systems | 7 systems | 7 systems |
| Historical | Present | Present | Present | Same |
| Neural-to-Symbolic Bridge | Conceptual | Conceptual | Conceptual | **Implementable:** 3 quantization approaches, formal complexity |
| Limitations | None | None | **NEW:** 3 subsections | Updated with equation references |
| Implications | Present | Hedged | Hedged | Formalized (align environment) |
| Conclusion | Strong claims | Hedged | Hedged | Same |

---

## Dimension-by-Dimension Analysis

### 1. Evidence Quality

| Metric | Original | v1 | v2 | v3 |
|--------|----------|----|----|-----|
| Unsupported claims | 5+ | 0 | 0 | 0 |
| TiDAR error | Present | **FIXED** | Fixed | Fixed |
| Economic figures | $4.7B, $2.4M→$240k | Removed | Removed | Removed |
| Table accuracy | "Hidden Principle" | "Analogous Principle" | Same | Same |

**Winner:** v1/v2/v3 (tied) - all have equivalent evidence quality

---

### 2. Epistemic Hedging

| Claim Type | Original | v1 | v2 | v3 |
|------------|----------|----|----|-----|
| "This is" statements | 15+ | ~5 | ~5 | ~5 |
| "This may be" statements | ~3 | ~15 | ~15 | ~15 |
| "We argue" vs "We prove" | Prove-like | Argue | Argue | Argue |
| Falsifiability criteria | None | None | **Present** | Present |

**Winner:** v2/v3 (tied) - hedging plus explicit limitations

---

### 3. CACM Audience Fit

| Metric | Original | v1 | v2 | v3 |
|--------|----------|----|----|-----|
| CDS/ISIS background | Assumed | Assumed | **Provided** | Provided |
| "Why now?" addressed | No | No | **Yes** | Yes |
| Limitations section | No | No | **Yes** | Yes |
| Alternative interpretations | No | No | **Yes** | Yes |
| Technical accessibility | Medium | Medium | **High** | High |

**Winner:** v2/v3 (tied) - both provide necessary context

---

### 4. Technical Rigor

| Metric | Original | v1 | v2 | v3 |
|--------|----------|----|----|-----|
| Numbered equations | 0 | 0 | 0 | **10** |
| Complexity justification | Assertion | Assertion | Assertion | **Formal proof** |
| Quantization approaches | 0 | 0 | 0 | **3 (k-means, PQ, LSH)** |
| End-to-end complexity | None | None | None | **Equation 10** |
| Cross-references | None | None | None | **8+ equation refs** |

**Winner:** v3 - substantially more rigorous

---

### 5. Novelty & Contribution Clarity

| Metric | Original | v1 | v2 | v3 |
|--------|----------|----|----|-----|
| Core thesis clear | Yes | Yes | Yes | Yes |
| Two-Level Theory | Proposed | Proposed | Proposed | **Formalized** |
| Neural-to-Symbolic Bridge | Conceptual | Conceptual | Conceptual | **Implementable** |
| Falsifiability | None | None | **Stated** | Stated |

**Winner:** v3 - clearest contribution with implementation path

---

## Trade-off Analysis

### v1 Trade-offs
| Gained | Lost |
|--------|------|
| Evidence credibility | Bold rhetorical impact |
| Removes factual errors | Some memorable phrases |
| Academic tone | Journalistic punch |

**Net Assessment:** Necessary foundation for any submission

---

### v2 Trade-offs
| Gained | Lost |
|--------|------|
| CACM accessibility | Conciseness (~900 words added) |
| Reviewer preemption | Fast reading experience |
| Intellectual honesty | Confident voice (sometimes) |

**Net Assessment:** Appropriate for CACM's broad audience

---

### v3 Trade-offs
| Gained | Lost |
|--------|------|
| Technical credibility | Accessibility for non-technical readers |
| Implementability | Conceptual simplicity |
| Mathematical rigor | Some may find equations intimidating |

**Net Assessment:** Strongest for reviewers who want to see the math

---

## Recommendation Matrix

| Submission Venue | Recommended Version | Rationale |
|------------------|---------------------|-----------|
| **CACM** | v3 | Technical rigor + accessibility |
| **TOIS/IRJ** | v3 | Needs mathematical formalism |
| **Blog/Medium** | v1 | More accessible, maintains impact |
| **arXiv preprint** | v3 | Full technical detail |
| **Conference talk** | v2 | Background context helpful |

---

## Specific Changes Summary

### Changes from Original → v1 (45 changes)
- **Critical:** TiDAR removal (7 locations)
- **Hedging:** 25 softened claims
- **Removed:** 4 economic figures
- **Table:** 3 terminology changes

### Changes from v1 → v2 (3 major additions)
- **NEW:** Section 1.1 "Why Now?" (~210 words)
- **NEW:** Section 2 Background (~350 words)
- **NEW:** Section 7 Limitations (~400 words)
- **Removed:** 2 paragraphs from intro (~80 words)

### Changes from v2 → v3 (10 equation additions)
- **NEW:** 10 numbered equations with labels
- **NEW:** Section 3.4 Complexity Decomposition
- **NEW:** Section 6.2 Quantization Function Design
- **NEW:** Section 6.3 Complexity Analysis
- **Updated:** Key Takeaways references equations
- **Updated:** Limitations references equation numbers

---

## Risk Assessment

| Version | Risk Level | Primary Risks |
|---------|------------|---------------|
| Original | **HIGH** | TiDAR error → immediate rejection |
| v1 | **MEDIUM** | Lacks reviewer preemption |
| v2 | **LOW-MEDIUM** | May seem too hedged |
| v3 | **LOW** | Comprehensive but long |

---

## Final Recommendation

**Submit v3** for the following reasons:

1. **No Factual Errors:** TiDAR removed, economic claims removed
2. **Academic Rigor:** 10 numbered equations, formal complexity analysis
3. **Intellectual Honesty:** Explicit limitations and falsifiability
4. **CACM Accessibility:** Background section for unfamiliar readers
5. **Implementable Framework:** Three concrete quantization approaches

**Confidence Level:** HIGH

---

## Appendix: File Inventory

| File | Status | Purpose |
|------|--------|---------|
| `caprazli-neural-scale.tex` | Original (preserved) | Reference baseline |
| `caprazli-neural-scale-v1.tex` | Complete | Evidence & hedging |
| `caprazli-neural-scale-v2.tex` | Complete | CACM calibration |
| `caprazli-neural-scale-v3.tex` | Complete | Technical rigor |
| `references-v3.bib` | Complete | TiDAR removed, kraska2018 added |
| `changes-v1.md` | Complete | Changelog v1 |
| `changes-v2.md` | Complete | Changelog v2 |
| `changes-v3.md` | Complete | Changelog v3 |
| `initial-assessment.md` | Complete | Phase 1 analysis |
| `factual-verification.md` | Complete | Phase 3 verification |
| `comparison-report.md` | Complete | This document |
