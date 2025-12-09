<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# PROMPT 5: Vector Quantization Theory for IR

Main takeaway:
There are now precise **theoretical conditions under which dimension reduction and vector quantization preserve nearest‑neighbor structure and retrieval ranking**, alongside **nonasymptotic distortion bounds** from classical quantization theory and **recent (2023–2025) work on learned/discrete representations and embedding quantization** that quantifies the empirical loss–efficiency trade‑off. These give you both (i) provable ordering guarantees and (ii) realistic bounds on how much you can compress before retrieval degrades.

***

### Key Finding 1 – Explicit “ranking preserved under quantization” conditions (QPAD, 2025)

- **Direct quote / specific claim**

QPAD (Quantile-Preserving Approximate Dimension Reduction) introduces an unsupervised DR layer that is explicitly designed to **preserve nearest‑neighbor rankings for ANN search**, and proves a sufficient condition under which **nearest‑neighbor identity is unchanged after projection and quantization**:

> “We therefore seek an unsupervised, neighborhood-aware DR method that (a) explicitly preserves the ranking of true k-NNs… Our approach directly optimizes relative neighborhood rankings so that, after projection, each point’s true neighbors remain closer than non-neighbors.”[^1]

QPAD defines a **quantization‑stability criterion**: if the gap between the projected distances to a true neighbor $u$ and a non‑neighbor $v$ is large enough compared to the quantization noise, the NN identity is guaranteed to be preserved:

> “If

> $$
> \|M x_q - M x_u\|_2 - \|M x_q - M x_v\|_2 > 2\sqrt{m}\,\varepsilon,
>
$$

> then the nearest-neighbor identity is preserved under quantization.”[^1]
- **Source with date**

QPAD: “Quantile-Preserving Approximate Dimension Reduction (QPAD)”, arXiv preprint, September 2025.[^1]
- **Why this matters for our paper**

This gives a **clean, directly-usable sufficient condition** for when DR + subsequent quantization **provably leaves retrieval ordering intact**:
    - The margin between true and false neighbors after projection must exceed a **quantization‑noise radius** $2\sqrt{m}\varepsilon$, where $m$ is the reduced dimension and $\varepsilon$ bounds per‑coordinate noise.[^1]
    - It explicitly connects **local geometry (k‑NN margins)** to **index/quantization noise**, giving a handle for theoretical sections where you want to say: “If our learned projection achieves margin $\gamma$ and our quantizer has noise ≤ $\varepsilon$, then the top‑k set is unchanged.”
    - QPAD is designed to be **inserted on top of precomputed embeddings** with no label supervision and is evaluated directly on **Recall@k** of neighbors before vs. after projection and quantization, so it is structurally very close to dense‑IR practice.[^1]

***

### Key Finding 2 – Fundamental bit‑complexity for binary / 1‑bit quantization preserving distances

- **Direct quote / specific claim**

Yi et al. study **binary embeddings** (one‑bit quantization of JL embeddings) and prove lower bounds on the number of bits needed so that Hamming distances approximate original distances for all pairs of $N$ points within additive error $\delta$:

> “We provide lower bounds for both data-oblivious and data-aware embeddings… any binary embedding oblivious to the set of points requires $m = \Omega(\frac{1}{\delta^{2}}\log N)$ bits and a similar lower bound for non-oblivious embeddings into Hamming distance.”[^2]

They define binary embeddings that are exactly **“one-bit quantization of a standard JL embedding”** and prove that if $m$ satisfies this bound, the binary Hamming distance $\mathrm{d_H}$ approximates the original distance $d(x,y)$ for all pairs with error at most $\delta$.[^2]
- **Source with date**

X. Yi et al., “Binary Embedding: Fundamental Limits and Fast Algorithm,” technical report (widely cited; pre‑2018 but foundational).[^2]
- **Why this matters for our paper**
    - It gives a **quantitative bit‑complexity vs. distortion trade‑off** for **1‑bit vector quantization** (sign of random projections) with **uniform worst‑case guarantees** over all pairs $(x_i,x_j)$.
    - For IR, “distortion ≤ $\delta$” at the Hamming level implies **pairwise distance ordering is approximately preserved**, and nearest neighbors (with sufficiently large relative margin) remain nearest after quantization.
    - This is the **binary analogue of JL**: the result justifies that with $m = O(\delta^{-2}\log N)$ bits per vector, **ranking stability is guaranteed up to an error band**, which matches the intuition behind Hamming‑based ANN indexes.

***

### Key Finding 3 – Nonasymptotic distortion bounds for vector quantization in Hilbert spaces

- **Direct quote / specific claim**

Lerasle and Lugosi provide **nonasymptotic upper bounds** on the **expected mean‑squared distortion** of optimal vector quantizers in Hilbert spaces, showing that under suitable assumptions, the distortion converges at rate $O(1/n)$ in the sample size:

> “Recent results in quantization theory show that the mean-squared expected distortion can reach a rate of convergence of $O(1/n)$, where $n$ is the [sample size].”[^3]
- **Source with date**

M. Lerasle, G. Lugosi, “Nonasymptotic bounds for vector quantization in Hilbert spaces,” *Annals of Statistics* 43(2), 2015.[^3]
- **Why this matters for our paper**
    - Gives **rigorous, distribution‑free bounds** on **information loss (distortion)** as a function of **codebook size** and data sample size.
    - This is the right technical backbone for statements like: “Under standard assumptions (bounded support / sub‑Gaussian tails), the distortion of empirically learned codebooks converges to the population optimum at rate $O(1/n)$, so information loss from finite‑sample learning can be controlled.”
    - While not IR‑specific, these nonasymptotic bounds can be **combined with margin‑based retrieval conditions** (as in QPAD) to say: if **distortion ≤ margin/2**, nearest‑neighbor and ranking structure is preserved.

***

### Key Finding 4 – Embedding dimension limits for representing all retrieval orderings (DeepMind LIMIT, 2025)

- **Direct quote / specific claim**

DeepMind’s LIMIT paper studies **combinatorial limits** of single‑vector embeddings for top‑k retrieval:

> “We provide a theoretical connection that shows that embedding models cannot represent all combinations of top‑k documents until they have a large enough embedding dimension $d$.”[^4]

and:

> “We connect known results in learning theory, showing that the number of top-k subsets of documents capable of being returned as the result of some query is limited by the dimension of the embedding.”[^5]
- **Source with date**

O. Weller et al., “On the Theoretical Limitations of Embedding-Based Retrieval,” arXiv preprint, August 2025 (Google DeepMind).[^4][^5]
- **Why this matters for our paper**
    - This gives a **dimension lower bound** for embedding‑based retrieval: beyond information loss from quantization, there is a **fundamental capacity limit** on how many distinct top‑k rankings a fixed‑dimensional embedding can realize.
    - It supports a narrative like: even with perfect distance preservation and no quantization, **some retrieval tasks require exponentially large dimension** in the worst case; quantization then further shrinks the set of representable rankings.
    - For your argument, this allows a clean separation of:
        - **Capacity limits (embedding dimension)**
        - **Representation noise (quantization, ANN index noise)**
        - and to argue where vector quantization “sits” in the stack of losses.

***

### Key Finding 5 – Learned quantization for IR: constrained clustering \& PQ (RepCONC, 2023)

- **Direct quote / specific claim**

RepCONC is a 2023 IR model that **jointly learns dual encoders and product quantization codebooks** as constrained clustering to get **discrete document representations** and efficient ANN retrieval:

> “We… propose a novel retrieval model that learns discrete representations via constrained clustering. RepCONC jointly trains dual-encoders and the Product Quantization (PQ) method to learn discrete document representations and enables fast approximate NNS with compact indexes.”[^6]

It also introduces a **uniform clustering constraint**:

> “We also introduce a uniform clustering constraint to maximize the representation distinguishability. We conduct experiments on widely-adopted ad-hoc retrieval [benchmarks].”[^6]
- **Source with date**

H. Zhang et al., “Learning Discrete Representations via Constrained Clustering for Efficient Ad-hoc Retrieval (RepCONC),” *IJCAI 2023*.[^6]
- **Why this matters for our paper**
    - RepCONC is a **learned quantization framework specifically for IR**, not just generic ANN.
    - It models PQ as **constrained clustering** in the joint encoder–codebook space, linking **codebook distortion minimization** to **retrieval effectiveness**.
    - Although it is empirically evaluated (NDCG/Recall) rather than providing explicit distortion bounds, it is a key recent **learned-vector-quantization‑for‑IR** reference to pair with your more theoretical results (QPAD, binary embedding, classical quantization).

***

### Key Finding 6 – Empirical bounds: quantization with near‑lossless retrieval quality at large speed/size gains (industry, 2023–2024)

These are not formal theorems but provide **strong empirical constraints** on how much information loss is tolerable in real IR systems.

#### 6a. HuggingFace 2024 – Binary and scalar embedding quantization

- **Direct quotes / specific claims**

HuggingFace engineering work quantifies the trade‑off between float32, int8, and binary quantization of dense embeddings for MTEB Retrieval:

> “This quantization can reduce the memory demands of the database by a factor of four or eight.”[^7]

and more precisely (summarizing their table):

> “Memory \& Index size savings: float32 1x, int8/uint8 exactly 4x, binary/ubinary exactly 32x… Retrieval Speed: float32 1x, int8/uint8 up to 4x, binary/ubinary up to 45x… Percentage of default performance: float32 100%, int8/uint8 ~99.3%, binary/ubinary ~96%.”[^8]
- **Source with date**

HuggingFace blog, “Binary and Scalar Embedding Quantization for Significantly Faster Retrieval,” November 2024.[^8]
- **Why this matters**
    - Shows that **4x–32x compression** and **up to ~45x speedup** can be achieved **with <4% relative loss in retrieval quality** on large benchmarks.[^8]
    - Empirically supports the claim that **embedding spaces are over‑parameterized for IR**, and that substantial quantization noise is tolerable before rankings meaningfully change.


#### 6b. Qdrant 2023 – Binary quantization and over‑parameterization

- **Direct quote / specific claim**

Qdrant’s analysis of binary quantization for vector search claims:

> “In exchange for reducing our 32 bit embeddings to 1 bit embeddings we can see up to a 40x retrieval speed up gain! One of the reasons vector search still works with such a high compression rate is that these large vectors are over-parameterized for retrieval.”[^9]
- **Source with date**

Qdrant blog, “Binary Quantization – Vector Search, 40x Faster,” September 2023.[^9]
- **Why this matters**
    - Explicitly points out **over‑parameterization for retrieval vs. ranking/clustering**, aligning with LIMIT’s theoretical results and your thesis that much of the “extra” information can be discarded without killing IR performance.[^9]
    - Provides concrete **speedup figures (~40x) at extreme 1‑bit compression** that you can contrast with theoretical bit‑complexity results.


#### 6c. 4‑bit quantization for RAG embeddings (2023)

- **Direct quote / specific claim**

A 2023 arXiv paper on 4‑bit quantization for vector‑embedding RAG databases reports:

> “This quantization can reduce the memory demands of the database by a factor of four or eight… Our findings indicate that 8‑bit quantization maintains retrieval accuracy with only slight degradation. Group-wise quantization can alleviate some of the accuracy loss encountered with 4‑bit quantization.”[^7]
- **Source with date**

“4bit-Quantization in Vector-Embedding for RAG,” arXiv preprint, December 2023.[^7]
- **Why this matters**
    - Provides **concrete performance observations** at 8‑bit and 4‑bit resolutions for RAG scenarios, which are directly relevant for IR‑style retrieval on text corpora.
    - Confirms that **8‑bit quantization is almost lossless for retrieval accuracy**, while more aggressive 4‑bit schemes need **group‑wise or learned quantization** to keep rankings stable.[^7]

***

### Numbers / Statistics (for quick reference)

- **Binary / scalar quantization vs float32 (HuggingFace 2024)**[^8]
    - Memory \& index size:
        - float32: $1\times$
        - int8/uint8: **$4\times$ smaller**
        - binary/ubinary: **$32\times$ smaller**
    - Retrieval speed (CPU exact search on MTEB Retrieval, mxbai‑embed‑large‑v1, 1024‑D):
        - float32: baseline $1\times$
        - int8: **up to $4\times$ speedup**
        - binary: **up to $45\times$ speedup**
    - Performance vs float32:
        - int8: **≈99.3% of default performance**
        - binary: **≈96% of default performance**[^8]
- **Qdrant binary quantization (2023)**
    - 32‑bit → 1‑bit embeddings: **up to $40\times$ retrieval speedup**.[^9]
- **4‑bit quantization for RAG (2023)**
    - Memory reduction by **factor 4–8**.
    - 8‑bit quantization: **“only slight degradation”** in retrieval accuracy; group‑wise 4‑bit helps mitigate loss.[^7]
- **Binary embedding lower bound (theoretical)**
    - Any oblivious binary embedding achieving additive distortion ≤ $\delta$ on all $\binom{N}{2}$ pairs needs

$$
m = \Omega\!\left(\frac{1}{\delta^2}\log N\right)
$$

bits per vector.[^2]
- **QPAD’s quantization‑stability condition (theoretical)**
    - If for query $x_q$, true neighbor $u$ and non‑neighbor $v$,

$$
\|M x_q - M x_u\|_2 - \|M x_q - M x_v\|_2 > 2\sqrt{m}\,\varepsilon,
$$

then the nearest‑neighbor identity is **guaranteed to be preserved** after quantization noise bounded by $\varepsilon$.[^1]
- **Nonasymptotic distortion for vector quantization**
    - Under appropriate conditions, optimal mean‑squared distortion can achieve **rate $O(1/n)$** in sample size $n$.[^3]

***

### Citations

(Each line: title, venue or type, year, with citation id.)

- QPAD: “Quantile-Preserving Approximate Dimension Reduction (QPAD),” arXiv preprint, 2025.[^1]
- “On the Theoretical Limitations of Embedding-Based Retrieval,” arXiv preprint (Google DeepMind), 2025.[^5][^4]
- X. Yi et al., “Binary Embedding: Fundamental Limits and Fast Algorithm,” technical report.[^2]
- M. Lerasle, G. Lugosi, “Nonasymptotic bounds for vector quantization in Hilbert spaces,” *Annals of Statistics*, 2015.[^3]
- H. Zhang et al., “Learning Discrete Representations via Constrained Clustering for Efficient Ad-hoc Retrieval (RepCONC),” *IJCAI 2023*.[^6]
- HuggingFace, “Binary and Scalar Embedding Quantization for Significantly Faster Retrieval,” engineering blog, 2024.[^8]
- Qdrant, “Binary Quantization – Vector Search, 40x Faster,” blog, 2023.[^9]
- “4bit-Quantization in Vector-Embedding for RAG,” arXiv preprint, 2023.[^7]
- “Alignment Quantization With ADMM-Based Correlation Preservation (AlignQ),” *CVPR 2022*.[^10]
- “Vector Quantization – Data Compression” (lecture notes, Freie Universität Berlin).[^11]
- “Distribution Preserving Quantization,” PhD thesis (DiVA portal).[^12]
- “Order Preserving Hashing for Approximate Nearest Neighbor Search,” Microsoft Research, ACM MM 2013.[^13][^14]
- “Rank Quantization,” Roy Schwartz et al., technical report.[^15]
- “Unleashing the Full Potential of Product Quantization for Large-Scale Face Recognition,” *NeurIPS 2023*.[^16]
- “Semantic-Aware Adversarial Training for Reliable Deep Hashing,” arXiv / ICCV‑adjacent, 2023.[^17][^18]
- “Deep Hashing with Semantic Hash Centers for Image Retrieval,” *Neurocomputing* or related journal.[^19]
- “Fine-grained similarity semantic preserving deep hashing for cross-modal retrieval,” *Frontiers in Physics*, 2023.[^20]
- Survey: “Information Retrieval: Recent Advances and Beyond,” 2023.[^21]
- Qdrant, “What is Vector Quantization?,” blog, 2024.[^22]
<span style="display:none">[^23][^24][^25][^26][^27][^28][^29][^30][^31][^32][^33][^34][^35][^36][^37][^38][^39][^40][^41][^42][^43][^44][^45][^46][^47][^48]</span>

<div align="center">⁂</div>

[^1]: https://arxiv.org/html/2504.16335v2

[^2]: https://users.ece.utexas.edu/~cmcaram/pubs/binary_embedding.pdf

[^3]: https://projecteuclid.org/journals/annals-of-statistics/volume-43/issue-2/Nonasymptotic-bounds-for-vector-quantization-in-Hilbert-spaces/10.1214/14-AOS1293.pdf

[^4]: https://arxiv.org/html/2508.21038v1

[^5]: https://arxiv.org/abs/2508.21038

[^6]: https://www.ijcai.org/proceedings/2023/0728.pdf

[^7]: https://arxiv.org/html/2501.10534v1

[^8]: https://huggingface.co/blog/embedding-quantization

[^9]: https://qdrant.tech/articles/binary-quantization/

[^10]: https://openaccess.thecvf.com/content/CVPR2022/papers/Chen_AlignQ_Alignment_Quantization_With_ADMM-Based_Correlation_Preservation_CVPR_2022_paper.pdf

[^11]: https://iphome.hhi.de/schwarz/assets/dc/11-VectorQuant.pdf

[^12]: http://www.diva-portal.org/smash/get/diva2:437204/FULLTEXT02.pdf

[^13]: https://dl.acm.org/doi/10.1145/2502081.2502100

[^14]: https://www.microsoft.com/en-us/research/wp-content/uploads/2017/01/ACMMM13-OrderPreservingHashing.pdf

[^15]: https://schwartz.cswp.cs.technion.ac.il/wp-content/uploads/sites/68/2016/12/RQ-KLSV13.pdf

[^16]: https://proceedings.neurips.cc/paper_files/paper/2023/file/c2469e35d469e3c0eca09dbe484eb474-Paper-Conference.pdf

[^17]: https://arxiv.org/abs/2310.14637

[^18]: https://arxiv.org/html/2310.14637v2

[^19]: https://dl.acm.org/doi/10.1145/3749983

[^20]: https://www.frontiersin.org/journals/physics/articles/10.3389/fphy.2023.1194573/epub

[^21]: https://www.di.ubi.pt/~hugomcp/doc/Survey_Information_Retrieval_2023.pdf

[^22]: https://qdrant.tech/articles/what-is-vector-quantization/

[^23]: https://scholar.google.com/citations?view_op=view_citation\&hl=en\&user=KEmF6jcAAAAJ\&citation_for_view=KEmF6jcAAAAJ%3AzYLM7Y9cAGgC

[^24]: http://www.mi.sanu.ac.rs/~ai_conf/2025/AI_Conference_Book_of_Abstracts.pdf

[^25]: https://www.bhumipublishing.com/wp-content/uploads/2025/05/Trends-in-Computer-Science-and-Information-Technology-Research-1.pdf

[^26]: https://www.purdue.edu/undergrad-research/conferences/summer/archive/AbstractBook_Summer2025.pdf

[^27]: http://lonepatient.top/2025/09/19/arxiv_papers_2025-09-19

[^28]: https://www.youtube.com/watch?v=1ftmVDwdeO0

[^29]: https://www.linkedin.com/posts/sagarjain2_ever-feel-like-your-embedding-based-retrieval-activity-7367347997866696704-FZLU

[^30]: https://academ.us/list/cs/

[^31]: https://rlj.cs.umass.edu/2024/papers/RLJ_RLC_2024_84.pdf

[^32]: https://aclanthology.org/2024.blackboxnlp-1.8.pdf

[^33]: https://www.linkedin.com/posts/abhishekdas93_limitations-of-embedding-based-retrieval-activity-7370409506570235904-3MRa

[^34]: https://ml-research.github.io/NeuralConceptBinder/

[^35]: https://github.com/google-deepmind/limit

[^36]: https://aclanthology.org/2025.findings-acl.644.pdf

[^37]: https://staff.fnwi.uva.nl/m.derijke/wp-content/papercite-data/pdf/liu-2024-robust-arxiv.pdf

[^38]: https://www.youtube.com/watch?v=5okkh7oUtJo

[^39]: https://arxiv.org/html/2510.18604v1

[^40]: https://openreview.net/forum?id=sTlL1rwGVb

[^41]: http://proceedings.mlr.press/v32/zhangd14.pdf

[^42]: https://arxiv.org/html/2505.21895v1

[^43]: https://www.sciencedirect.com/science/article/abs/pii/S2214212622001806

[^44]: https://arxiv.org/html/2504.10816v2

[^45]: https://openaccess.thecvf.com/content/ICCV2023/html/Chen_Overcoming_Forgetting_Catastrophe_in_Quantization-Aware_Training_ICCV_2023_paper.html

[^46]: https://keyurramoliya.com/posts/Muvera/

[^47]: https://www.sciencedirect.com/science/article/abs/pii/S0925231221019299

[^48]: https://www.shaped.ai/blog/the-vector-bottleneck-limitations-of-embedding-based-retrieval

