<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# PROMPT 6: Industry Convergence on Hierarchical Structures (2024–2025)

Main takeaway: Across Elastic, MongoDB, DataStax, Vespa, and Typesense, production vector search is converging on **hierarchical, graph- and tree-based indexing (HNSW, hierarchical k‑means/IVF, DiskANN‑style hierarchies)** plus hybrid lexical–vector pipelines. These are explicitly framed as necessary to break scaling barriers in cost/latency and to better exploit hierarchical structure in data and indices.

Below, “hierarchical” is interpreted broadly: HNSW’s multilevel graph, DiskANN/Vamana‑style graph hierarchies, recursive clustering/IVF, and explicit parent–child document trees.

***

## Elastic / Elasticsearch \& Lucene

### Key Finding 1 – Hierarchical HNSW as Core ANN Index

- **Direct quote / claim**

“Lucene's architecture organizes data into segments, immutable units that undergo periodic merging… With vector search, Lucene extends its capabilities to handle multi-dimensional points, employing the **hierarchical navigable small world (HNSW)** algorithm to index vectors.”[^1]

“Furthermore, this optimization is particularly beneficial for **Hierarchical Navigable Small World (HNSW)** searches, as **each graph is independent of the others and can be searched in parallel**, maximizing efficiency and speeding up retrieval times even further.”[^1]
- **Source with date**

Elastic Search Labs blog, *“Making Elasticsearch and Lucene the best vector database”*, 8 Oct 2024.[^1]
- **Why this matters for the paper**

Elastic explicitly positions **HNSW’s hierarchical graph structure** as the core vector index in Lucene/Elasticsearch, leveraging **per‑segment HNSW graphs** searched in parallel. This is a clear industry signal that large‑scale production search is being re‑architected around **hierarchical graph indices** rather than flat structures. It also underscores **hierarchical decomposition at the storage layer (segments + per‑segment HNSW graphs)** as a design principle.

***

### Key Finding 2 – Hierarchical k‑means / IVF for Vector Indices

- **Direct quote / claim**

“For IVF indices, vectors are clustered and a map is created which lists the vectors associated with each cluster… Retrieval proceeds by embedding a query, then looking up the nearest cluster centroids and finally comparing the vectors in each cluster to the query vector. **This bears a striking resemblance to traditional lexical retrieval by inverted index (hence the name).** Compared to graph based methods such as HNSW it has some distinct pros and cons.”[^2]

“In order to tackle quadratic scaling we somehow need to guarantee that we only ever compare each vector to $a$ clusters even if we eventually need $k$ clusters in total. **There is a very simple strategy which achieves this: cluster the dataset recursively.** … For each cluster that is larger than the target size, simply cluster its assigned vectors using $k$ centroids and repeat.”[^2]

“We explored **hierarchical k‑means** to break this scaling and show the resulting scheme requires only $O(nk \log k)$ comparisons. **This results in very substantial speedups: we got an average of 18×** for the datasets in our evaluation set.… With these changes we achieve an **average speedup of 8×** as well as a small improvement in index quality over k‑means.”[^2]
- **Source with date**

Elastic Search Labs, *“K‑means for building vector indices”*, 10 Sept 2025 (discussing work that “will feed into the IVF index implementation we’re bringing to Elasticsearch”).[^2]
- **Why this matters for the paper**

This is a strong, explicit **industry acknowledgement that hierarchical clustering is required to overcome scaling limits** of flat k‑means/IVF. The blog directly motivates **recursive (hierarchical) clustering** as a way to reduce complexity from quadratic to near‑linear‑log and reports **large empirical speedups (18× raw, 8× after quality fixes)**. It also explicitly draws an analogy between IVF and **symbolic inverted indices**, supporting a “neurosymbolic” interpretation of modern vector indexing.

***

### Numbers / Statistics (Elastic \& Lucene)

- “Elasticsearch 8.14.0 marks the first release to leverage native code for vector search… leading to a **significant reduction in overall indexing time**.” (qualitative but tied to concrete release.)[^3]
- Hierarchical k‑means for IVF:
    - “average of **18 times** [speedup] for the datasets in our evaluation set.”[^2]
    - After fix‑up step: “**average speedup of 8 times** as well as a small improvement in index quality over k‑means.”[^2]
    - Target cluster size for disk‑friendliness: “we expect one will need to use a value in the **low hundreds**.”[^2]

Elastic’s HNSW blogs also emphasize **layered traversal (“multiple layers… each layer adding more datapoints”)** in external commentary: “You go through multiple layers, each layer adding more datapoints to get you as close as possible to where you want to go, rather than comparing all of the documents.”[^4]

***

## MongoDB Atlas

### Key Finding 1 – HNSW as Hierarchical Graph Index

- **Direct quote / claim**

“At its core, **Atlas Vector Search uses the Hierarchical Navigable Small World (HNSW) algorithm for indexing and searching vector data. This creates a multi level graph of the vector space so you can do Approximate Nearest Neighbor (ANN) searches.** It’s a balance of speed and accuracy for large scale vector search.”[^5]

“The MongoDB database uses the vector index **HNSW, which is a graph-based indexing algorithm that organizes vectors in a hierarchical structure** …”[^6]
- **Source with date**
    - Zilliz blog comparison, *“MongoDB vs MyScale on Vector Search Capabilities”*, 31 Oct 2025 (describing MongoDB Atlas Vector Search).[^5]
    - MongoDB blog, *“Scaling Vector Search with MongoDB Atlas Quantization \& Voyage …”* (undated snippet but clearly about current Atlas Vector Search; emphasis on hierarchical structure).[^6]
- **Why this matters for the paper**

MongoDB explicitly describes its vector index as a **hierarchical graph (HNSW) over the vector space**, with industry‑standard language about multi‑level structure and ANN. This is a mainstream document‑database vendor stating that **hierarchical organization is central to vector search**, not just an implementation detail.

***

### Key Finding 2 – Hybrid / Rank Fusion as Structured Combination

- **Direct quote / claim**

“We’re excited to introduce a **native hybrid search experience** that seamlessly combines the power of MongoDB Atlas’ native text search and vector search capabilities. Now in public preview, this capability **leverages reciprocal rank fusion (RRF) to rank result sets from both text and vector searches**, significantly improving relevance and user experiences.”[^7]

“You can now **streamline hybrid search implementations with a single \$rankFusion aggregation stage**. This allows for effortlessly combining full-text and vector search result sets into a unified ranked list, quickly surfacing the most relevant information.”[^7]
- **Source with date**

MongoDB blog, *“Boost Search Relevance with MongoDB Atlas' Native Hybrid Search”*, 25 June 2025, updated 17 Sept 2025.[^7]
- **Why this matters for the paper**

While not hierarchical in the spatial sense, this is a **symbolic aggregation layer** that defines a structured operator (\$rankFusion / \$scoreFusion) to combine multiple evidence sources (text, vector, geo) into a single ranking. This shows a major vendor converging on **symbolic, operator‑based composition of neural/vector signals**, which is an important component of “neurosymbolic” retrieval architectures.

***

### Numbers / Statistics (MongoDB)

- Dimensions: “You can query any kind of data that can be embedded **up to 4096 dimensions**.”[^5]
- Performance/scale:
    - Atlas provides **Search Nodes** as dedicated infrastructure “for Atlas Search and Vector Search workloads… independent scaling of search needs so you get **better performance at scale**.”[^5]
- Hybrid search impact example:
    - “This has **improved the context retrieval accuracy for our Eddy AI chatbot by 30%**.” (customer quote from Kovai.co about rank‑fusion based hybrid search.)[^7]

***

## DataStax / Apache Cassandra (JVector \& SAI)

### Key Finding 1 – Explicit Hierarchical Graph Index (JVector)

- **Direct quote / claim**

“Graph-based indexes tend to be simpler to implement and faster, but more importantly they can be constructed and updated incrementally.… **That is why all the major commercial vector indexes use graph approaches.**”[^8]

“**JVector is a graph index that merges the DiskANN and HNSW family trees. JVector borrows the hierarchical structure from HNSW, and uses Vamana (the algorithm behind DiskANN) within each layer.**”[^8]

“Setting the `addHierarchy` parameter to true, **build a multi-layer index. This approach has proven more robust in highly challenging scenarios.**”[^8]
- **Source with date**

DataStax GitHub project, *JVector: the most advanced embedded vector search engine*. Initial commit Aug 2023; hierarchy described in current README/docs (used by 2024+ DataStax Storage-Attached Indexing).[^8]
- **Why this matters for the paper**

JVector is used under the hood in **DataStax’s Storage-Attached Indexing (SAI) vector search**. The documentation is an unusually clear, explicit statement that:
    - Major vendors are **standardizing on graph‑based ANN**.
    - JVector explicitly **inherits HNSW’s hierarchical structure** and integrates DiskANN/Vamana **within each layer**, i.e., a layered, hybrid symbolic structure.
    - A boolean parameter literally named `addHierarchy` exposes the hierarchy as a first‑class concept.

***

### Key Finding 2 – Cassandra/SAI: “Hierarchy of Navigable Graph Indexes”

- **Direct quote / claim**

“SAI uses the **JVector Approximate Nearest Neighbor (ANN) search algorithm** for similarity search.… Taking inspiration from DiskANN, **JVector balances speed and accuracy by creating a hierarchy of navigable graph indexes.** All data points, or nodes, on the graph, can find a path to any other node.”[^9]
- **Source with date**

DataStax documentation, *“Vector search quickstart | CQL for DataStax Hyper‑Converged …”*. The vector‑search sections are current and describe the JVector‑based behavior.[^9]
- **Why this matters for the paper**

This is a major distributed database vendor describing its production vector search stack explicitly as a **“hierarchy of navigable graph indexes”**. That phrasing is particularly valuable as a concise description linking **hierarchical structure** and **graph‑based ANN**. It also mirrors HNSW language but in a vendor’s own docs.

***

### Numbers / Statistics (DataStax)

- No explicit percentage numbers in the docs snippet, but several **design properties**:
    - SAI is “ideal for **large datasets**… that must support vector search.”[^9]
    - Vector search works “optimally on tables with **no overwrites or deletions** of the vector column… For a vector column with changes, expect **slower search results**.”[^9]
- JVector discusses **memory vs. disk split**:
    - “The upper layers of the hierarchy are represented by an **in-memory adjacency list per node.**… The bottom layer of the graph is represented by an **on-disk adjacency list per node.**”[^8]
    - It also employs **product quantization** for compressed representations during construction.[^8]

These details are important for your argument about **symbolic hierarchical structure interacting with physical layout** (memory vs disk tiers, layered graphs).

***

## Vespa

### Key Finding 1 – HNSW Hierarchy \& Multi‑Vector HNSW

- **Direct quote / claim**

“Since exact nearest neighbor search over millions and millions of vectors is prohibitively expensive, **Vespa employs the HNSW (Hierarchical Navigable Small World) algorithm for approximate nearest-neighbor (ANN) search**, trading a bit of accuracy for a vast reduction in response time.”[^10]

“In **HNSW, a hierarchy of graphs is used as an index**, and while there is a comparably high initial indexing cost for building the index, **the search throughput is much higher** than with other algorithms.”[^10]

“Since then, there have been advancements in Vespa like **multi-vector HNSW indexing**, but also some recent enhancements to the HNSW search itself.”[^10]
- **Source with date**

Vespa blog, *“Additions to HNSW in Vespa: ACORN‑1 and Adaptive Beam Search”*, 3 Sept 2025.[^10]
- **Why this matters for the paper**

Vespa is a flagship **large‑scale, industry‑grade search engine**. Its description of HNSW as “a hierarchy of graphs used as an index” is one of the clearest articulations of hierarchical structure at the core of ANN in production. The mention of **multi‑vector HNSW** shows Vespa extending this hierarchy to richer structured representations (e.g., multiple embeddings per document), aligning closely with hybrid symbolic‑neural retrieval ideas.

***

### Key Finding 2 – Parent–Child Hierarchies for Document Modeling

- **Direct quote / claim**

“Parent-child relationships let you **model hierarchical relations in your data**. This blog post talks about why and how we added this feature to Vespa, and how you can use it in your own applications.”[^11]

“Parent-child is limited to **DAG relations** and therefore can’t be used to model an arbitrary graph.”[^11]

“As mentioned in the Global documents section, **all parent documents must be present on all nodes.** This is one of the biggest caveats with the parent-child feature: **all nodes must have sufficient capacity for all parents.** A core assumption that we have made for the use of this feature is the **number of parent documents is much lower than the number of child documents. At least an order of magnitude fewer documents per parent level is a reasonable heuristic.**”[^11]

“ElasticSearch reports query slowdowns of **500–1000% when using parent-child**, while expected overhead when using parent-child attribute fields in Vespa is on the order of **10–20%**.”[^11]
- **Source with date**

Vespa blog, *“Parent-child in Vespa”* (evergreen documentation‑style article; parent–child feature is a relatively recent addition used in large‑scale ad serving).[^11]
- **Why this matters for the paper**

Although independent from HNSW, this shows Vespa **explicitly engineering hierarchical (DAG) document structures** into the search engine, with detailed reasoning about cardinality ratios (parents vs children), distribution, and performance. It also offers a direct **comparison with Elasticsearch’s parent‑child model**, including large overheads on the Elastic side, which you can use to argue that **well‑designed hierarchies can be both expressive and efficient**.

***

### Numbers / Statistics (Vespa)

- Parent–child heuristics:
    - “At least an **order of magnitude fewer documents per parent level** is a reasonable heuristic.”[^11]
- Performance comparison:
    - “ElasticSearch reports query slowdowns of **500–1000%** when using parent-child… while expected overhead when using parent-child attribute fields in Vespa is on the order of **10–20%**.”[^11]
- HNSW hierarchy:
    - Vespa uses the **original HNSW index with one entry point** and applies ACORN‑1 only on the **lowest layer**.[^10]
    - Lucene’s HNSW is explicitly mentioned as using similar one‑entry‑point HNSW with ACORN‑1‑inspired heuristics at the lowest layer, for comparison.[^10]

***

## Typesense

### Key Finding 1 – HNSW Vector Index with Configurable Hierarchical Parameters

- **Direct quote / claim**

“By default, **Typesense uses the built-in HNSW index to do approximate nearest neighbor vector searches.** This scales well for large datasets.”[^12][^13]

“You can set `ef_construction` (default: `200`) and `M` (default: `16`) for vector and embedding fields while creating the collection.”[^12]

Configuration example:

```json
"fields": [
  {
    "name": "vec",
    "type": "float[]",
    "num_dim": 768,
    "hnsw_params": {
      "ef_construction": 100,
      "M": 8
    }
  }
]
```

- **Source with date**

Typesense docs, *“Vector Search – Typesense”*, v0.29 / 29.0 docs page (API docs current in 2023–2024).[^13][^12]
- **Why this matters for the paper**

Typesense is a popular open‑source search engine. Its vector search docs clearly describe **HNSW as the default index**, and expose standard HNSW parameters that control the **graph’s hierarchical layer density and connectivity**. While they don’t narratively emphasize the word “hierarchical,” the use of HNSW and its parameters is another data point that **industry‑standard vector search = hierarchical graph indexing**.

***

### Key Finding 2 – Hybrid and Fallback Strategies around the HNSW Index

- **Direct quote / claim**

“By default, Typesense uses the built-in HNSW index to do approximate nearest neighbor vector searches. This **scales well for large datasets. However, if you wish to bypass the HNSW index and do a flat / brute-force ranking of vectors, you can do that via the `flat_search_cutoff` parameter.**”[^13][^12]

“Typesense will do a keyword search using the `q` parameter, and a nearest neighbor search using the `vector_query` field and **combine the results into a ranked set of results using rank fusion** as described earlier.”[^12]
- **Source with date**

Typesense Vector Search docs, v0.29 / 0.24.1.[^13][^12]
- **Why this matters for the paper**

Typesense’s design shows:
    - HNSW as the **default hierarchical ANN** mechanism.
    - An explicit **fallback to flat search** for small candidate sets (a simple “symbolic” conditional on set size via `flat_search_cutoff`).
    - A **rank‑fusion‑style hybrid** of keyword and vector search.

Combined, this is a compact example of **hierarchical and symbolic control logic around a neural index**.

***

### Numbers / Statistics (Typesense)

- Default HNSW parameters:
    - `ef_construction`: **200** (default)[^12]
    - `M`: **16** (default)[^12]
- Example override:
    - `ef_construction: 100`, `M: 8` for a `768`‑dimensional vector field.[^12]
- Fallback threshold:
    - `flat_search_cutoff=20` example: “bypass the HNSW index when the number of results found is **less than 20**.”[^13][^12]

These are useful concrete parameter values to anchor your discussion of **practical hierarchical index tuning**.

***

## Elastic vs Vespa Segment vs Node Hierarchies

A useful cross‑vendor contrast appears in Vespa’s terminology mapping:

- **Direct quote / claim**

“Most importantly, when it comes to approximate nearest neighbor (ANN), **Vespa has one HNSW graph per node, while the Lucene implementation has one HNSW graph per segment. This makes ANN typically much faster in Vespa, because it’s like searching in an index force-merged to 1 segment.**”[^14]
- **Source with date**

Vespa blog, *“Vespa Terminology for Elasticsearch, OpenSearch or Solr …”*, 15 Aug 2024.[^14]
- **Why this matters for the paper**

This is an explicit **hierarchy‑of‑graphs design comparison**:
    - Lucene: many per‑segment HNSW graphs, later merged.
    - Vespa: fewer, per‑node HNSW graphs, closer to a single global hierarchical index.

It shows vendors actively reasoning about **at which level in the storage hierarchy** the HNSW graph should live, and trading off merge complexity vs search latency.

***

## Additional Supporting Material

### Elastic’s Large‑Scale Vector Search Positioning

- **Direct quote / claim**

“Elasticsearch 8.14.0 marks the first release to leverage **native code for vector search**. A native Elasticsearch codec is employed during merges to accelerate similarities between int8 vectors, **leading to a significant reduction in overall indexing time**.”[^3]
- **Source**

Elastic Search Labs, *“Designing for large scale vector search with Elasticsearch”*, 8 Oct 2024.[^3]
- **Relevance**

While not explicitly about hierarchy, this shows Elastic treating vector search as a **first‑class large‑scale system problem** and optimizing index merges, which become more complex when hierarchical graph and IVF indices are involved.

***

## Citations (with URLs)

Elastic / Lucene
Elastic, “Designing for large scale vector search with Elasticsearch”, 8 Oct 2024.[^3]
URL: https://www.elastic.co/search-labs/blog/elasticsearch-vector-large-scale-part1

Elastic, “Making Elasticsearch and Lucene the best vector database”, 8 Oct 2024.[^1]
URL: https://www.elastic.co/search-labs/blog/elasticsearch-lucene-vector-database-gains

TechStrong.ai, “Elastic Improves Search Experience With Additions to Its Vector Database”, 30 Sept 2024 (quotes Elastic’s Philipp Krenn on HNSW).[^4]
URL: https://techstrong.ai/sponsored-content/elastic-improves-search-experience-with-additions-to-its-vector-database/

Elastic, “K-means for building vector indices”, 10 Sept 2025.[^2]
URL: https://www.elastic.co/search-labs/blog/k-means-for-vector-indices

Elastic, “How to set up vector search in Elasticsearch”, 2025.[^15]
URL: https://www.elastic.co/search-labs/de/blog/vector-search-set-up-elasticsearch

MongoDB
Zilliz, “MongoDB vs MyScale on Vector Search Capabilities”, 31 Oct 2025.[^5]
URL: https://zilliz.com/blog/mongodb-vs-myscale-a-comprehensive-vector-database-comparison

MongoDB University, “Using Vector Search for Semantic Search”, 21 Apr 2024.[^16]
URL: https://learn.mongodb.com/courses/using-vector-search-for-semantic-search

MongoDB blog snippet, “Scaling Vector Search with MongoDB Atlas Quantization \& Voyage …”.[^6]
URL: https://www.mongodb.com/company/blog/technical/scaling-vector-search-mongodb-atlas-quantization-voyage-ai-embeddings

MongoDB, “Boost Search Relevance with MongoDB Atlas' Native Hybrid Search”, 25 June 2025, updated 17 Sept 2025.[^7]
URL: https://www.mongodb.com/company/blog/product-release-announcements/boost-search-relevance-mongodb-atlas-native-hybrid-search

DataStax / JVector
DataStax, GitHub README for “JVector: the most advanced embedded vector search engine”, 2023+, used in 2024–2025 products.[^8]
URL: https://github.com/datastax/jvector

[^9] DataStax docs, “Vector search quickstart | CQL for DataStax Hyper-Converged …” (SAI vector search).
URL: https://docs.datastax.com/en/cql/hcd/get-started/vector-search-quickstart.html

Vespa
Vespa, “Vespa Terminology for Elasticsearch, OpenSearch or Solr …”, 15 Aug 2024.[^14]
URL: https://blog.vespa.ai/dictionary-vespa-to-elasticsearch-opensearch-solr/

Vespa, “Parent-child in Vespa”.[^11]
URL: https://blog.vespa.ai/parent-child-in-vespa/

Vespa, “Additions to HNSW in Vespa: ACORN-1 and Adaptive Beam Search”, 3 Sept 2025.[^10]
URL: https://blog.vespa.ai/additions-to-hnsw/

Typesense
Typesense Docs v29.0, “Vector Search – Typesense” (includes HNSW, `flat_search_cutoff`, `ef`, `M`).[^12]
URL: https://typesense.org/docs/29.0/api/vector-search.html

Typesense Docs v0.24.1, “Vector Search – Typesense”.[^13]
URL: https://typesense.org/docs/0.24.1/api/vector-search.html

Cross‑cutting / context
Zilliz, “Elasticsearch vs Vearch on Vector Search Capabilities” (explains Elasticsearch’s HNSW‑based index).[^17]
URL: https://zilliz.com/blog/elasticsearch-vs-vearch-a-comprehensive-vector-database-comparison

Pureinsights, “Comparing Vector Search Solutions 2024”, 29 Apr 2025.[^18]
URL: https://pureinsights.com/blog/2024/comparing-vector-search-solutions-2024/

Appwrite, “The top 6 Vector Databases to use for AI applications in 2025”, 17 Nov 2025.[^19]
URL: https://appwrite.io/blog/post/top-6-vector-databases-2025
<span style="display:none">[^20]</span>

<div align="center">⁂</div>

[^1]: https://www.elastic.co/search-labs/blog/elasticsearch-lucene-vector-database-gains

[^2]: https://www.elastic.co/search-labs/de/blog/k-means-for-vector-indices

[^3]: https://www.elastic.co/search-labs/blog/elasticsearch-vector-large-scale-part1

[^4]: https://techstrong.ai/sponsored-content/elastic-improves-search-experience-with-additions-to-its-vector-database/

[^5]: https://zilliz.com/blog/mongodb-vs-myscale-a-comprehensive-vector-database-comparison

[^6]: https://www.mongodb.com/company/blog/technical/scaling-vector-search-mongodb-atlas-quantization-voyage-ai-embeddings

[^7]: https://www.mongodb.com/company/blog/product-release-announcements/boost-search-relevance-mongodb-atlas-native-hybrid-search

[^8]: https://github.com/datastax/jvector

[^9]: https://docs.datastax.com/en/cql/hcd/get-started/vector-search-quickstart.html

[^10]: https://blog.vespa.ai/additions-to-hnsw/

[^11]: https://blog.vespa.ai/parent-child-in-vespa/

[^12]: https://typesense.org/docs/29.0/api/vector-search.html

[^13]: https://typesense.org/docs/0.24.1/api/vector-search.html

[^14]: https://blog.vespa.ai/dictionary-vespa-to-elasticsearch-opensearch-solr/

[^15]: https://www.elastic.co/search-labs/de/blog/vector-search-set-up-elasticsearch

[^16]: https://learn.mongodb.com/courses/using-vector-search-for-semantic-search

[^17]: https://zilliz.com/blog/elasticsearch-vs-vearch-a-comprehensive-vector-database-comparison

[^18]: https://pureinsights.com/blog/2024/comparing-vector-search-solutions-2024/

[^19]: https://appwrite.io/blog/post/top-6-vector-databases-2025

[^20]: https://stackoverflow.com/questions/49643896/creating-dynamic-parent-child-relationship-in-vespa

