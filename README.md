# Data Management Plan for DiSSCo infrastructure
Data Management Plan for DiSSCo infrastructure.

## Document information
| Date and version no. | Author | Comments/Changes |
| --- | --- | --- |
| 03.01.2025, v0.1 | Kessy Abarenkov | Adding basic structure and initial content |

## Table of Contents
1. [Introduction](#introduction)
2. [Lifecycle of DiSSCo Data](#lifecycle-of-dissco-data)
3. [Protected characteristics](#protected-characteristics)
4. [DiSSCo data summary](#dissco-data-summary)
5. [FAIR](#fair)
   - 5.1 [Making data findable](#making-data-findable)
   - 5.2 [Making data openly accessible](#making-data-openly-accessible)
   - 5.3 [Making data interoperable](#making-data-interoperable)
   - 5.4 [Increasing data re-use](#increasing-data-re-use)
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

## List of Figures

## Preface

### Status
The current Data Management Plan (DMP) for the DiSSCo infrastructure has been prepared as part of deliverable D3.3 of the DiSCCo Transition project. The DiSSCo DMP, initially published during the ICEDIG project ([D6.6](https://doi.org/10.5281/zenodo.3532937)) and later supplemented by the DiSSCo Prepare (D6.4) and DiSSCo Transition ([D5.1](https://doi.org/10.5281/zenodo.11451849)) projects, has been revised to reflect the project's status at the time of this deliverable. To improve accessibility, facilitate management, and track updates and changes, the provisional DMP has been updated and migrated to GitHub for ongoing revisions. One of the aims of deliverable D3.3 was to make the DMP machine-actionable, in alignment with the Research Data Alliance (RDA) DMP Common Standard for machine-actionable Data Management Plans [http://doi.org/10.15497/rda00039](http://doi.org/10.15497/rda00039). The test implementation of the maDMP for the DiSSCo infrastructure has been developed on the [PlutoF](https://plutof.ut.ee) platform.

### Acknowledgements

## Executive summary

## Summary of DiSSCo data management principles
The DiSSCo data management principles can be summarized as the following:

**DMpr 1:** All design decisions (technical, procedural, organisational, etc.) must be assessed for their effect on the protected characteristics. Such decisions and changes must not destroy or lessen the protected characteristics. (ref)

**DMpr 2:** Digitisation is the process of making physical objects digitally available, and the output of that process is Digital Specimens and Digital Collections. (ref)

**DMpr 3:** DiSSCo treats data as digital objects, each having a persistent identifier (pid) and a type. (ref)

**DMpr 4:** A link must be maintained by the Digital Specimen to the physical specimen it represents. This link is the identifier of the physical specimen. (ref)

**DMpr 5:** DiSSCo Facilities are encouraged to publish the fullest available digital data about their individual specimens and collections at the earliest opportunity, aiming as best practice to achieve at least MIDS level 2 for Digital Specimens and MICS level 2 for Digital Collections information. (ref)

**DMpr 6:** The principal digital object types to be managed by DiSSCo are: Collection and DigitalSpecimen. Other object types include: StorageContainer, SpecimenCategory, Presentation, Gathering, Annotation, Interpretation, and Provenance. (ref)

**DMpr 7:** Management of the DiSSCo digital object types shall be based on the general principles of the DiSSCo Data Management Plan, supplemented where necessary with additional management requirements for specific object types. (ref)

**DMpr 8:** Provenance data must be generated and preserved by all operations acting upon DiSSCo data objects. (ref)

**DMpr 9:** DiSSCo digital objects must be serialized as JSON [ECMA-404], as specified in section 4 and appendix A of the Digital Object Interface Protocol specification (DOIP) [DOIP 2.0 2018]. (ref)

**DMpr 10:** Information about Digital Specimens and Digital Collections must be published and managed as part of the European Collection Objects Index. (ref)

**DMpr 11:** Each Digital Specimen or other digital object instance handled by the DiSSCo infrastructure must be unambiguously, universally and persistently identified by a Natural Science Identifier (NSId), which shall be assigned when the object is first created. (ref)

**DMpr 12:** Each DiSSCo Facility shall be responsible for creating (minting) and managing their own NSIds in accordance with the DiSSCo policy for NSIds, and for registering their own Digital Specimens with the DiSSCo Hub infrastructure. (ref)

**DMpr 13:** Resolution of an NSId shall always return the current version of an object’s content, as well as any interpretations and annotations associated with it. (ref)

**DMpr 14:** The principle object types in DiSSCo (Digital Specimens, Digital Collections) are treated as mutable objects with access control and object history (provenance). (ref)

**DMpr 15:** Timestamped records of change (provenance data) must be kept, allowing reconstruction of a specific ‘version’ of a digital object at a date and time in the past. (ref)

## Introduction
DiSSCo, the Distributed System of Scientific Collections, is a state-of-the-art Research Infrastructure (RI) for natural science collections. Its goal is to digitally unify all European natural science assets into a single, integrated European collection, providing common access, standardised curation, and harmonised policies and practices across countries. With more than 200 institutions across 23 countries, DiSSCo offers uniform access to carefully curated natural science collections (i.e., data about physical specimens) within a community curation space open to contributions from diverse sources of expertise. Contributions to the data will no longer be limited by the capacities of collection-holding institutions, thus widening the base for generating new scientific knowledge. 

In addition to serving as the future framework for interpreting, validating, and improving specimen data, DiSSCo connects historical and contemporary collection data with literature data in which species are described, as well as data emerging from advanced techniques, such as DNA barcoding, whole genome sequencing, chemical analysis, trait studies, and imaging technologies. The human discoverability and accessibility of the DiSSCo knowledge base will enable researchers across disciplines to tap into a previously inaccessible pool of quality assured data, while its machine-readibility will enable users to seamlessly integrate these datasets into automated analytical workflows and tools.

With approximately 1.5 billion objects to be digitised, bringing natural science collections to the information age is expected to generate 90 petabytes of new data over the next two decades, with an anticipated daily use by 5,000 - 15,000 unique users. This requires new skills, clear policies and robust procedures to create, work with, and manage large digital datasets throughout the entire research data lifecycle, including their long-term storage, preservation, and open acess. DiSSCo ensures that all data complies with the FAIR principles (Findable, Accessible, Interoperable, and Reusable).

This document, the DiSSCo Data Management Plan (DiSSCo DMP), is a living document reflecting the active data management planning and stewardship philosophy adopted by DiSSCo. It focuses on maximising data openness and reusability, enduring data longevity and preservation, and promoting reproducible science. To address the changing needs, capabilities, and capacities of the evolving scientific community, this DMP will be revised as necessary to reflect current DiSSCo data management policies, associated decisions, and procedural changes.

## Lifecycle of DiSSCo Data

## Protected characteristics

## DiSSCo data summary

## FAIR

### Making data findable

### Making data openly accessible

### Making data interoperable

### Increasing data re-use

## Identification of DiSSCo Data

## Mutability, versioning and obsolescence

## Service management and service level agreements

## Data quality and minimum information standards

## Data security

## Data provenance

## Ethical and legal aspects

### Compliance with GDPR

## Software maintenance and sustainability

## Machine-actionable DMP for DiSSCo Infrastructure

## Glossary of terms and abbreviations
