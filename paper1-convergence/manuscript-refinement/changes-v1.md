# Changes Log: v1 (Evidence & Hedging)

**Version:** caprazli-neural-scale-v1.tex
**Focus:** Evidence strengthening, epistemic hedging, TiDAR removal

---

## Critical Fix: TiDAR Removal

### Rationale
TiDAR (arXiv:2411.08923) is NOT an information retrieval system. It is "Think in Diffusion, Talk in Autoregression" - an LLM text generation acceleration architecture that combines diffusion and autoregressive decoding for faster token generation. The 5.91x speedup refers to tokens-per-second generation, not retrieval latency.

### Changes Made
1. **Table 1:** Deleted TiDAR row (8 → 7 systems)
2. **Abstract:** Removed "from NVIDIA's TiDAR to Microsoft's SPANN" → "from Meta's FAISS to Microsoft's SPANN"
3. **Section 2.1:** Deleted sentence "NVIDIA's TiDAR acknowledges this implicitly: its ``Think in Diffusion'' phase leverages neural power for semantic encoding, but efficiency gains come from structural processing---Level 2"
4. **Section 5.3:** Deleted "Similarly, TiDAR's two-level processing achieved a 5.91x speedup"
5. **Key Takeaways:** Changed "FAISS, TiDAR, SPANN" → "FAISS, SPANN, DiskANN"
6. **Section 3 intro:** Changed "eight" → "seven" systems
7. **References:** TiDAR citation (liu2024) will be removed in v3 references.bib

---

## Epistemic Hedging Changes

### Abstract
| Original | v1 |
|----------|-----|
| "This convergence is not a coincidence; we argue it is an architecturally inevitable response" | "This convergence, we argue, is not coincidental; it may represent an architecturally inevitable response" |
| "The future of AI scaling does not require new invention. It simply requires remembering" | "The future of AI scaling may not require new invention---it may require remembering" |

### Section 1 (Introduction)
| Original | v1 |
|----------|-----|
| "the industry is unconsciously migrating back" | "the industry appears to be unconsciously migrating back" |
| "This convergence is not technological coincidence. It is likely a mathematical inevitability" | "This convergence, we suggest, is not mere technological coincidence. It may be a mathematical inevitability" |
| "Modern systems aren't innovating. They are converging" | "Modern systems aren't innovating in isolation. They appear to be converging" |

### Section 2 (Two-Level Theory)
| Original | v1 |
|----------|-----|
| "The crisis in scalable information retrieval stems from a category error" | "The crisis in scalable information retrieval stems from what we characterize as a category error" |
| "modern systems fail by ignoring forty years of evidence" | "modern systems struggle when they ignore forty years of evidence" |
| "The incompatibility between approaches appears mathematical" | No change (already hedged) |

### Section 3 (Convergence Evidence)
| Original | v1 |
|----------|-----|
| "Eight independent teams with combined budgets exceeding $10 billion have unknowingly recreated solutions" | "Seven independent teams have unknowingly recreated solutions resembling those" |
| "This precisely describes CDS/ISIS's inverted file structure" | "This approach closely resembles CDS/ISIS's inverted file structure" |
| "The mathematical formulation is identical" | Deleted (overclaim) |
| "These aren't independent discoveries---they're forced convergences" | "These may not be independent discoveries---they may be forced convergences" |

### Section 4 (Historical)
| Original | v1 |
|----------|-----|
| "the direct ancestor of the ragged tensors" | "what some consider a direct ancestor of the ragged tensors" |
| "He proved that hierarchical decomposition was practically mandatory" | "His design demonstrated that hierarchical decomposition was practically mandatory" |
| "We are not witnessing a new invention; we are witnessing the industry migrating" | "We may not be witnessing a new invention; we may be witnessing the industry migrating" |

### Section 5 (Solution)
| Original | v1 |
|----------|-----|
| "Projected Advantages" section | Changed "yield" → "is predicted to yield" |
| "our theoretical analysis predicts: replacing brute-force... could reduce costs by 10x ($2.4M → $240k)" | Removed specific dollar figure; replaced with "could substantially reduce infrastructure costs" |
| "Complexity Collapse" | "Complexity Reduction" (less hyperbolic) |

### Section 6 (Implications)
| Original | v1 |
|----------|-----|
| "The convergence on CDS/ISIS principles is a roadmap for the future" | "The convergence on CDS/ISIS principles may serve as a roadmap for the future" |
| "Our framework corrects this" | "Our framework could correct this" |
| "we democratize access to semantic search, potentially redirecting billions" | "we may democratize access to semantic search, potentially redirecting computational resources" |
| "recursive decomposition becomes mandatory" | "recursive decomposition may become mandatory" |

### Section 7 (Conclusion)
| Original | v1 |
|----------|-----|
| "The $4.7 billion crisis in information retrieval isn't a failure of technology---it's a failure of memory" | "The scaling crisis in information retrieval may not be a failure of technology---it may be a failure of memory" |
| "Our analysis of eight modern systems reveals a unified truth" | "Our analysis of seven modern systems reveals what appears to be a unified truth" |
| "This convergence suggests that these principles are fundamental constants" | "This convergence suggests that these principles may be fundamental constants" |
| "The $4.7 billion question has a free answer. It's been waiting in UNESCO archives for forty years." | "The architecture for the future may have been waiting in UNESCO archives for forty years." |

---

## Table 1 Improvements

### Column Header Changes
| Original | v1 |
|----------|-----|
| "Hidden Principle" | "Analogous Principle" |
| "Rediscovery" | "Mapping" |

### Row-Level Changes
- Removed TiDAR row entirely
- For SPANN: Changed "Field Independence Axiom" → "Hierarchical Decomposition" (author's terminology not in original paper)
- For DiskANN: Changed "B-tree Navigation" → "Hierarchical Navigation" (more accurate - Vamana graphs aren't B-trees)

---

## Economic Claims

### Removed/Modified
| Original | v1 | Rationale |
|----------|-----|-----------|
| "$4.7 billion" (abstract, conclusion) | Removed | Unsourced market figure |
| "$2.4M → $240k" (abstract, Section 5.2) | "could substantially reduce infrastructure costs" | Literature shows highly variable costs; specific figure unsourced |
| "combined budgets exceeding $10 billion" | Removed | Unsourced |
| "potentially redirecting billions in wasted compute" | "potentially redirecting computational resources" | Unsourced quantification |

---

## Sidebar Box Changes

### CDS/ISIS Box
| Original | v1 |
|----------|-----|
| "30 million records on 64KB RAM (1985)" | "Designed to handle millions of records on 64KB RAM (1985)" |
| "Poverty-driven design achieves mathematical optimality" | "Constraint-driven design often achieves mathematical efficiency" |

### Key Takeaways Box
| Original | v1 |
|----------|-----|
| "Modern IR systems (FAISS, TiDAR, SPANN) are unconsciously recreating" | "Modern IR systems (FAISS, SPANN, DiskANN) appear to be unconsciously recreating" |
| "Our Neural-to-Symbolic Bridge framework synthesizes these principles to project 10x cost reduction" | "Our Neural-to-Symbolic Bridge framework synthesizes these principles to project substantial cost reduction" |
| "Constraint is the mother of optimal architecture" | "Constraint is often the mother of optimal architecture" |
| "we must look to 'legacy' systems" | "we may need to look to 'legacy' systems" |

---

## Summary of v1 Changes

**Total edits:** ~45 changes

**Categories:**
- TiDAR removal: 7 locations
- Epistemic hedging: ~25 softened claims
- Economic figure removal: 4 locations
- Table improvements: 3 structural changes
- Sidebar updates: 6 changes

**Word count impact:** Net reduction of ~150 words (removal of TiDAR content and unsourced claims)

**Evidence strength:** Improved by removing indefensible claims; core thesis preserved
