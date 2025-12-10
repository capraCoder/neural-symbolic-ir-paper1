# Changes Document: Version 3

**Focus:** Technical Rigor Pass

---

## Package Additions

Added mathematical typesetting support:
```latex
\usepackage{amsmath}
\usepackage{amssymb}
```

---

## Abstract Refinements

### 1. Mathematical Notation Standardization

**Original:** "100 million documents"
**Revised:** "$10^8$ documents"

**Original:** "$O(n \cdot d)$"
**Revised:** "$O(nd)$" (standard notation)

**Original:** "substantial cost and latency improvements"
**Revised:** "order-of-magnitude cost improvements" (more specific claim)

---

## Introduction Changes

### 2. Removed Physics Analogy

**Original:** "The underlying physics---the need to minimize comparisons while maximizing recall---remains unchanged."
**Revised:** "The underlying problem---minimizing comparisons while maximizing recall---remains unchanged."

**Rationale:** "Physics" was imprecise metaphor; "problem" is accurate.

---

## Background Section: Technical Precision

### 3. Specific Constraint Parameters

**Original memory specification:** "64KB RAM on early implementations"
**Revised:** "64KB--256KB RAM on early implementations"

**Original storage specification:** "Slow, unreliable disk drives"
**Revised:** "Mechanical disk drives with seek times $\sim$10--50ms"

**Original processing specification:** "Single-core CPUs measured in MHz"
**Revised:** "Single-core CPUs at 4--16 MHz"

**Rationale:** Vague descriptions replaced with concrete specifications.

### 4. B-tree Parameters Added

Added branching factor specification:
> "A separate index mapping terms to record pointers (posting lists), organized as a B-tree with branching factor $m$ typically 50--200. For $k$ unique terms, any term lookup requires $\lceil \log_m k \rceil$ node accesses."

Added numerical example:
> "For $k = 10^6$ terms with $m = 100$, this meant $\lceil \log_{100} 10^6 \rceil = 3$ disk seeks versus $10^6$ sequential comparisons---a factor of $3 \times 10^5$ improvement."

### 5. Variable Distinction: $n$ vs $k$

Changed "$O(\log n)$ lookup" to "$O(\log k)$ lookup" throughout.

**Rationale:** $n$ = documents, $k$ = index terms/clusters. The lookup complexity depends on index size $k$, not document count $n$. This distinction is critical for the Two-Level Theory.

---

## Two-Level Theory: Major Expansion

### 6. Complexity Analysis Subsections

Added dedicated "Complexity Analysis" subsection under Level 1:

```latex
Let $n$ be the number of documents and $d$ the embedding dimension (typically $d \in [384, 4096]$). Exact $k$-nearest-neighbor search requires:
\begin{itemize}
    \item Computing $n$ similarity scores: $O(nd)$ operations
    \item Selecting top-$k$: $O(n \log k)$ with a heap, or $O(n)$ with quickselect
\end{itemize}
```

Added numerical example:
$$nd = 10^9 \times 768 = 7.68 \times 10^{11} \text{ operations per query}$$

Added latency calculation:
> "Even with GPU parallelization achieving $10^{13}$ FLOPS, this requires $\sim$77ms compute per query---before memory bandwidth constraints, which typically dominate."

### 7. Level 2 Complexity Analysis

Added formal analysis:
```latex
For $k$ index entries (cluster centroids, quantized codes, or vocabulary terms) organized in a B-tree with branching factor $m$:
\begin{itemize}
    \item Tree depth: $h = \lceil \log_m k \rceil$
    \item Comparisons per node: $O(\log m)$ with binary search
    \item Total lookup: $O(\log_m k \cdot \log m) = O(\log k)$
\end{itemize}
```

### 8. Expanded Summary Table

**Original columns:** Layer, Function, Complexity
**Revised columns:** Layer, Function, Input, Complexity

New table includes explicit input specification:

| Layer | Function | Input | Complexity |
|-------|----------|-------|------------|
| Level 1 | Semantic encoding | Query text | O(d · L) |
| Level 2 | Structural lookup | Quantized code | O(log k + |P|) |

### 9. Total Complexity Equation

Added formal equation with labeled terms:
$$C_{\text{total}} = \underbrace{O(d \cdot L)}_{\text{encoding}} + \underbrace{O(\log k)}_{\text{navigation}} + \underbrace{O(|P| \cdot d)}_{\text{reranking}}$$

Added numerical breakdown for typical parameters showing bottleneck shift from $O(10^{11})$ to $O(10^8)$.

### 10. Approximation Caveat

Added explicit note:
> "**Note on $O(d + \log k) \approx O(\log k)$:** This approximation holds only when $d$ is treated as a constant (fixed embedding dimension). More precisely, with variable $d$: $O(d) + O(\log k)$, where the $O(d)$ term dominates for small $k$ but becomes negligible relative to the $O(n/k)$ reranking cost for large $n$."

---

## Evidence Section: Precision Improvements

### 11. FAISS Case Study Algorithm

Added numbered algorithm steps:
1. **Training:** Cluster $n$ vectors into $k$ centroids using k-means
2. **Indexing:** Assign each vector to nearest centroid; store in posting list
3. **Query:** Find $p$ nearest centroids ($p \ll k$); search only those posting lists

Added complexity formula:
> "This reduces search from $O(nd)$ to $O(kd + p \cdot n/k \cdot d) = O(d(k + pn/k))$. With optimal $k = \sqrt{n}$ and small $p$, this approaches $O(d\sqrt{n})$---still superlinear, but substantially better than linear."

### 12. SPANN Case Study Memory Specification

Added explicit tiering:
> "**In-memory:** Centroid index (small, $O(k)$ vectors)
> **On-SSD:** Posting lists (large, $O(n)$ vectors)"

### 13. Pattern Summary Format

Changed from bullet list to numbered list for emphasis:
1. **Separation:** Navigation structure distinct from data storage
2. **Hierarchy:** Multi-level organization enabling sublinear access paths
3. **Discretization:** Continuous embeddings mapped to discrete keys
4. **Posting lists:** Keys map to document sets, not individual documents

---

## Neural-to-Symbolic Bridge: Formal Specification

### 14. Mathematical Pipeline Notation

**Original:** `Query → Encoder → ℝᵈ → Quantize → Σ → B-tree → Documents`

**Revised:** Full LaTeX equation with proper typesetting:
$$\underbrace{q}_{\text{query}} \xrightarrow{E(\cdot)} \underbrace{v \in \mathbb{R}^d}_{\text{embedding}} \xrightarrow{Q(\cdot)} \underbrace{s \in \Sigma}_{\text{symbol}} \xrightarrow{I(\cdot)} \underbrace{\{d_1, \ldots, d_m\}}_{\text{documents}}$$

### 15. Formal Component Specifications

Added typed function signatures for each component:

**Encoder:** $E: \mathcal{T} \rightarrow \mathbb{R}^d$
- Complexity: $O(dL)$ where $L$ is sequence length

**Quantizer:** $Q: \mathbb{R}^d \rightarrow \Sigma$
- Three implementation options listed with formulas:
  - Centroid assignment: $Q(v) = \arg\min_{c \in C} \|v - c\|$
  - Product quantization: $Q(v) = (q_1(v_1), \ldots, q_m(v_m))$
  - LSH: $Q(v) = \text{sign}(Wv)$
- Complexity: $O(kd)$ for centroids, $O(d)$ for PQ/LSH

**Index:** $I: \Sigma \rightarrow 2^{\mathcal{D}}$
- Complexity: $O(\log |\Sigma|)$ for B-tree, $O(1)$ amortized for hash

**Reranker:** Complexity $O(|P| \cdot d)$

### 16. New Subsection: Design Parameters

Added "Design Parameters" subsection covering:

**Codebook size $k$:**
- Larger $k$: Smaller posting lists, but more centroids to search
- Optimal: $k \approx \sqrt{n}$ balances navigation and search costs
- FAISS default: $k = 4\sqrt{n}$ (empirically tuned)

**Probe count $p$:**
- Larger $p$: Higher recall, higher latency
- Typical: $p \in [1, 64]$ depending on recall target

**Quantization method:**
- Centroid (IVF): Simple, $k$ symbols
- Product quantization: Exponential codebook ($m^{k'}$ symbols)
- Learned quantization: End-to-end optimized (cite zandieh2025)

### 17. Theoretical Grounding

Added new citation and explicit claim:
> "Information-theoretic analysis by Chen et al. [chen2025] suggests that decomposing semantic entropy from structural entropy is necessary to achieve $O(\log k)$ scaling while maintaining recall guarantees."

---

## Limitations Section: Technical Caveats

### 18. New Caveats Added

**Approximation Quality:**
> "The claim $O(d + \log k) \approx O(\log k)$ requires treating $d$ as constant. For variable or large $d$, the encoding cost may dominate."

**Reranking Costs:**
> "Our complexity analysis assumes posting list search is the bottleneck. For very small $k$ (large posting lists), reranking cost $O(n/k \cdot d)$ dominates and linear scaling returns."

### 19. Expanded Open Questions

Added four new research questions:
1. Optimal $k$ as function of $n$, $d$, and recall target
2. Recursive quantization for $O(\log \log n)$ scaling
3. Joint encoder-quantizer optimization
4. Tight lower bounds for hierarchical retrieval

---

## Sidebar Updates

### 20. First Sidebar: Complexity Added

Added line:
> "**Complexity:** $O(\log k)$ lookup for $k$ index terms"

### 21. Second Sidebar: Mathematical Notation

**Original:** "The **Two-Level Theory**: separate semantic encoding ($O(n \cdot d)$) from structural lookup"

**Revised:** "**Two-Level Theory**: separate semantic encoding ($O(nd)$ naive $\rightarrow$ $O(dL)$ per query) from structural lookup ($O(\log k)$)"

Added practical guidance:
> "**Neural-to-Symbolic Bridge**: Encoder $\rightarrow$ Quantizer $\rightarrow$ Index. Key parameter: codebook size $k \approx \sqrt{n}$."

---

## Summary: Technical Rigor Improvements

| Aspect | V2 | V3 |
|--------|----|----|
| **Complexity notation** | Informal descriptions | Formal $O(\cdot)$ with derivations |
| **Numerical examples** | Few | Multiple worked examples |
| **Component specification** | Prose descriptions | Typed function signatures |
| **Design parameters** | Implicit | Explicit section with tradeoffs |
| **Approximation caveats** | Missing | Explicit conditions stated |
| **B-tree parameters** | Generic | Branching factor $m$, depth $h$ |
| **FAISS algorithm** | Prose | Numbered algorithmic steps |
| **Research questions** | General | Specific with mathematical formulation |

---

## Items Preserved from V2

- All structural additions (Background, Why Now, Limitations sections)
- All epistemic hedging
- Seven-system analysis (TiDAR removed in v1)
- CACM audience calibrations
- Acknowledgment of modern innovation
- Authority control connection
- Author credentials and transparency
