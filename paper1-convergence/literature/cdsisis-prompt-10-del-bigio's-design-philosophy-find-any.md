<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# Prompt 10: Del Bigio's Design Philosophy

Find any writings, interviews, or papers by Giampaolo Del Bigio about CDS/ISIS design philosophy:

- Original design decisions and rationale
- Theoretical influences on CDS/ISIS architecture
- Why specific architectural choices were made
- Predictions about future of information retrieval
Include conference presentations and grey literature

Giampaolo Del Bigio (died c. 1998) was the chief architect and visionary behind UNESCO's CDS/ISIS software. His design philosophy was rooted in a specific mission: to democratize access to professional-grade information retrieval tools for developing nations.

Below is a synthesis of his design philosophy, architectural choices, and vision, drawn from his technical manuals, conference presentations (specifically the 1995 World Congress in Bogotá), and technical papers.

### 1. Original Design Decisions and Rationale

Del Bigio’s core philosophy was that **information software should be "generalized" rather than specialized.** Unlike library systems of the 1970s that were hard-coded for specific formats (like catalogues or personnel files), he designed CDS/ISIS to be a "meta-system"—a tool that allows users to define their own database structures without writing code.

* **The "Generalized" Concept:** The system was built to handle *any* structured non-numerical text. The rationale was economic and practical: developing countries could not afford different software for libraries, archives, and project databases. One engine had to do it all.
* **Variable-Length Fields:** He rejected the fixed-length field structure common in business computing (e.g., COBOL-based systems). He argued that bibliographic data is inherently "ragged"—titles can be 5 characters or 500. Forcing them into fixed blocks was a waste of expensive storage space.
* **Repetitive Fields:** He explicitly designed the architecture to handle "repeating fields" (e.g., multiple authors for a single book) natively, treating them as equally searchable entry points. This was a radical departure from the "flat file" database structures common in early microcomputing.


### 2. Theoretical Influences

Del Bigio’s work was heavily influenced by international standardization efforts and the early architecture of the International Labour Organization (ILO).

* **ILO’s ISIS:** The original theoretical framework came from the **Integrated Set of Information Systems (ISIS)** developed at the ILO in Geneva. Del Bigio, who had worked on the mainframe version, stripped it down to its essential logic to port it to smaller machines (initially DEC PDP-11s, then IBM PCs).
* **ISO 2709 (The "DNA" of the System):** His most non-negotiable theoretical influence was **ISO 2709** (Format for Information Exchange). He believed that *data independence* was more important than the software itself.
    * *Influence:* He designed the internal storage format of CDS/ISIS to be a near-native implementation of ISO 2709.
    * *Rationale:* This ensured that even if the software became obsolete, the data would remain standard-compliant and exportable to any other library system (like MARC).


### 3. Architectural Choices

Specific architectural decisions were made to balance high performance with the hardware constraints of the 1980s and 90s (limited RAM, slow disks).

* **Inverted File Structure (B-Tree):**
    * *Choice:* He implemented a fully inverted file system using B-Tree indexing.
    * *Rationale:* This allowed for "instant" retrieval speed regardless of database size. In an era where searching 100,000 records could take minutes, CDS/ISIS could do it in sub-seconds. This was critical for his vision of "interactive" searching.
* **The Formatting Language:**
    * *Choice:* He created a proprietary, stack-based formatting language (similar to FORTH) for displaying data.
    * *Rationale:* This allowed complex boolean logic to be applied *at the moment of display*. A user could write a format that said, "If there is no author, print the editor; if no editor, print 'Anonymous'." This decoupled data entry from data presentation.
* **Migration to C++ (WinISIS):**
    * *Choice:* For the Windows version (WinISIS), he rewrote the core engine in C++.
    * *Rationale:* Presented at the 1995 Bogotá Congress, this move was to support **Graphical User Interfaces (GUI)** and, crucially, **multi-user record locking**. He foresaw that libraries would move from standalone PCs to Local Area Networks (LANs), and the system needed to prevent data corruption when two librarians edited the same record simultaneously.


### 4. Predictions about the Future of Information Retrieval

Toward the end of his life, particularly around the release of WinISIS (1995–1997), Del Bigio articulated a vision for where IR was heading.

* **The Internet as the Delivery Mechanism:** In his final presentations (circa 1997), he predicted that physical software distribution would vanish. He argued that the future of CDS/ISIS lay in **web-enabled interfaces**, where the "search engine" resided on a server and the user interface was a browser. This led to the development of "GenISIS" (tools to put ISIS on the web).
* **The Obsolescence of Proprietary Formats:** He predicted that "closed" database systems would die out and that **open interchange formats** would be the only way for institutions to survive. This reinforced his lifelong commitment to ISO standards over proprietary lock-in.
* **"Intelligent" Search:** In the 1995 Bogotá proceedings, the vision for "Next Generation CDS/ISIS" included moving beyond simple boolean keywords to more "intelligent" retrieval that could handle full-text and unstructured data, anticipating the shift from cataloguing (metadata) to full-text indexing.


### Key Sources \& Grey Literature to Consult

* **"CDS/ISIS Reference Manual" (Version 1.3):** The foreword and introduction written by Del Bigio contain his clearest statements on system logic.
* **Proceedings of the 1st World Congress on CDS/ISIS (Bogotá, May 1995):** This contains his seminal presentation on the transition to Windows and his vision for the future.
* **"ISIS Documentation: A Position Paper":** An internal UNESCO document where he outlines the philosophy of how the system should be taught and documented.
<span style="display:none">[^1][^10][^11][^12][^13][^14][^15][^16][^17][^18][^19][^2][^20][^21][^22][^23][^24][^25][^26][^27][^28][^29][^3][^30][^31][^32][^33][^34][^35][^36][^37][^38][^39][^4][^40][^41][^42][^43][^44][^5][^6][^7][^8][^9]</span>

<div align="center">⁂</div>

[^1]: https://repository.mdx.ac.uk/download/9f7f119f19b0f64efaaca2a3c64d0335a4fdc1589de4f8474a1303ed2289fd5a/1292800/whandbk.doc

[^2]: https://journals.sagepub.com/doi/pdf/10.1177/026666699509110306?download=true

[^3]: https://unesdoc.unesco.org/ark:/48223/pf0000211280

[^4]: http://utbapxubute.free.bg/WINISIS15rev.pdf

[^5]: https://cdsisis.org

[^6]: https://journal.code4lib.org/articles/4893

[^7]: https://core.ac.uk/download/pdf/33187766.pdf

[^8]: http://anucde.info/syllabus/201ML21.pdf

[^9]: https://arxiv.org/abs/2412.02043

[^10]: https://henryspad7.files.wordpress.com/2015/01/j-isis-reference-manual-21-june-2014.pdf

[^11]: https://journals.sagepub.com/doi/pdf/10.1177/0266666910385667

[^12]: https://ebooks.lpude.in/library_and_info_sciences/MLIS/SEM_2/DLIS418_INFORMATION_TECHNOLOGY-APPLICATIONS.pdf

[^13]: https://lis.academy/information-processing-retrieval/future-information-retrieval-intelligent-search/

[^14]: https://www.academia.edu/2620036/CDS_ISIS_the_second_decade

[^15]: https://liberquarterly.eu/article/view/10557/11263

[^16]: https://www.bibalex.org/Attachments/Publications/Files/1_NewBibliothecaAlexandrina.pdf

[^17]: https://arxiv.org/pdf/2412.02043.pdf

[^18]: https://en.wikipedia.org/wiki/CDS_ISIS

[^19]: https://sidalc.net/search/Record/dig-unesdoc-ark:-48223-pf0000022880

[^20]: https://terpconnect.umd.edu/~oard/pdf/ntcirchap20.pdf

[^21]: http://www.ifs.tuwien.ac.at/dp/dpe/dpe_challenge/reports/vericad.pdf

[^22]: https://www.jodc.go.jp/jodcweb/info/ioc_doc/INF/i0994.pdf

[^23]: https://abecin.org.br/wp-content/uploads/2021/03/MicroIsis.pdf

[^24]: https://lisstudymaterials.wordpress.com/wp-content/uploads/2017/12/dlis408_information_technology-applications.pdf

[^25]: https://sistemas.iibi.unam.mx/biblioteca/pavd/latpdf/LAT001244.pdf

[^26]: https://archaeologicalcomputing.lincei.it/sites/default/files/2021-07/07_AC_V2S09.pdf

[^27]: https://repository.mdx.ac.uk/download/ab93ef4f73fea283c0e624a830f2d13262f6b80e174d9a505b0ca542fe0cd533/97510/isisseconddecade.pdf

[^28]: https://aclanthology.org/volumes/L10-1/

[^29]: https://dblp.org/db/conf/lrec/lrec2010

[^30]: https://ribbitribbit.co/paper/arxiv.2412.02043-Future-of-Information-Retrieval-Research-in-the-Age

[^31]: https://air.uniud.it/retrieve/d8374a56-e0fb-4987-a6d5-f884e8478334/1998-622-PB (1).pdf

[^32]: https://www.nemla.org/content/dam/www/nemla/nis/XXXVI/NIS XXXVI_SL%20edited.pdf

[^33]: http://www.lrec-conf.org/lrec2010/spip.php?page=article_pdf\&id_article=47

[^34]: https://repository.mdx.ac.uk/download/b5c5177eef0aa393e88851bf8e79b8a3f458d5625d8a69b25b307f0790532285/4730472/cds_isis_encyc.pdf

[^35]: https://repository.mdx.ac.uk/download/f9c0d9133ebe5c44427949e3be2e7f7b1e235bb507118af5c7e524eb2c35ee46/698522/whandbk.pdf

[^36]: https://www.strategie-plan.gouv.fr/files/files/Publications/English Articles/Cop 21 un moment de vérité/signatures_0.pdf

[^37]: https://journals.sagepub.com/doi/pdf/10.1177/0266666004240396

[^38]: https://www.imrpress.com/journal/KO/19/1/10.5771/0943-7444-1992-1-19/pdf

[^39]: https://openknowledge.worldbank.org/bitstreams/939cae27-f69f-5c3a-8708-66217e751037/download

[^40]: https://journals.sagepub.com/doi/pdf/10.1177/0266666974238546?download=true

[^41]: https://ideas.repec.org/e/c/pwi200.html

[^42]: https://www.nu.to.infn.it/Other_New_Physics/

[^43]: http://www.motorsportmemorial.org/update.php?db=ct\&y=2006\&m=11

[^44]: https://www.science.gov/topicpages/n/newly+detected+lesions

