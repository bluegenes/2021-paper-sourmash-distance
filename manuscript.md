---
title: Alignment-free distance estimation ...
keywords:
- metagenomics
- OGRI
- ANI
lang: en-US
date-meta: '2020-12-28'
author-meta:
- N. Tessa Pierce Ward
- C. Titus Brown
header-includes: |-
  <!--
  Manubot generated metadata rendered from header-includes-template.html.
  Suggest improvements at https://github.com/manubot/manubot/blob/main/manubot/process/header-includes-template.html
  -->
  <meta name="dc.format" content="text/html" />
  <meta name="dc.title" content="Alignment-free distance estimation ..." />
  <meta name="citation_title" content="Alignment-free distance estimation ..." />
  <meta property="og:title" content="Alignment-free distance estimation ..." />
  <meta property="twitter:title" content="Alignment-free distance estimation ..." />
  <meta name="dc.date" content="2020-12-28" />
  <meta name="citation_publication_date" content="2020-12-28" />
  <meta name="dc.language" content="en-US" />
  <meta name="citation_language" content="en-US" />
  <meta name="dc.relation.ispartof" content="Manubot" />
  <meta name="dc.publisher" content="Manubot" />
  <meta name="citation_journal_title" content="Manubot" />
  <meta name="citation_technical_report_institution" content="Manubot" />
  <meta name="citation_author" content="N. Tessa Pierce Ward" />
  <meta name="citation_author_institution" content="Department of Population Health and Reproduction, University of California, Davis" />
  <meta name="citation_author_orcid" content="0000-0002-2942-5331" />
  <meta name="twitter:creator" content="@saltyscientist" />
  <meta name="citation_author" content="C. Titus Brown" />
  <meta name="citation_author_institution" content="Department of Population Health and Reproduction, University of California, Davis" />
  <meta name="citation_author_orcid" content="0000-0001-6001-2677" />
  <meta name="twitter:creator" content="@ctitusbrown" />
  <link rel="canonical" href="https://bluegenes.github.io/2021-ani-paper/" />
  <meta property="og:url" content="https://bluegenes.github.io/2021-ani-paper/" />
  <meta property="twitter:url" content="https://bluegenes.github.io/2021-ani-paper/" />
  <meta name="citation_fulltext_html_url" content="https://bluegenes.github.io/2021-ani-paper/" />
  <meta name="citation_pdf_url" content="https://bluegenes.github.io/2021-ani-paper/manuscript.pdf" />
  <link rel="alternate" type="application/pdf" href="https://bluegenes.github.io/2021-ani-paper/manuscript.pdf" />
  <link rel="alternate" type="text/html" href="https://bluegenes.github.io/2021-ani-paper/v/de414d1ea03a44279c8f92e8742269a29c84cbe6/" />
  <meta name="manubot_html_url_versioned" content="https://bluegenes.github.io/2021-ani-paper/v/de414d1ea03a44279c8f92e8742269a29c84cbe6/" />
  <meta name="manubot_pdf_url_versioned" content="https://bluegenes.github.io/2021-ani-paper/v/de414d1ea03a44279c8f92e8742269a29c84cbe6/manuscript.pdf" />
  <meta property="og:type" content="article" />
  <meta property="twitter:card" content="summary_large_image" />
  <link rel="icon" type="image/png" sizes="192x192" href="https://manubot.org/favicon-192x192.png" />
  <link rel="mask-icon" href="https://manubot.org/safari-pinned-tab.svg" color="#ad1457" />
  <meta name="theme-color" content="#ad1457" />
  <!-- end Manubot generated metadata -->
bibliography:
- content/manual-references.json
manubot-output-bibliography: output/references.json
manubot-output-citekeys: output/citations.tsv
manubot-requests-cache-path: ci/cache/requests-cache
manubot-clear-requests-cache: false
...






<small><em>
This manuscript
([permalink](https://bluegenes.github.io/2021-ani-paper/v/de414d1ea03a44279c8f92e8742269a29c84cbe6/))
was automatically generated
from [bluegenes/2021-ani-paper@de414d1](https://github.com/bluegenes/2021-ani-paper/tree/de414d1ea03a44279c8f92e8742269a29c84cbe6)
on December 28, 2020.
</em></small>

## Authors



+ **N. Tessa Pierce Ward**<br>
    ![ORCID icon](images/orcid.svg){.inline_icon}
    [0000-0002-2942-5331](https://orcid.org/0000-0002-2942-5331)
    · ![GitHub icon](images/github.svg){.inline_icon}
    [bluegenes](https://github.com/bluegenes)
    · ![Twitter icon](images/twitter.svg){.inline_icon}
    [saltyscientist](https://twitter.com/saltyscientist)<br>
  <small>
     Department of Population Health and Reproduction, University of California, Davis
     · Funded by NSF 1711984, NSF 2018911
  </small>

+ **C. Titus Brown**<br>
    ![ORCID icon](images/orcid.svg){.inline_icon}
    [0000-0001-6001-2677](https://orcid.org/0000-0001-6001-2677)
    · ![GitHub icon](images/github.svg){.inline_icon}
    [ctb](https://github.com/ctb)
    · ![Twitter icon](images/twitter.svg){.inline_icon}
    [ctitusbrown](https://twitter.com/ctitusbrown)<br>
  <small>
     Department of Population Health and Reproduction, University of California, Davis
     · Funded by Moore Foundation GBMF4551
  </small>



## Abstract {.page_break_before}




## Introduction

Pairwise overall genome relatedness forms the basis genome-based taxonomic classification and phylogentic analysis.
Average Nucleotide Identity (ANI) is a widely-accepted method for estimating genome similarity. 
Massive-scale sequencing of microbial genomes has necessitated a transition to alignment-free estimation of genome relatedness.
A number of alignment-free similarity estimates exist, including several that closely approximate ANI.


### Acknowledgements

Thank you to all the members and affiliates of the Lab for Data-Intensive Biology at UC Davis for providing valuable feedback on earlier versions of this manuscript. This manuscript was written using manubot [@doi:10.1371/journal.pcbi.1007128] and is available in a GitHub repository [@url:https://github.com/bluegenes/2021-ani-paper].

### Author Contributions

|Author|Contributions|
|---|---|
|NTP| Conceptualization; Methodology; Writing - Original Draft; Writing - Review and Editing; Visualization; Supervision; Funding Acquisition |
|...|...|
|CTB| Conceptualization; Methodology; Writing - Original Draft; Writing - Review and Editing; Visualization; Supervision; Funding Acquisition |

### Competing Interests

The authors declare no competing interests.


## References {.page_break_before}

<!-- Explicitly insert bibliography here -->
<div id="refs"></div>
