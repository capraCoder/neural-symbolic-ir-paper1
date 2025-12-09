<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

### IFLA and Library Science Theory in CDS/ISIS

The following report documents the theoretical principles of library science implemented in CDS/ISIS (Computerized Documentation System / Integrated Set of Information Systems), based on IFLA publications and library science literature from 1980–2000.

These principles were largely architected by **Giampaolo Del Bigio** at UNESCO and were designed to support IFLA's **Universal Bibliographic Control (UBC)** programme by providing a standard-compliant tool for developing nations.

#### 1. Bibliographic Control Theory

The theoretical foundation of bibliographic control in CDS/ISIS is rooted in the **Universal Bibliographic Control (UBC)** paradigm promoted by IFLA. The system was designed to ensure that bibliographic data created in any country could be exchanged internationally.

* **ISBD and Variable Fields:** CDS/ISIS implemented the theoretical requirement for **ISBD (International Standard Bibliographic Description)** by allowing variable-length fields. Unlike fixed-length relational databases of the era, CDS/ISIS used a directory structure (based on ISO 2709) that allowed fields to expand as needed, preserving the integrity of complex bibliographic data (e.g., long titles, multiple authors) without truncation.[^1][^2]
* **Exchange Formats:** The system was theoretically grounded in the concept of "exchange capability." It was built natively around **ISO 2709**, the international standard for bibliographic information interchange. This allowed it to serve as a bridge between local cataloging and international systems like **UNIMARC** and **CCF** (Common Communication Format).[^2][^3]


#### 2. Authority Control Theoretical Foundations

In CDS/ISIS, authority control theory was implemented through **Inverted File Indexing** and **Dictionary Validation**, moving away from the simple "heading lists" used in card catalogs to dynamic, machine-readable authority files.

* **Inverted File Structure:** The theoretical innovation was the separation of the "Master File" (bibliographic data) from the "Inverted File" (access points). This allowed for rapid retrieval and effectively functioned as a dynamic authority list. Terms extracted from records were stored in a B-tree structure, allowing indexers to view existing terms (the "dictionary") before assigning them, ensuring consistency—a core tenet of authority control.[^4][^5]
* **Thesaurus Integration:** CDS/ISIS supported the theoretical structure of thesauri (BT, NT, RT relationships) via the `ANY` term function and specific Pascal applications. This allowed for **syndetic structure control**, ensuring that users searching for a term could also retrieve records indexed under related or narrower terms, a key principle of subject authority control.[^2]


#### 3. Field Independence Axiom

The "Field Independence" principle (often discussed in technical documentation as **Data Independence** or the **Definition Table** concept) is the axiom that **logical data definition must be independent of physical storage**.

* **Field Definition Table (FDT):** CDS/ISIS operationalized this by separating the logical definition of fields (Tag, Name, Type, Pattern) from the physical records. This allowed libraries to define their own structures (e.g., MARC, local formats) without modifying the software code.
* **ISO 2709 Directory Principle:** The "axiom" underlying this is the use of a **Directory** (pointers to tags, lengths, and starting positions) at the start of every record. This makes every field physically independent; a field's location is not fixed but relative. This theoretical approach solved the problem of "sparse data" in library catalogs, where many fields (like "Edition" or "Series") are empty for most records.[^6][^7]


#### 4. Hierarchical Decomposition Principles

CDS/ISIS implemented hierarchical decomposition theories to handle complex bibliographic relationships (e.g., Series -> Monograph -> Analytic) that linear card catalogs could not easily represent.

* **Record Segments (CCF Implementation):** The most significant theoretical implementation was the support for the **Common Communication Format (CCF)** structure. CCF, developed by UNESCO/IFLA, proposed breaking a record into "segments" to handle hierarchy within a single record. CDS/ISIS adopted this via **Repeating Groups**, allowing a single record to contain a hierarchy of bibliographic levels (e.g., a journal title [Level 1] and the article details [Level 2]).[^3][^8]
* **Linking Functions:** The system implemented **virtual hierarchy** through the link (`L`) and reference (`REF`) functions. This allowed "analytics" (chapters/articles) to be stored as independent records but logically linked to their parent "monograph" or "serial" record during retrieval or printing. This validated the theoretical principle that bibliographic entities should be described once and linked, rather than duplicated.[^7]


### Key References (1980–2000)

* **IFLA Journal \& ICBC:** Articles discussing the "Universal Bibliographic Control" programme and the role of software like CDS/ISIS in standardizing cataloging in developing countries.[^9][^1]
* **UNESCO/PGI Documents:** The *CCF: The Common Communication Format* (edited by Peter Simmons and Alan Hopkinson) serves as the primary theoretical text for the field independence and hierarchical segment structures implemented in CDS/ISIS.[^10][^8]
* **Program: Electronic Library and Information Systems:** This journal frequently published technical articles by Alan Hopkinson and others detailing the specific implementation of these library science theories in CDS/ISIS.[^11][^10]
<span style="display:none">[^12][^13][^14][^15][^16][^17][^18][^19][^20][^21][^22][^23][^24][^25][^26][^27][^28][^29][^30][^31][^32][^33][^34][^35][^36][^37][^38][^39][^40][^41][^42][^43][^44][^45][^46][^47][^48][^49][^50]</span>

<div align="center">⁂</div>

[^1]: https://www.ifla.org/files/assets/hq/publications/icbc-toc-v13-v31.pdf

[^2]: https://liberquarterly.eu/article/download/10557/12378?inline=1

[^3]: https://www.academia.edu/2620036/CDS_ISIS_the_second_decade

[^4]: http://eprints.rclis.org/32367/1/IS 5(1) -2 Hussain.pdf

[^5]: https://henryspad7.files.wordpress.com/2015/01/j-isis-reference-manual-21-june-2014.pdf

[^6]: https://cdsisis.org

[^7]: https://repository.mdx.ac.uk/download/9f7f119f19b0f64efaaca2a3c64d0335a4fdc1589de4f8474a1303ed2289fd5a/1292800/whandbk.doc

[^8]: https://repository.mdx.ac.uk/download/57ea80cb0e676cc885bd50340cd4c56f48637ecc7e7520b906cc0209b1af9505/142681/FIMP.RTF

[^9]: https://repository.ifla.org/bitstreams/355d4ac3-23f3-44eb-bdb2-d0c4cd77bd20/download

[^10]: https://www.academia.edu/2620034/CDS_ISIS_information

[^11]: https://repository.mdx.ac.uk/download/f9c0d9133ebe5c44427949e3be2e7f7b1e235bb507118af5c7e524eb2c35ee46/698522/whandbk.pdf

[^12]: https://www.ifla.org/publications/ifla-series-on-bibliographic-control/

[^13]: https://www.ifla.org/ifla-series-on-bibliographic-control/

[^14]: https://www.ifla.org/files/assets/hq/publications/ifla-journal/ifla-journal-1-2005.pdf

[^15]: https://mmv.ac.in/pdf/MRP UGC Final.pdf

[^16]: https://www.ala.org/lhrt/popularresources/libhistorybib/lhrtbibearly2000s

[^17]: https://aiirjournal.com/uploads/Articles/2018/02/2855_19.dr.vikram%20giri.pdf

[^18]: https://core.ac.uk/download/pdf/162014949.pdf

[^19]: https://www.gpntb.ru/win/inter-events/crimea2000/program/eng/index.html

[^20]: https://www.zfs.uni-hamburg.de/dgfs2020/dgfs2020/downloads/dgfs2020-booklet-web-v1.pdf

[^21]: http://eprints.rclis.org/22581/1/Sabitri final thesis.pdf

[^22]: https://fr.scribd.com/presentation/36695931/Isis-Tutorial2

[^23]: https://grokipedia.com/page/CDS_ISIS

[^24]: https://www.academia.edu/74621045/Information_Technology_in_Central_American_Libraries

[^25]: https://journal.code4lib.org/articles/4893

[^26]: https://ebooks.lpude.in/library_and_info_sciences/MLIS/SEM_2/DLIS418_INFORMATION_TECHNOLOGY-APPLICATIONS.pdf

[^27]: http://anucde.info/syllabus/201ML21.pdf

[^28]: https://www.igi-global.com/viewtitle.aspx?TitleId=24468\&isxn=9781605660325

[^29]: https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nbsspecialpublication724.pdf

[^30]: https://www.semanticscholar.org/paper/The-DANIS-database-system:-integrating-and-factual-Smet-Nieuwenhuysen/8b4e75068378ec4574a96bc317471584de6db0c6

[^31]: https://repository.mdx.ac.uk/download/b5c5177eef0aa393e88851bf8e79b8a3f458d5625d8a69b25b307f0790532285/4730472/cds_isis_encyc.pdf

[^32]: https://core.ac.uk/download/577322229.pdf

[^33]: https://www.cs.huji.ac.il/~dolev/pubs/JWSR.pdf

[^34]: https://unesdoc.unesco.org/ark:/48223/pf0000263460

[^35]: https://onlinelibrary.wiley.com/doi/10.1002/sce.3730670308

[^36]: https://mediatum.ub.tum.de/doc/1274439/186405.pdf

[^37]: https://unesdoc.unesco.org/ark:/48223/pf0000127825

[^38]: http://eprints.nottingham.ac.uk/10577/1/ejb-thesis-for-ethesis-archive.pdf

[^39]: https://www.irbnet.de/daten/iconda/CIB14762.pdf

[^40]: https://www.scribd.com/doc/311361979/English-Russian-Dictionary-of-Computer-Technology-pdf

[^41]: https://www.academia.edu/6075578/СОВРЕМЕННЫЙ_%D0%90%D0%9D%D0%93%D0%9B%D0%9E%D0%9E%D0%A0%D0%A3%D0%A1%D0%A1%D0%9A%D0%98%D0%99_%D0%A1%D0%9B%D0%9E%D0%92%D0%90%D0%A0%D0%AC_%D0%9A%D0%9E%D0%9C%D0%9F%D0%AC%D0%AE%D0%A2%D0%95%D0%A0%D0%9D%D0%AB%D0%A5_%D0%A2%D0%95%D0%A5%D0%9D%D0%9E%D0%9B%D0%9E%D0%93%D0%98%D0%99

[^42]: https://english8poly.narod.ru/anglo-russkij_slovar_kompjuternykh_tekhnologij.pdf

[^43]: https://id.scribd.com/document/416427322/p6-report

[^44]: https://d-nb.info/1240806957/34

[^45]: https://discovery.ucl.ac.uk/id/eprint/1334914/1/AidaSlavicOverfield_thesis_UCL2005.pdf

[^46]: https://archive.isis.vanderbilt.edu/sites/default/files/Nordstrom_SG_5_0_2003_A_Runtime_.pdf

[^47]: https://www.ica.org/app/uploads/2024/01/CBPS_2000_Guidelines_ISADG_Second-edition_EN.pdf

[^48]: https://digitalcommons.unl.edu/cgi/viewcontent.cgi?article=5700\&context=libphilprac

[^49]: https://egyankosh.ac.in/bitstream/123456789/35928/5/Unit-3.pdf

[^50]: https://core.ac.uk/download/pdf/144515092.pdf

