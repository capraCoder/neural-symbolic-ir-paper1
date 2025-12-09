<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# UNESCO CDS/ISIS Technical Documentation (1980–1995)

**Main takeaway:**
Core CDS/ISIS technical documentation for 1980–1995 consists of the Mini‑micro CDS/ISIS Reference Manual and its later “Mini‑micro CDS/ISIS: reference manual (version 2.3)” revisions, associated training/handbook literature (Buxton, Hopkinson), and scattered reports and newsletters. Giampaolo Del Bigio’s role is documented mostly through forewords, programmatic overviews, and workshop reports rather than a single “design philosophy” monograph. Andrew Buxton’s main formal contribution in this period is as co‑author of *The CDS/ISIS Handbook* (1994), an explanatory companion to the UNESCO reference manuals.

Below is what can be identified and located with report numbers or stable archival locations for 1980–1995.

***

## 1. Technical Reference Manuals (core system documentation)

### 1.1 Mini‑micro CDS/ISIS: Reference Manual (initial DOS release)

Evidence from bibliographic and review literature shows that the primary technical reference for the DOS “Mini‑micro version” was issued by UNESCO in 1985, under titles such as:

- **“CDS/ISIS (mini‑micro version) – reference manual”**
– Place: Paris, UNESCO
– Year: 1985
– Extent: c. 193–196 pages (“196 p with supplements and additions”)[^1][^2][^3][^4]

Multiple independent bibliographic sources cite it in this form, but do not expose the full PGI/PGI‑xx or UNESDOC report number in the snippets available online. In library catalogues and training documents it is often listed as:[^2][^3][^4][^1]

> CDS/ISIS mini‑micro version: reference manual. UNESCO, 1985. 193–224 p.[^5][^4][^2]

This appears as the canonical technical reference for Micro CDS/ISIS throughout the late 1980s and early 1990s, and is the “official Reference manual” that later handbooks (e.g. Buxton/Hopkinson) treat as the primary specification.[^6]

Archival location (practical):

- UNESDOC entry is not clearly surfaced by short search snippets, but the manual can be reliably located through:
    - UNESDOC search by title “CDS/ISIS mini‑micro version: reference manual” or “Mini‑micro CDS/ISIS: reference manual” (see next item for a clearly indexed version).
    - National library and university catalogues referencing UNESCO as publisher with year 1985.[^4][^1][^5][^2]

Given how UNESDOC numbers are assigned, the original reference manual likely carries a PGI series number (e.g., PGI‑85/WS‑xx), but this cannot be retrieved from the accessible fragments without directly opening the UNESDOC record.

### 1.2 Mini‑micro CDS/ISIS: reference manual (version 2.3)

A later, clearly catalogued edition is:

- **Title:** *Mini‑micro CDS/ISIS: reference manual (version 2.3)*
- **Publisher:** UNESCO, Paris
- **UNESDOC ark:** `ark:/48223/pf0000211280`
- **Role of Del Bigio:** appears as “Giampaolo Del Bigio, Chief, Division of Software Development and Applications …” in the front matter.[^7]

This is the core technical specification for version 2.3 of the DOS Mini‑micro CDS/ISIS in the early 1990s. It supersedes or extends the 1985 reference manual and is squarely within the 1980–1995 window.

Archival location:

- UNESDOC: `https://unesdoc.unesco.org/ark:/48223/pf0000211280`.[^7]

Report number:

- The full PGI or internal report code is not visible in the snippet. Within UNESDOC, it is standard to list a PGI code (e.g. “PGI‑93/WS/xx”) on the cover or verso page; this must be read from the PDF itself.


### 1.3 Micro CDS/ISIS v.2/v.3 documentation (secondary evidence)

Several manuals and training texts from outside UNESCO cite the UNESCO reference manual as the authoritative technical documentation, under very similar titles and 1985 dating:

- UNAM library automation text cites:
“CDS/ISIS mini‑micro version: reference manual. UNESCO, 1985. 224 p.”[^4]
- Peruvian thesis bibliography cites:
“UNESCO (1985) CDS/ISIS mini‑micro version: reference manual.”[^5]
- Other bibliographies list:
“CDS/ISIS mini‑micro version: reference manual. (1985). New York: UNESCO. 193 p.”[^2]

From the user’s point of view, these are all references to the same UNESCO technical reference manual, with minor variations in page count.

***

## 2. “Design philosophy” and conceptual documentation

There does not appear to be a UNESCO‑branded document literally titled “Design Philosophy of CDS/ISIS” in 1980–1995 that is publicly indexed. Instead, the design philosophy of CDS/ISIS is conveyed in:

- Program overviews and historical sections in manuals and handbooks.
- Articles and newsletters (e.g. *Information Development*’s “CDS/ISIS Information” column).
- General descriptions of CDS/ISIS technology in later retrospectives.


### 2.1 System overview and design rationale in reference material

The reference manuals and later handbooks contain sections that effectively act as “design philosophy” expositions:

- The Micro CDS/ISIS Reference Manual (and similar DOS/Windows manuals) include:
    - A system overview describing CDS/ISIS as a generalized information storage and retrieval system for structured non‑numerical databases.[^8]
    - Explanations of record structure, master file and cross‑reference file separation, and directory‑style record layout inspired by ISO 2709/MARC.[^8]
    - Rationale for separating database definition (FDT, FST, PFT, etc.) from data, allowing generic software plus local configuration.[^6][^8]

These sections describe a modular, format‑driven architecture: all database semantics are encoded in external tables; the engine is kept generic and text‑oriented, matching the UNESCO objective of providing flexible bibliographic software for developing countries at low cost.[^9][^10][^3][^11][^12][^1]

### 2.2 External “design philosophy” references

Later literature summarises the design intent, even if it post‑dates the main 1980–1995 period:

- Historical notes explain that the original mainframe CDS/ISIS was designed in the mid‑1970s under Giampaolo Del Bigio for UNESCO’s Computerized Documentation System, based on the ILO’s ISIS.[^10][^13][^12][^9]
- A review in *Information Development* (“CDS/ISIS Information” by Alan Hopkinson, 1989) outlines goals: low‑cost, flexible bibliographic software aimed at developing countries, compatible with international standards such as ISO 2709 and the Common Communication Format (CCF).[^3][^1]
- Training and documentation repeatedly emphasise modularity and genericity: CDS/ISIS provides a generic text‑database engine; all domain specifics are handled by database definition and formatting tools (a “modular design philosophy”).[^14][^11][^8][^7]

Although these texts are not labelled “Design philosophy” as a standalone UNESCO technical report, together they represent the design philosophy documentation available for CDS/ISIS during and shortly after 1980–1995.

***

## 3. Giampaolo Del Bigio: documents and contributions

### 3.1 Role and positions

Giampaolo Del Bigio is consistently cited as:

- The original designer/architect of CDS/ISIS on IBM mainframes for UNESCO’s CDS in the mid‑1970s, based on the ILO ISIS.[^13][^11][^12][^9][^10]
- Chief of relevant units within UNESCO (e.g. “Chief, Division of Software Development and Applications”), as explicitly credited in the *Mini‑micro CDS/ISIS: reference manual (version 2.3).*[^7]
- Later Deputy Director (in UNESCO/PGI context), who presented overviews of CDS/ISIS and its evolution.[^15]


### 3.2 Technical or semi‑technical documents (1980–1995)

Within 1980–1995, identifiable Del Bigio contributions that relate directly to the CDS/ISIS system include:

1. **Internal authorship and editing of reference manuals and technical specifications**
    - Del Bigio is not always listed as “author” but appears in editorial/front‑matter roles in the reference manuals, indicating leadership of the development team and responsibility for the system specification.[^1][^3][^7]
    - The Micro CDS/ISIS reference manual and its later version 2.3 manual reflect his technical direction even if co‑written by staff.
2. **Overviews and evolution reports**
    - A workshop report (“The First Twenty Years” of IOC/IODE) notes that “the Deputy Director, Giampaolo Del Bigio” presented an overview of CDS/ISIS, noting that it had become the most widely used bibliographic software in the world, particularly in developing countries.[^15]
    - While this IOC document is oceanographic rather than core IT, the section on CDS/ISIS functions as a semi‑technical summary of the system’s role and design aims.
3. **Foreword to The CDS/ISIS Handbook (1994)**
    - The first edition of *The CDS/ISIS Handbook* (1994, Library Association) includes a foreword by Giampaolo Del Bigio. The later *CDS/ISIS for Windows Handbook* recalls his words from that foreword, describing the handbook as “complementary to the official Reference manual” and highlighting CDS/ISIS’s role as the world’s most widely used bibliographic information retrieval package.[^16][^6]
    - This foreword articulates the relationship between the official technical reference manual and user‑oriented documentation – a concise expression of UNESCO’s documentation philosophy.
4. **UNESCO Micro CDS/ISIS web page maintenance**
    - A German bibliographic record notes: “The UNESCO micro CDS/ISIS software [Computerdatei] / this page is maintained by Giampaolo Del Bigio. – [Paris], 1997.”[^17]
    - This is slightly outside the 1980–1995 window but indicates continuing responsibility for technical documentation and distribution infrastructure.

Archival locations:

- The most directly attributable Del Bigio‑linked technical UNESCO document within UNESDOC is the Mini‑micro CDS/ISIS reference manual version 2.3, ark `pf0000211280`, where he is named in the front matter.[^7]
- Del Bigio’s foreword is preserved in the original 1994 *CDS/ISIS Handbook*, which is accessible via UNESDOC:
`ark:/48223/pf0000099201` (The CDS/ISIS handbook – Buxton \& Hopkinson).[^18]

UNESCO report numbers:

- For the IOC/IODE “First Twenty Years” document: this is an IOC/INF series document; the PDF is IOC/INF‑994, which includes the note on Del Bigio’s CDS/ISIS overview.[^15]
- For the reference manual and handbook, the PGI or related report numbers are not visible in the search excerpts and must be read directly from the cover pages in the PDFs.

***

## 4. Andrew Buxton: contributions in the CDS/ISIS context

Andrew Buxton’s principal CDS/ISIS‑related work in the relevant period is the UK Library Association handbook published with UNESCO’s support.

### 4.1 The CDS/ISIS Handbook (1994)

- **Title:** *The CDS/ISIS handbook*
- **Authors:** Andrew Buxton; Alan Hopkinson
- **Publisher:** Library Association (London), produced in cooperation with UNESCO
- **UNESDOC entry:** `ark:/48223/pf0000099201` (UNESCO catalogue record).[^18]
- **Year:** 1994
- **Extent:** 178 pages (according to UNESDOC).[^18]

Function and relationship to UNESCO documentation:

- Serves as a user‑level handbook for the DOS “CDS/ISIS for microcomputers” package, explaining database definition, indexing, formats, searching, and typical applications in more detail than the official reference manual.[^16][^6]
- Explicitly described in Del Bigio’s foreword as “complementary to the official Reference manual.”[^6]
- Widely cited as the standard approachable exposition of CDS/ISIS for practitioners, especially in the developing world.[^19][^16]

Archival location:

- UNESDOC record: `ark:/48223/pf0000099201`.[^18]

Although this book is not itself a UNESCO technical report with a PGI number, it is effectively part of the UNESCO documentation ecosystem and was produced at UNESCO’s request, as the later Windows handbook explains.[^16][^6]

### 4.2 Later but related: CDS/ISIS for Windows Handbook (post‑1995)

- **Title:** *CDS/ISIS for Windows Handbook*
- **Authors:** Andrew Buxton; Alan Hopkinson
- **Commissioned by:** UNESCO
- **Date:** early 2000s (reference manual 1998–2001), therefore outside the 1980–1995 scope.[^16][^6]

Although beyond the requested timeframe, this handbook is useful for tracing references backward:

- It cites the earlier UNESCO DOS reference manual and winISIS reference manuals and supplements.[^16]
- It reprints or quotes Del Bigio’s statement from his foreword to the original 1994 handbook, confirming the position of both handbooks relative to the official technical documentation.[^6]


### 4.3 Other technical articles

Andrew Buxton also authored later articles on putting CDS/ISIS databases on the internet (e.g. a 2006 *Program* article on Unix CDS/ISIS, JavaISIS, WWWISIS, etc.), but these fall outside the 1980–1995 range.[^20][^19]

***

## 5. Other UNESCO / CDS‑ISIS technical and training documents (1980–1995)

While the reference manuals and Buxton/Hopkinson handbook are the core, UNESCO also produced technical and training material around CDS/ISIS during the period. Some examples that intersect with CDS/ISIS, even if not exclusively technical reference works:

### 5.1 Creation and management of databases using CDS/ISIS

- **Title:** *Creation and management of databases using CDS/ISIS*
- **Publisher:** UNESCO
- **UNESDOC ark:** `ark:/48223/pf0000127825` (training/lesson material for CDS/ISIS).[^21]
- **Content:** lesson‑style material introducing CDS/ISIS concepts, database management, and basic operations.[^21]

Although more pedagogical than deeply technical, it can be considered semi‑technical documentation.

### 5.2 UNISIST / PGI materials and newsletters

Earlier UNISIST and PGI documentation (1970s–1980s) frames CDS/ISIS within UNESCO’s broader information policy:

- Hopkinson’s 1989 article “CDS/ISIS Information” in *Information Development* lists as references:
    - “CDS/ISIS (mini‑micro version) – reference manual. Paris, Unesco, 1985. 196 p. With supplements and additions.”[^3][^1]
    - “CCF: the Common Communication Format. 2nd ed. Paris, Unesco, 1988. (PGI‑88/WS/2).”[^3]
    - Other PGI manuals on machine‑readable bibliographic descriptions (e.g. PGI/86/WS/6).[^3]

These are not CDS/ISIS manuals per se, but they document the bibliographic standards that heavily influenced CDS/ISIS’s record and file design.

### 5.3 Tutorial introduction and sector‑specific manuals

Non‑UNESCO but strongly linked to UNESCO’s CDS/ISIS distribution:

- **A tutorial introduction to CDS/ISIS** – a tutorial on version 2.3 for small libraries (Alastair Smith), teaching use of UNESCO’s software.[^22]
- **IDIN manual** (OECD, Di Lauro, 1988), building on Micro‑ISIS and CCF.[^14][^3]

These are not UNESCO reports but indicate the extended technical literature ecosystem around CDS/ISIS.

***

## 6. Summary list: key items, report/record identifiers and locations

Below is a consolidated list of the main CDS/ISIS technical and quasi‑technical documents relevant to 1980–1995, with what can be established about report numbers and archive locations.

### 6.1 Core UNESCO system manuals

- **CDS/ISIS (mini‑micro version) – reference manual**
– Publisher: UNESCO, Paris
– Year: 1985
– Extent: approx. 193–196 p, “with supplements and additions”[^1][^2][^4][^3]
– Content: full technical reference for Micro CDS/ISIS (DOS).
– Likely PGI‑series report number (not visible in snippets; must be read from PDF).
– Location: UNESDOC via title search; also widely catalogued in academic and national libraries.[^2][^4][^1]
- **Mini‑micro CDS/ISIS: reference manual (version 2.3)**
– Publisher: UNESCO, Paris
– Role: updated reference manual for version 2.3 of the DOS Mini‑micro CDS/ISIS.
– Notable credit: Giampaolo Del Bigio appears as “Chief, Division of Software Development and Applications …” in the front matter.[^7]
– UNESDOC ark: `ark:/48223/pf0000211280`.[^7]
– Report number: a PGI‑style code is likely printed on the cover (must be read directly from the PDF).
- **Creation and management of databases using CDS/ISIS**
– Type: training/lesson booklet on CDS/ISIS database management.[^21]
– UNESDOC ark: `ark:/48223/pf0000127825`.[^21]


### 6.2 Associated handbooks and explanations

- **The CDS/ISIS handbook**
– Authors: Andrew Buxton, Alan Hopkinson
– Publisher: Library Association, London (prepared in cooperation with UNESCO)
– Year: 1994
– Extent: 178 p.[^18]
– Function: explains CDS/ISIS for Microcomputers; explicitly positioned as complementary to the UNESCO reference manual; includes a foreword by Giampaolo Del Bigio.[^6][^18][^16]
– UNESDOC ark: `ark:/48223/pf0000099201`.[^18]
- **CDS/ISIS for Windows Handbook** (post‑1995, but useful for context)
– Authors: Buxton \& Hopkinson
– Commissioned by UNESCO; distributed freely online.[^16][^6]
– References: *CDS/ISIS for Windows Reference manual (version 1.3)*, *Winisis – supplement to the Reference Manual*, etc., but these are 1998+ and outside your requested window.[^16]


### 6.3 Del Bigio‑linked documents

- **Mini‑micro CDS/ISIS: reference manual (version 2.3)** – front‑matter credits Del Bigio as chief of the division responsible for the software.[^7]
- **Foreword to The CDS/ISIS handbook (1994)**
– Del Bigio’s foreword is quoted in the later Windows handbook: recognising the handbook as complementary to the official reference manual and praising CDS/ISIS as “the world’s most widely used bibliographic information retrieval package.”[^6][^16]
– Location of original: 1994 *The CDS/ISIS handbook*, UNESDOC `ark:/48223/pf0000099201`.[^18]
- **Workshop and programme report references**
– In the IOC/INF‑994 “The First Twenty Years”, Del Bigio is mentioned as presenting an overview of CDS/ISIS, emphasising its widespread use, particularly in the developing world.[^15]
– This is not core technical documentation, but it provides an official UNESCO perspective on CDS/ISIS in the early 1990s.


### 6.4 Buxton contributions (inside or touching 1980–1995)

- **The CDS/ISIS handbook** (1994) – as above.[^6][^18]
- No UNESCO‑branded technical reference manuals authored by Buxton have been identified in the 1980–1995 window; his main CDS/ISIS role at that time was through the handbook and related training activities.

***

## 7. Practical notes for archival retrieval

For reconstructing design, architecture and evolution of CDS/ISIS in detail:

- **Start with the PDFs for:**
    - *CDS/ISIS (mini‑micro version) – reference manual* (1985) – via UNESDOC title search or any library catalogue entry.[^4][^1][^2]
    - *Mini‑micro CDS/ISIS: reference manual (version 2.3)* – ark `pf0000211280`.[^7]
    - *The CDS/ISIS handbook* – ark `pf0000099201`.[^18]
    - *Creation and management of databases using CDS/ISIS* – ark `pf0000127825`.[^21]
- **Within each PDF, extract:**
    - UNESCO series/report number (e.g. PGI‑xx/WS/yy).
    - Chapter(s) dealing with system overview, file structures, field/tag design and the rationale for the modular architecture, which collectively constitute the “design philosophy”.
- **For Del Bigio’s conceptual framing:**
    - Read his foreword in the 1994 *CDS/ISIS handbook* and any prefaces or introductory notes in the reference manuals where he is credited.[^6][^18][^7]
    - Use the IOC/INF‑994 PDF’s section on CDS/ISIS for a concise UNESCO view of the system’s impact and positioning in the early 1990s.[^15]

If desired, a next step would be a manual pass through those PDFs to pull exact PGI numbers, prefaces, and design‑philosophy passages into a structured bibliography with quotations.
<span style="display:none">[^23][^24][^25][^26][^27][^28][^29][^30][^31][^32][^33][^34]</span>

<div align="center">⁂</div>

[^1]: https://journals.sagepub.com/doi/10.1177/026666698900500302

[^2]: https://sistemas.iibi.unam.mx/biblioteca/pavd/latpdf/LAT002487.pdf

[^3]: https://journals.sagepub.com/doi/pdf/10.1177/026666698900500302

[^4]: https://ru.iibi.unam.mx/jspui/bitstream/IIBI_UNAM/L211/1/L211.pdf

[^5]: https://cybertesis.unmsm.edu.pe/backend/api/core/bitstreams/3b5e3807-9bdd-4c5e-9853-fd1a2f301454/content

[^6]: https://repository.mdx.ac.uk/download/f9c0d9133ebe5c44427949e3be2e7f7b1e235bb507118af5c7e524eb2c35ee46/698522/whandbk.pdf

[^7]: https://unesdoc.unesco.org/ark:/48223/pf0000211280

[^8]: http://utbapxubute.free.bg/WINISIS15rev.pdf

[^9]: https://en.wikipedia.org/wiki/CDS_ISIS

[^10]: https://cdsisis.org

[^11]: https://journal.code4lib.org/articles/4893

[^12]: https://lisstudymaterials.wordpress.com/wp-content/uploads/2017/12/dlis408_information_technology-applications.pdf

[^13]: https://henryspad7.files.wordpress.com/2015/01/j-isis-reference-manual-21-june-2014.pdf

[^14]: https://mjlis.um.edu.my/index.php/MJLIS/article/view/1697/4139

[^15]: https://www.jodc.go.jp/jodcweb/info/ioc_doc/INF/i0994.pdf

[^16]: https://repository.mdx.ac.uk/download/9f7f119f19b0f64efaaca2a3c64d0335a4fdc1589de4f8474a1303ed2289fd5a/1292800/whandbk.doc

[^17]: https://files.dnb.de/EDBI/deposit.ddb.de/ep/netpub/89/96/96/967969689/_data_stat/www.dbi-berlin.de/dbi_ber/dobi/dobinet/209104.html

[^18]: https://unesdoc.unesco.org/ark:/48223/pf0000099201

[^19]: https://opendocs.ids.ac.uk/articles/journal_contribution/Options_for_putting_CDS_ISIS_databases_on_the_internet/26445154

[^20]: https://www.emerald.com/dta/article/40/3/286/330218/Options-for-putting-CDS-ISIS-databases-on-the

[^21]: https://unesdoc.unesco.org/ark:/48223/pf0000127825

[^22]: https://nla.gov.au/nla.cat-vn2622769

[^23]: https://www.academia.edu/2620036/CDS_ISIS_the_second_decade

[^24]: https://abcd-community.org/download/www-isis-technical-reference-manual-v-5-1-0-00-12-01/

[^25]: https://openknowledge.fao.org/server/api/core/bitstreams/7644682f-c93f-40dd-b600-7bbd78f40cac/content

[^26]: https://www.gpntb.ru/win/inter-events/crimea2000/program/eng/Doc28.HTML

[^27]: https://journals.sagepub.com/doi/pdf/10.1177/026666698900500302?download=true

[^28]: https://journals.sagepub.com/doi/pdf/10.1177/026666699509110306?download=true

[^29]: https://www.scribd.com/presentation/36695931/Isis-Tutorial2

[^30]: https://discovery.ucl.ac.uk/id/eprint/1334914/1/AidaSlavicOverfield_thesis_UCL2005.pdf

[^31]: https://code.iim.th-koeln.de/birds/litie/search?q=editor_ss%3A%22schwerpunktinitiativen+%22digitale+information%22+der+alliance+der+deutschen+wissenschaftsorganisationen%22\&fq%5B%5D=type_ss%3A%22a%22\&fq%5B%5D=theme_ss%3A%22Bibliographische+Software%22

[^32]: https://pure.iiasa.ac.at/id/eprint/2951/1/WP-87-101.pdf

[^33]: https://fox.cs.vt.edu/DigitalLibrary/DLSB.pdf

[^34]: https://docbox.etsi.org/stf/archive/stf321_tispan3_ec_emergency_call_location/public/library/Ofcom%20(UK)/Communications%20-%20The%20next%20decade%20(Ofcom).pdf

