---
title: Scaled MinHash Containment enables alignment-free distance estimation across the tree of life
keywords:
- metagenomics
- OGRI
- ANI
lang: en-US
date-meta: '2021-01-21'
author-meta:
- N. Tessa Pierce-Ward
- C. Titus Brown
header-includes: |-
  <!--
  Manubot generated metadata rendered from header-includes-template.html.
  Suggest improvements at https://github.com/manubot/manubot/blob/main/manubot/process/header-includes-template.html
  -->
  <meta name="dc.format" content="text/html" />
  <meta name="dc.title" content="Scaled MinHash Containment enables alignment-free distance estimation across the tree of life" />
  <meta name="citation_title" content="Scaled MinHash Containment enables alignment-free distance estimation across the tree of life" />
  <meta property="og:title" content="Scaled MinHash Containment enables alignment-free distance estimation across the tree of life" />
  <meta property="twitter:title" content="Scaled MinHash Containment enables alignment-free distance estimation across the tree of life" />
  <meta name="dc.date" content="2021-01-21" />
  <meta name="citation_publication_date" content="2021-01-21" />
  <meta name="dc.language" content="en-US" />
  <meta name="citation_language" content="en-US" />
  <meta name="dc.relation.ispartof" content="Manubot" />
  <meta name="dc.publisher" content="Manubot" />
  <meta name="citation_journal_title" content="Manubot" />
  <meta name="citation_technical_report_institution" content="Manubot" />
  <meta name="citation_author" content="N. Tessa Pierce-Ward" />
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
  <link rel="alternate" type="text/html" href="https://bluegenes.github.io/2021-ani-paper/v/6fc183b39683ff4de8a6d37382030812114783df/" />
  <meta name="manubot_html_url_versioned" content="https://bluegenes.github.io/2021-ani-paper/v/6fc183b39683ff4de8a6d37382030812114783df/" />
  <meta name="manubot_pdf_url_versioned" content="https://bluegenes.github.io/2021-ani-paper/v/6fc183b39683ff4de8a6d37382030812114783df/manuscript.pdf" />
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
([permalink](https://bluegenes.github.io/2021-ani-paper/v/6fc183b39683ff4de8a6d37382030812114783df/))
was automatically generated
from [bluegenes/2021-ani-paper@6fc183b](https://github.com/bluegenes/2021-ani-paper/tree/6fc183b39683ff4de8a6d37382030812114783df)
on January 21, 2021.
</em></small>

## Authors



+ **N. Tessa Pierce-Ward**<br>
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

**Background**
Sequence similarity estimation is critical for genome analyses ranging from taxonomic classification to phylogenetic reconstruction.
Current practices are still insufficient for environmental samples. Even best-practices samples can only assign a small fraction of metagenomic sequencing to known species...
Given the scale of sequencing data now available, there is a great need for tools that can accurately estimate pairwise genome relatedness in an assembly-free and alignment-free manner.

**Results**
Here, we introduce an alignment-free k-mer based method for quickly and accurately estimating pairwise sequence similarity, including Average Nucleotide Identity (ANI) and Average Amino Acid Identity (AAI).
Because this method is assembly-independent and sequence-agnostic, it can be applied to both DNA and protein sequence data from across the tree of life. 
We demonstrate the utility of this technique with two primary examples: phylogenetic reconstruction of the genome-based prokaryotic taxonomy (GTDB) and fast and accurate microbial taxonomic classification.
To demonstrate utility in other domains, we demonstrate proof-of-concept analysis on two published eukaryotic and viral datasets.

**Conclusions**
Containment-based pairwise distance estimation via Scaled Minhash enables accurate assembly-free and alignment-free phylogenomic reconstruction and taxonomic classification across a wide range of evolutionary distances.

## Keywords (3-10)
Overall Genome Relatedness Index (OGRI), Average Nucleotide Identity (ANI), Average Amino Acid Identity (AAI), pairwise evolutionary distance



## Background

As the scale of genomic sequencing continues to grow, alignment-free methods for estimating sequence similarity have become critical for conducting tasks ranging from taxonomic classification to phylogenetic analysis on large-scale datasets [@doi:10.1186/s13059-016-0997-x; @doi:10.1186/gb-2014-15-3-r46].
The majority of alignment-free methods rely upon exact matching of k-mers: subsequences of length k, that can be counted and compared across datasets, with or without use of subsampling methods such as MinHash.
As k-mer based methods rely on exact sequence matches, they can suffer from limited sensitivity when comparing highly polymorphic sequences or classifying organisms from groups that are not well represented in reference databases.

Current best practices methods can still only categorize a fraction of the metagenomic and metatranscriptome data, especially for understudied and/or diverse habitats (xx% recovery for soil, xx% recovery ocean metagenomes, etc).
Even well-studied environments such as human gut can produce significant uncharacterized metagenome content.
"For example, a reference-based approach failed to map 35% of reads in the iHMP study on inflammatory bowel disease (Supp. Data. of (Franzosa et al., 2019)), omitting them from any further analysis. These reads may belong to unknown microbes, phage or viruses, plasmids, or accessory elements of known microbes, all of which can
play a role in disease.[from RO1]". This phenomenon is not restricted to metagenome samples. Alignment-based estimates can fail at larger evolutionary distances and even rRNA amplicon surveys may underestimate bacterial diversity [@doi:10.1128/AEM.00014-18].

To increase sensitivity of alignment-free methods, modified k-mer approaches have been introduced, including spaced seeds /split k-mers, which accommodate polymorphic sites in highly similar genomes (CITE).
For larger evolutionary distances, recent methods have turned to coding protein sequence, which is more conserved than the underlying DNA sequence.
Protein coding sequence alignment has long been the gold-standard for taxonomic and functional annotation [@pubmed:2231712; @doi:10.1038/nmeth.3176].
As microbial and viral genomes are gene-dense, [MinHash-based] alignment-free comparisons of translated protein sequence have been shown to increase sensitivity for taxonomic classification and genome discovery [@doi:10.1038/ncomms11257; @doi:10.1186/s13059-019-1841-x].
Here, we demonstrate the utility of protein k-mer comparisons for phylogenomic reconstruction and taxonomic classification at larger evolutionary distances and across both gene-rich and gene-sparse sequences.
We use Scaled Minhash containment estimates to facilitate conducting these comparisons at scale [Irber et al., 2021; @https://dib-lab.github.io/2020-paper-sourmash-gather/].

Scaled Minhash is a MinHash variant that selects a set of representative k-mers from a sequence dataset [@https://dib-lab.github.io/2020-paper-sourmash-gather/]. Unlike traditional MinHash, Scaled MinHash sketches scale with the size of the dataset, meaning each sketch will include a set proportion of k-mers in the input datset, rather than a set number of k-mers.
Downsampling sequencing datasets in this way enables estimation of containment, which has been shown to permit more accurate estimation of genomic distance, particularly for genomes of very different lengths [@doi:10.1016/j.amc.2019.02.018; @doi:10.1186/s13059-019-1875-0].
Streaming containment estimates have been shown to facilitate genome discovery and correlate with Mash Distance, a proxy for Average Nucleotide Identity (ANI) [@doi:10.1186/s13059-019-1841-x; @doi:10.1186/s13059-020-02159-0].

Standardized genomic measures of relatedness such as ANI and it's protein counterpart, Average Amino Acid Identity (AAI) have shown lasting utility for genome relatedness and phylogenomic analysis.
ANI and AAI encompass the sequence similarity of all orthologous genes, either in nucleotide or protein space.
Both been shown to be robust measure of overall pairwise genome relatedness even for highly incomplete datasets, such as those comprised of only ~4% of the genome or 100 genes [@doi:10.1128/AEM.01398-06; @doi:10.1038/ismej.2017.113].
ANI has emerged as the most widely-accepted method for estimating pairwise similarity of microbial genomes and delimiting species boundaries [@doi:10.1073/pnas.0906412106].
Recent research appears to confirm 95% ANI species threshold for prokaryotic species, although there is some debate as to the universality of this threshold [@doi:10.1038/s41467-018-07641-9; @doi:10.1128/mSystems.00731-19; @doi:10.1101/2020.07.27.223511].
AAI thresholds have been proposed for higher taxonomic ranks, <45%, 45-65% and 65-95% for family, genus, and species [@doi:10.1016/j.mib.2007.08.006; @doi:10.1038/ismej.2017.113].
While traditional alignment-based estimation of ANI and AAI are computationally intensive, sketching-based estimates and sketching-facilitated estimates have permitted ANI calculations at the scale of whole-databases [@doi:10.1186/s13059-016-0997-x; @doi:10.1186/s13059-019-1841-x; @doi:10.1038/s41467-018-07641-9].

Pierce-Ward et al., 2021 showed that Scaled MinHash containment estimates can be used to approximate both ANI (nucleotide k-mers) and Average Amino Acid Identity (AAI; protein k-mers), while accounting for the nonindependence of mutated k-mers [@doi:10.1101/2021.01.15.426881].
Furthermore, Scaled MinHash estimates work well for genome pairs of varying lengths and for compositional analysis of metagenome samples.
Taken together, these properties enable robust assembly and alignment-free pairwise relatedness estimation that can be used on spequences separated by a wide range of evolutionary distances.
Here, we demonstrate that the utility of Scaled MinHash protein containment, both used directly and a an approximation of ANI and AAI, for taxonomic classification and phylogenomic reconstruction for species across the tree of life.


#### Notes

- AAI::phylogeny https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1236649/








## Results

![**Max Containment to ANI and AAI.** 
Containment calculation is guaranteed to be more similar to traditional calculation of Average Nucleotide Identity and Average Amino Acid Identity, which compared only the sections of genome that align. The shared k-mer content (containment numerator) can be thought of as the alignable sections of the genomes. 
The denominator of the Jaccard index is the alignable sections + the unalignable sections. 
The lower bound of the containment denominator will be the exact same as the numerator at 100% containment, where all k-mers are found within the comparison dataset. The upper bound will be the same as the Jaccard denominator, where all k-mers of the comparison dataset are found within the query dataset, and it is the query that contains any additional nonshared k-mers/unalignable sequence.
](images/containment-ANI-AAI.png){#fig:containmentANI}


Main q's to answer:
1. We promise it works
   - how does it compare with gold standard? (ANIb/ANIm)
   - how does it compare with current alignment-free methods (Mash, FastANI)
   - how does it function on contaminated and/or incomplete genomes?
   - how does it function on novel genomes that are v. distant from refs?


2. How is it useful?
   -

### Maximum-Containment ANI and AAI estimation (tech paper)

- jaccard vs containment vs total shared k-mers
- nucleotide vs protein (vs dayhoff?)

		
### Simulated data

ANI and AAI estimations were assessed on biologically-relevant simulated data from Criscuolo, 2020. 


#### alphabet and k-size selection for optimal distance estimation

### Alignment-free phylogenomic recontruction
_evolpaths analysis_
		




### Maximum-containment AAI enables fast and accurate taxonomic classification

### Comparison with other alignment-free methods (advantages, disadvantages, etc)


Alignment-based metrics are looking at the specific sequence variation of aligned regions, while k-mer based comparisons are comparing shared k-mers vs distinct k-mers. Since each nucleotide polymorphims generates mutated k-mers with an expected frequency, k-mer containment estimates can be used to accurately estimate both the Average Nucleotide Identity and Average Amino Acid Identity  [@doi:10.1101/2021.01.15.426881; @doi:10.1186/s13059-016-0997-x]


## Discussion



### Comparison with other alignment-free methods (advantages, disadvantages, etc)


## Conclusions


## Methods


## Availability of data and materials

## Competing Interests

The authors declare that they have no competing interests.

## Funding

## Authors' Contributions

|Author|Contributions|
|---|---|
|NTP| Conceptualization; Methodology; Writing - Original Draft; Writing - Review and Editing; Visualization; Supervision; Funding Acquisition |
|...|...|
|...|...|
|...|...|
|CTB| Conceptualization; Methodology; Writing - Original Draft; Writing - Review and Editing; Visualization; Supervision; Funding Acquisition |

## Acknowledgements

Thank you to all the members and affiliates of the Lab for Data-Intensive Biology at UC Davis for providing valuable feedback on this manuscript. This manuscript was written using manubot [@doi:10.1371/journal.pcbi.1007128] and is available in a GitHub repository [@url:https://github.com/bluegenes/2021-ani-paper].




## References {.page_break_before}

<!-- Explicitly insert bibliography here -->
<div id="refs"></div>
