# Data Management Plan for DiSSCo infrastructure
Data Management Plan for DiSSCo infrastructure.

## Document information
| Date and version no. | Author | Comments/Changes |
| --- | --- | --- |
| 03.01.2025, v0.1 | Kessy Abarenkov | Adding basic structure and initial content |

## Table of Contents
1. [Introduction](#introduction)
2. [FAIR Digital Object Architecture as the basis](#fair-digital-object-architecture-as-the-basis)
3. [Lifecycle of DiSSCo Data](#lifecycle-of-dissco-data)
   - 3.1 [Data acquisition](#data-acquisition)
   - 3.2 [Data curation](#data-curation)
   - 3.3 [Data publishing](#data-publishing)
   - 3.4 [Data processing](#data-processing)
   - 3.5 [Data use](#data-use)
4. [Protected characteristics](#protected-characteristics)
5. [DiSSCo data summary](#dissco-data-summary)
6. [Identification of DiSSCo Data](#identification-of-dissco-data)
7. [Mutability, versioning and obsolescence](#mutability-versioning-and-obsolescence)
8. [Service management and service level agreements](#service-management-and-service-level-agreements)
9. [Data quality and minimum information standards](#data-quality-and-minimum-information-standards)
10. [Data security](#data-security)
11. [Data provenance](#data-provenance)
12. [Ethical and legal aspects](#ethical-and-legal-aspects)
    - 12.1 [Compliance with GDPR](#compliance-with-gdpr)
13. [Software maintenance and sustainability](#software-maintenance-and-sustainability)
14. [Machine-actionable DMP for DiSSCo Infrastructure](#machine-actionable-dmp-for-dissco-infrastructure)
15. [Glossary of terms and abbreviations](#glossary-of-terms-and-abbreviations)

## List of Tables
- [Table 1.](#table-1) List of datasets and services managed by DiSSCo (partially adapted from DiSSCo Transition D5.1, Table 1 and [D6.6](https://doi.org/10.5281/zenodo.3532937), DiSSCo data summary).

## List of Figures
- [Figure 1.](#figure-1) A generic diagram to show how FDO fits into the architecture.
- [Figure 2.](#figure-2) Simplified lifecycle of DiSSCo data, focusing on Digital Specimen data.

## Preface

### Status
The current Data Management Plan (DMP) for the DiSSCo infrastructure has been prepared as part of deliverable D3.3 of the DiSCCo Transition project. The DiSSCo DMP, initially published during the ICEDIG project ([D6.6](https://doi.org/10.5281/zenodo.3532937)) and later supplemented by the DiSSCo Prepare (D6.4) and DiSSCo Transition ([D5.1](https://doi.org/10.5281/zenodo.11451849)) projects, has been revised to reflect the project's status at the time of this deliverable. To improve accessibility, facilitate management, and track updates and changes, the provisional DMP has been updated and migrated to GitHub for ongoing revisions. One of the aims of deliverable D3.3 was to make the DMP machine-actionable, in alignment with the Research Data Alliance (RDA) DMP Common Standard for machine-actionable Data Management Plans ([http://doi.org/10.15497/rda00039](http://doi.org/10.15497/rda00039)). The test implementation of the maDMP for the DiSSCo infrastructure has been developed on the [PlutoF](https://plutof.ut.ee) platform.

### Acknowledgements
The following individuals are gratefully acknowledged for their contributions to the present document: Wouter Addink, Sharif Islam

## Executive summary

## Summary of DiSSCo data management principles
The DiSSCo data management principles can be summarized as the following:

**DMpr 1:** All design decisions (technical, procedural, organisational, etc.) must be assessed for their effect on the protected characteristics. Such decisions and changes must not destroy or lessen the protected characteristics. (ref)

**DMpr 2:** Digitisation is the process of making physical objects digitally available, and the output of that process is Digital Specimens and Digital Collections. (ref)

**DMpr 3:** DiSSCo treats data as digital objects, each having a persistent identifier (pid) and a type. (ref)

**DMpr 4:** A link must be maintained by the Digital Specimen to the physical specimen it represents. This link is the identifier of the physical specimen. (ref)

**DMpr 5:** DiSSCo Facilities are encouraged to publish the fullest available digital data about their individual specimens and collections at the earliest opportunity, aiming as best practice to achieve at least MIDS level 2 for Digital Specimens and MICS level 2 for Digital Collections information. (ref)

**DMpr 6:** The principal digital object types to be managed by DiSSCo are: Collection and DigitalSpecimen. Other object types include: StorageContainer, SpecimenCategory, Presentation, Gathering, Annotation, and Provenance. (ref)

**DMpr 7:** Management of the DiSSCo digital object types shall be based on the general principles of the DiSSCo Data Management Plan, supplemented where necessary with additional management requirements for specific object types. (ref)

**DMpr 8:** Provenance data must be generated and preserved by all operations acting upon DiSSCo data objects. (ref)

**DMpr 9:** DiSSCo digital objects must be serialized as JSON [ECMA-404], as specified in section 4 and appendix A of the Digital Object Interface Protocol specification (DOIP) [DOIP 2.0 2018]. (ref)

**DMpr 10:** Information about Digital Specimens and Digital Collections must be published and managed as part of the European Collection Objects Index. (ref)
<!-- is the European Collection Objects Index (ECOI) an existing or planned repository? -->

**DMpr 11:** Each Digital Specimen or other digital object instance handled by the DiSSCo infrastructure must be unambiguously, universally and persistently identified by a Natural Science Identifier (NSId), which shall be assigned when the object is first created. (ref)

**DMpr 12:** Each DiSSCo Facility shall be responsible for creating (minting) and managing their own NSIds in accordance with the DiSSCo policy for NSIds, and for registering their own Digital Specimens with the DiSSCo Hub infrastructure. (ref)

**DMpr 13:** Resolution of an NSId shall always return the current version of an object’s content, as well as any annotations associated with it. (ref)

**DMpr 14:** The principle object types in DiSSCo (Digital Specimens, Digital Collections) are treated as mutable objects with access control and object history (provenance). (ref)

**DMpr 15:** Timestamped records of change (provenance data) must be kept, allowing reconstruction of a specific ‘version’ of a digital object at a date and time in the past. (ref)

## Introduction
DiSSCo, the Distributed System of Scientific Collections, is a state-of-the-art Research Infrastructure (RI) for natural science collections. Its goal is to digitally unify all European natural science assets into a single, integrated European collection, providing common access, standardised curation, and harmonised policies and practices across countries. With more than 200 institutions across 23 countries, DiSSCo offers uniform access to carefully curated natural science collections (i.e., data about physical specimens) within a community curation space open to contributions from diverse sources of expertise. Contributions to the data will no longer be limited by the capacities of collection-holding institutions, thus widening the base for generating new scientific knowledge. 

In addition to serving as the future framework for interpreting, validating, and improving specimen data, DiSSCo connects historical and contemporary collection data with literature data in which species are described, as well as data emerging from advanced techniques, such as DNA barcoding, whole genome sequencing, chemical analysis, trait studies, and imaging technologies. The human discoverability and accessibility of the DiSSCo knowledge base will enable researchers across disciplines to tap into a previously inaccessible pool of quality assured data, while its machine-readability will enable users to seamlessly integrate these datasets into automated analytical workflows and tools.

With approximately 1.5 billion objects to be digitised, bringing natural science collections to the information age is expected to generate 90 petabytes of new data over the next two decades, with an anticipated daily use by 5,000 - 15,000 unique users. This requires new skills, clear policies and robust procedures to create, work with, and manage large digital datasets throughout the entire research data lifecycle, including their long-term storage, preservation, and open access. DiSSCo ensures that all data complies with the FAIR principles (Findable, Accessible, Interoperable, and Reusable).

This document, the DiSSCo Data Management Plan (DiSSCo DMP), is a living document reflecting the active data management planning and stewardship philosophy adopted by DiSSCo. It focuses on maximising data openness and reusability, enduring data longevity and preservation, and promoting reproducible science. To address the changing needs, capabilities, and capacities of the evolving scientific community, this DMP will be revised as necessary to reflect current DiSSCo data management policies, associated decisions, and procedural changes.

## FAIR Digital Object Architecture as the basis
DiSSCo's architecture framework is built on the FAIR Digital Object (FDO) approach, advancing the concepts outlined in the ICEDIG project and RDA recommendations ([Islam et al., 2020](#islam-et-al-2020)). Each digital specimen in the infrastructure is assigned a PID (either DOI or Handle), ensuring persistent and unique identification. Digital objects across the ecosystem are treated as FAIR Digital Objects with their own JSON schemas, supported by FDO Profiles and FDO Records. These enable machine-actionable metadata, facilitating efficient discovery, interoperability, and reusability. The FDO Profiles specify required metadata attributes, while FDO Records provide a minimal, static kernel of essential elements for machine readability, aligned with RDA’s PID Kernel Information recommendations. This implementation supports scalable data processing, seamless integration, and adherence to FAIR principles. 

This implementation was based on the ICEDIG work and the core concept of 'digital objects'—open, editable, and interactive entities representing physical or digital assets. The Digital Object Architecture (DOA; [Kahn 2006](#kahn-2006), [Wittenburg 2019](#wittenburg-2019)) provides a technology-neutral and future-proof foundation that accommodates the evolution and replacement of specific data management technologies over time. This flexibility ensures that the DiSSCo infrastructure remains adaptable and sustainable throughout its lifecycle.

Persistent Identifiers (PIDs) are integral to this framework, ensuring unique, unambiguous identification and enabling robust citation, reproducibility, and data provenance. These identifiers connect digital objects to their physical counterparts, record their history, and facilitate meaningful linkages across datasets and systems. By leveraging established best practices, such as those from the ENVRI community ([ENVRI 2017](#envri-2017)), DiSSCo enhances data accessibility, interoperability, and long-term usability, ensuring the infrastructure remains FAIR-compliant throughout its lifecycle.

![alt text](https://github.com/TU-NHM/DiSSCo_DMP/blob/main/images/DiSSCo_DMP_FDO.png "Figure 1")

<a name="figure-1"></a>**Figure 1.** A generic diagram to show how FDO fits into the architecture.

## Lifecycle of DiSSCo Data
DiSSCo handles various types of data, some of which are generated by the DiSSCo infrastructure, while others are reused - provided by the DiSSCo Facilities, stored, and published within the DiSSCo infrastructure. A significant portion of the data managed by DiSSCo consists of Digital Specimen data - produced by the DiSSCo Facilities through the operation of digitisation lines or factories, which can be carried out either in-house or externally. Data produced through digitisation follows a lifecycle (Figure 1):

![alt text](https://github.com/TU-NHM/DiSSCo_DMP/blob/main/images/DiSSCo_DMP_data_lifecycle.png "Figure 2")

<a name="figure-2"></a>**Figure 2.** Simplified lifecycle of DiSSCo data, focusing on Digital Specimen data.

All activities, data management principles, applications, services and software tools of the DiSSCo infrastructure are designed and implemented to support this DiSSCo data lifecycle.

> [!NOTE]
> More detailed information about the lifecycle of DiSSCo data can be found in Hardisty (2019) ([D6.6](https://doi.org/10.5281/zenodo.3532937)).

### Data acquisition
Data acquisition is concerned with the principal activity of digitising physical specimens by dedicated digitisation lines/factories. This involves prioritising the specimens and collections to be digitised; retrieving, transporting and preparing specimens or containers from collection storage to be processed for digitisation, cleaning specimens to be digitised, and returning to storage afterwards; and operating digitisation equipment to digitise specimens (capture information, transcription, imaging). These operations are carried out by the DiSSCo Facilities.

### Data curation
Data curation is concerned with curating digital specimen and collection data. This involves caring for and improving the data resulting from digitisation processes in the data acquisition phase e.g., checking, cleaning and improving data i.e., quality control, assigning (persistent) identifiers, depositing in databases/image stores, etc. Data produced by digitisation is normally curated in the Collection Management Systems (CMS) of DiSSCo Facilities.

### Data publishing
Data publishing is concerned with making curated data accessible to DiSSCo users and publicly to parties external to the DiSSCo infrastructure (e.g. GBIF), as well as directly to other services within DiSSCo. The work is carried out by data publishers following data publishing procedure that leads to data becoming publicly available in a database and/or a scholarly data paper. Data publishing is based on the DiSSCo open access policy (ref) and must adhere to relevant quality control criteria, including relevant minimum information standards (e.g., [MIDS](https://www.tdwg.org/community/cd/mids/)) for the type of data being published. Specimen data must be published as Digital Specimen objects in DiSSCo's Digital Specimen Repository (ref) by DiSSCo Facilities.

### Data processing
Data can be further processed after it has been curated and published, which falls under the data processing phase. DiSSCo provides a range of services (expected to grow over time) for transforming data from one form to another (e.g., serving data in various useful representation formats such as JSON, RDF, CSV, etc.), for collating and aggregating data (e.g., to produce data summaries), and for analysing data in different ways. The results of data processing can include new data (such as annotations by external users), which must be curated within the infrastructure and subsequently published.

### Data use
In the final lifecycle phase, data use, the broader research community can exploit the digital and physical collections for science and can design digital experiments and analyses acting on the published and processed data. These experiments produce results (new data) that in turn can be acquired by DiSSCo for further curation, publishing and processing, thus restarting the lifecycle.

Much of the data managed by DiSSCo requires interpretation and validation. Information can change as new knowledge becomes available. This presents challenges for research reproducibility from the perspective of tracking workflow and data integrity.

## Protected characteristics
There are nine characteristics (Cn) of DiSSCo data management that are essential to protect throughout and ultimately beyond the lifetime of the DiSSCo data infrastructure. This lifetime is expected to be 25 – 30 years. These characteristics are essential for engendering community trust in the value, veracity and reliability of the data to be managed.

This means that proposals for design decisions and changes, technical, procedural and organisational) must be assessed for their effect on the protected characteristics. Ideally, all design decisions and changes must not destroy or lessen any of the protected characteristics and should aim to enhance one or more of the characteristics.

### Centrality of the digital specimen (C1)
The digital surrogate of the physical specimen, as represented by a Digital Specimen (DS) object type is the central asset of interest in the DiSSCo infrastructure and is the design unit/concept that all other design decisions must respect.

### Accuracy and authenticity of the digital specimen (C2)
The digital specimen, as represented by a Digital Specimen object type is the best available digital representation (surrogate) for a physical specimen in a natural science collection. The possibility of data reuse implies that digital specimen data can be adapted, remixed, transformed, and built upon for different purposes. It might not be obvious when this happens, so it is important that the accuracy, authenticity and meaning of the digital specimen data is clear and preserved throughout its lifetime.

### FAIRness (C3)
FAIRness is a characteristic exhibited by an infrastructure (component) and the data it manages when that infrastructure maintains compliance with the principles of FAIR (Findable, Accessible, Interoperable, and Reusable). This characteristic must be protected throughout the DiSSCo lifetime. The principles of the present DMP are oriented around maintaining FAIRness and this is substantially aided by adoption of Digital Object Architecture and treatment of DiSSCo data as digital objects.

### Protection of data (C4)
Data held and managed by DiSSCo must be protected in accordance with legal regulations and community norms for the kind of data concerned. For example, data considered to be sensitive by the community, such as that revealing the geographical location of endangered species must be protected from unauthorised access. Data revealing personal details of individuals such as researchers and collectors must be protected in accordance with the EU’s General Data Protection Regulation 2016/679.

### Preserving readability and retrievability (C5)
Maintaining the ability to retrieve categorical reference images from 'deep archive' and preserving the readability of the image and other file formats over long periods of time is essential. This means maintaining the ability to read and use:
a) Lossless, archived TIFF files and the related JPEG files used for data sharing and data processing;
b) Files in other specific formats, even after those formats become obsolete.
It means (potentially) systematically replacing image files in image archives/repositories with newer files using up-to-date file formats.

### Traceability (provenance) of specimens (C6)
Traceability (provenance) of specimens, their digitisation and change history, annotation and usage must be maintained consistently through the entire lifetime of the DiSSCo infrastructure. Storing and managing provenance information is a shared responsibility of the DiSSCo Facilities and DiSSCo Hub. Provenance shall be based on the W3C PROV framework ([W3C PROV 2013](#w3c-prov-2013)), with provenance stored as part of the digital specimen itself. The DiSSCo Trace subsystem is how this is achieved, requiring the adoption of a standard provenance framework (W3C PROV) and recording library wherever provenance must be recorded.

### Annotation history (C7)
Annotations attached to specimens and collections are an important part of the scientific and historical record (provability) and must not be lost or altered.

### Determinability (status and trends) of digitisation (C8)
Information (statistics) about the volume and scope (description) of natural history collections and their state of digitisation is needed, both to show progress and to assist with prioritisation of digitisation activities. This information must be maintained consistently to ensure a common basis for comparison is maintained over time. The Collections Digitisation Dashboard (CDD; [https://www.dissco.eu/services/#cdd](https://www.dissco.eu/services/#cdd)) is the subsystem by which this is achieved.

### Securability (C9)
Securability (authentication, authorization, accounting, auditing) of multiple levels of access for users according to their authority and permissions, including access to retrieve and/or modify sensitive information must be maintained over the DiSSCo lifetime; considering that potential users from come from many communities, not only the European research and education community.

## DiSSCo data summary
The scientific vision and mission of DiSSCo includes mobilising and harmonising natural science collection data as a single European digital virtual collection available in human and machine-readable forms via the Internet. At the same time, it includes connecting that historical collection data with data emerging from new techniques including imaging, tissue banking, DNA barcoding, whole genome sequencing, and legacy literature digitisation.

At the heart of DiSSCo are 'Digital Collections', 'Digital Specimens', and 'Digital Media', acting as digital representations in computer systems for collections and specimens in the real world. These digital representations are specialisations by DiSSCo of the more general-purpose notion of 'digital objects'.

The scope of DiSSCo includes all kinds of natural science collections, including fossils, rocks and minerals, anthropological artefacts, preserved biological specimens (plants, seeds, animals, insects, etc.) and living biological collections. Digital Specimens are at the heart of an interconnected graph of diverse and dispersed data classes, equipping them for many research and teaching purposes that might not otherwise be possible.

### Types of data generated/acquired
DiSSCo accrues and manages data comprising digital collections and digital specimens at progressively more comprehensive levels of digitisation, as well as other types of data relating to its subsystems for managing and administering the scientific use of collections and specimens (Table 1). This DMP primarily focuses on the principal data types - digital collections and digital specimens - but the principles it outlines are applicable to all types of data handled by DiSSCo. In the context of digital specimens and collections, DiSSCo data management distinguishes several categories of data to be managed:
1. **Specimen and collection data**: This refers to data about physical specimens and collections. A key characteristic of this data is its authoritative nature - it is determined by approved and authorised experts, such as scientists and curators.
2. **Annotations**: These are assertions that replicate the traditional written annotation of physical objects, such as species determination or comments relating to label information.
3. **Supplementary data (including third-party data)**: This encompasses additional data about a specimen that goes beyond the aforementioned categories and contributes to better understanding and increased knowledge of the specimen. Supplementary data can be generated by specimen owners or by third-parties and can include biodiversity literature references, DNA sequence data, trait data, acoustic recordings, or other relevant information related to specific specimens and collections. Such data may reside outside the DiSSCo infrastructure but can be referenced from DiSSCo.
4. **Provenance data**: This category provides a traceable record of the origins of the data and the processing actions applied to it.

<a name="table-1"></a>**Table 1.** List of datasets and services managed by DiSSCo (partially adapted from DiSSCo Transition D5.1, Table 1 and [D6.6](https://doi.org/10.5281/zenodo.3532937), DiSSCo data summary).
| Title | Type | Formats | Standards | Reference |
| --- | --- | --- | --- | --- |
| DiSSCover (Unified Curation & Annotation System) | Service or Interactive resource |  |  |  |
| ELViS (European Loans and Visits System) | Service or Interactive resource |  |  |  |
| CDD (Collection Digitisation Dashboard) | Service or Interactive resource |  |  |  |
| Digital Specimen Repository |  Service or Interactive resource |  |  |  |
| Knowledgebase | Service or Interactive resource |  |  |  |
| **Digital Collection data** | Dataset/Compiled data |  |  |  |
| **Digital Specimen data** | Dataset/Compiled data |  |  |  |
| Links to Digital Media (and other extended data) | Dataset/Compiled data |  |  |  |
| Annotations | Dataset/Compiled data |  |  |  |
| Provenance data | Dataset/Compiled data |  | W3C PROV Data Model |  |
| Method and protocol descriptions | Text/Research protocol |  |  |  |
| Infrastructure and operational data (logs, error reports) | Text/Log or Text/Error report |  |  |  |
| User authentication and authorization records | Text |  |  |  |
| DiSSCo agreed vocabularies and ontologies | Text |  |  |  |
| Technical documentation on standards developed by DiSSCo | Text |  |  |  |
| Transactions (loans, visits, access requests, queries) | Dataset/Compiled data |  |  |  |
| Website data | Interactive resource/Website |  |  |  |
| Literature (scientific papers, posters) | Text/Journal article or Text/Conference poster or Text/Conference paper or Text/Report |  |  |  |
| Dissemination and communication materials | Text/Blog post |  |  |  |
| Training materials | Learning object |  |  |  |


### Re-use of existing data
Digital Specimen data incorporated into DiSSCo's Digital Specimen Repository originates from the collection management systems used by DiSSCo Facilities. Therefore, it can be referred to as existing data that is re-used by DiSSCo. There is also a wide range of pre-existing data, such as biodiversity literature, genetic sequence and other molecular information, traits data, habitats data, alien and invasive species data, data about species conservation, etc. that can be linked with specimens in collection. DiSSCo makes it possible to build links between such data and Digital Specimens. 

### Expected size of the data
With approximately 1.5 billion physical specimens in Europe to be digitised, bringing natural science collections to the information age is expected to result in petabytes of new data over the next decades. However, the number of links between digital specimens and other related information could greatly exceed the number of objects themselves, perhaps by 3 – 5 times. This growth will continue as digital specimens become increasingly interconnected with other pieces of information related to the specimens. Additional sources of data expected to grow over the years include annotations data entered into the Unified Curation & Annotation System and provenance data linked to both Digital Specimen and Annotation records.

### Data utility
There is a wide range of traditional and new user groups for DiSSCo data. Conventionally, this community includes all researchers engaged in discovering, describing and interpreting life on Earth, both past and present, as well as researchers studying the geological history of the planet.

European collections hold circa 80% of the 2 million species presently described and are at the forefront of efforts to describe what is estimated to be approximately 6 million new species that await discovery ([Mora 2011](#mora-2011)). DiSSCo collections also include extensive palaeontological and mineralogical collections, including concentrations of rock and ore samples, making them a valuable resource for the field of economic geology as well as for research focused on climate change and the origin of our solar system.

The unprecedented taxonomic, geographic, stratigraphic and historical coverage gathered within these collections, coupled with their increasing digital accessibility, is opening them up to entirely new user communities, and increasingly to the private sector/industry. These users are increasingly drawn to the time series and patterns represented within these collections, to make predictions about the sustainable exploitation of bio- and geo-diversity that inform practice and policy decisions. Table 2 provides some examples of typical DiSSCo data usages beyond academic/scholarship uses. These also include education, virtual exhibitions, documentaries, citizen science, historians & artists.

**Table 2.** Typical purposes for DiSSCo data usage.
| Environment | Agriculture | Health | Border control | Biobanking |
| --- | --- | --- | --- | --- |
| - Urban planning<br />- Environmental impact assessment<br />- Deep-sea mining<br />- Conservation planning & monitoring<br />- Prospecting<br />- Shifts in species geographic distributions and abundances<br />- Biomes, ecosystems and environmental signatures and trends<br />- Tectonics | - Species identification<br />- Future domestication<br />- Land use change<br />Industrial (insect) farming<br />- Forestry<br />- Agri-chemicals<br />- Emergence of new pests and diseases<br />- Climate change, agricultural effects | - Pathogen identification<br />- Medicine and food supplement verification<br />- Pharmaceutical industry<br />- Biotechnology | - Invasive species and pests<br />- CITES protected species enforcement<br />- Countering illegal wildlife trade identification<br />- Shifts in species geographic distributions | Preserve genetic material (tissues & seeds) for:<br />- Research<br />- Government<br />- Industry (medicine, biotech. & agriculture) |

DiSSCo data is expected to be used on average by 5,000 – 15,000 unique users each day.

## Identification of DiSSCo Data

## Mutability, versioning and obsolescence

## Service management and service level agreements

## Data quality and minimum information standards

## Data security

## Data provenance

## Ethical and legal aspects

### Compliance with GDPR

## Software maintenance and sustainability

To ensure the long-term sustainability and maintainability of the software developed within the DiSSCo project, the following strategies will be implemented:
1. **Open Source:** All software developed under DiSSCo will be made publicly available as open-source software. By adhering to open-source principles, the project ensures transparency, collaboration, and community-driven development. We prefer using permissive licenses (e.g., MIT, Apache 2.0) to maximize the software’s reuse and integration potential with other projects and systems. 
2. **Version Control and Collaboration:** The source code and related assets will be hosted on GitHub, providing a central, version-controlled repository that supports collaboration and continuous integration. GitHub will facilitate community engagement through issues, pull requests, and code reviews, ensuring the software remains well-maintained and up-to-date. Repositories will include comprehensive documentation, contribution guidelines, and clear coding standards to support external contributors and ensure consistency and quality.
3. **Open Documentation and Review Process:** Clear, comprehensive, and up-to-date documentation will be maintained throughout the development of the software. Documentation will include user guides, API references, and technical specifications, making it easier for developers and end-users to understand and contribute to the software. The documentation will be hosted in public repositories (e.g., GitHub Pages) and subjected to open peer review and RFCs to encourage input from the community. This transparent review process ensures that the documentation is accurate, accessible, and improves over time. The open review process can also extend to the software itself, where the community can contribute to bug reports, feature suggestions, and code improvements.
4. ...

## Machine-actionable DMP for DiSSCo Infrastructure

## Glossary of terms and abbreviations

## References
- <a name="envri-2017"></a>ENVRIplus deliverable D6.1. 2017. D6.1 A system design for data identifier and citation services for environmental RIs projects to prepare an ENVRIPLUS strategy to negotiate with external organisations. http://www.envriplus.eu/wpcontent/uploads/2015/08/D6.1-A-system-design-for-data-identifier-and-citationservices-for-environmental-RIs.pdf
- <a name="islam-et-al-2020"></a>Islam, S., Hardisty, A., Addink, W., Weiland, C., & Glöckler, F. (2020). Incorporating RDA Outputs in the Design of a European Research Infrastructure for Natural Science Collections. In Data Science Journal (Vol. 19). Ubiquity Press, Ltd. https://doi.org/10.5334/dsj-2020-050
- <a name="kahn-2006"></a>Kahn, R. and Wilensky, R., 2006. A framework for distributed digital object services. International Journal on Digital Libraries, 6(2), pp.115-123. https://doi.org/10.1007/s00799-005-0128-x
- <a name="mora-2011"></a>Mora, C., Tittensor, D.P., Adl, S., Simpson, A.G.B., Worm, B. 2011. How Many Species Are There on Earth and in the Ocean?. PLOS Biology 9(8): e1001127. https://doi.org/10.1371/journal.pbio.1001127
- <a name="wittenburg-2019"></a>Wittenburg, P., Strawn, G., Mons, B., Boninho, L., Schultes, E. 2019. Digital Objects as Drivers towards Convergence in Data Infrastructures. doi: 10.23728/b2share.b605d85809ca45679b110719b6c6cb11
- <a name="w3c-prov-2013"></a>W3C PROV 2013 - Groth P and Moreau L (2013) PROV-Overview An Overview of the PROV Family of Documents. W3C Working Group Note 30 April 2013. https://www.w3.org/TR/provoverview/
