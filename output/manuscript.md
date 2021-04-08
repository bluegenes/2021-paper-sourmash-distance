---
title: Scaled MinHash Containment enables alignment-free distance estimation across the tree of life
keywords:
- metagenomics
- OGRI
- ANI
lang: en-US
date-meta: '2021-04-08'
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
  <meta name="dc.date" content="2021-04-08" />
  <meta name="citation_publication_date" content="2021-04-08" />
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
was automatically generated
on April 8, 2021.
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

Sequence similarity estimation is critical for genome analyses ranging from taxonomic classification to phylogenetic reconstruction. Here, we introduce an alignment-free k-mer based method for quickly and accurately estimating pairwise sequence similarity, including Average Nucleotide Identity (ANI) and Average Amino Acid Identity (AAI). Because this method is assembly-independent and sequence-agnostic, it can be applied to both DNA and protein sequences across the tree of life. We demonstrate the utility of this method with similarity comparisons and protein taxonomic classification for benchmarking sets from the genome-based prokaryotic taxonomy (GTDB). We then extend the analysis to highly divergent and incomplete datasets as well as alternate domains of life.


## Keywords (3-10)
Overall Genome Relatedness Index (OGRI), Average Nucleotide Identity (ANI), Average Amino Acid Identity (AAI), pairwise evolutionary distance, Jaccard Index, Containment Index, MinHash, Scaled MinHash, k-mer



## Background

As the scale of genomic sequencing continues to grow, alignment-free methods for estimating sequence similarity have become critical for conducting tasks ranging from taxonomic classification to phylogenetic analysis on large-scale datasets [@doi:10.1186/s13059-016-0997-x; @doi:10.1186/gb-2014-15-3-r46].
The majority of alignment-free methods rely upon exact matching of k-mers: subsequences of length k, that can be counted and compared across datasets, with or without use of subsampling methods such as MinHash.
As k-mer based methods rely on exact sequence matches, they can suffer from limited sensitivity when comparing highly polymorphic sequences or classifying organisms from groups that are not well represented in reference databases.

Current best practices methods can still only categorize a fraction of the metagenomic and metatranscriptomic data, especially for understudied and/or diverse habitats (xx% recovery for soil, xx% recovery ocean metagenomes, etc).
Even well-studied environments such as human gut can produce significant uncharacterized metagenome content.
"For example, a reference-based approach failed to map 35% of reads in the iHMP study on inflammatory bowel disease (Supp. Data. of (Franzosa et al., 2019)), omitting them from any further analysis. These reads may belong to unknown microbes, phage or viruses, plasmids, or accessory elements of known microbes, all of which can
play a role in disease.[from RO1]". This phenomenon is not restricted to metagenome samples. Alignment-based estimates can fail at larger evolutionary distances and even rRNA amplicon surveys may underestimate bacterial diversity [@doi:10.1128/AEM.00014-18].

To increase sensitivity of alignment-free methods, modified k-mer approaches have been introduced, including spaced seeds /split k-mers, which accommodate polymorphic sites in highly similar genomes (CITE).
For larger evolutionary distances, protein-based comparisons have long been the gold-standard approach for taxonomic and functional annotation, as protein sequence is more conserved than the underlying DNA sequence [@pubmed:2231712; @doi:10.1038/nmeth.3176].
As microbial and viral genomes are gene-dense, [MinHash-based] alignment-free comparisons of translated protein sequence have been shown to increase sensitivity for taxonomic classification and genome discovery [@doi:10.1038/ncomms11257; @doi:10.1186/s13059-019-1841-x].
Here, we demonstrate the utility of protein k-mer comparisons for phylogenomic reconstruction and taxonomic classification at larger evolutionary distances and across both gene-rich and [gene-sparse] sequences.
We use Scaled Minhash subsampling to facilitate conducting these comparisons at scale [Irber et al., 2021; @https://dib-lab.github.io/2020-paper-sourmash-gather/].

Scaled Minhash is a MinHash variant for selecting and hashing a set of representative k-mers from a sequence dataset [@https://dib-lab.github.io/2020-paper-sourmash-gather/]. Unlike traditional MinHash, Scaled MinHash sketches scale with the size of the dataset, meaning each sketch is comprised of the chosen proportion of k-mers in the input dataset, rather than a chosen number of k-mers.
Downsampling sequencing datasets in this way enables estimation of containment, which has been shown to permit more accurate estimation of genomic distance, particularly for genomes of very different lengths [@doi:10.1016/j.amc.2019.02.018; @doi:10.1186/s13059-019-1875-0].
Streaming containment estimates have been shown to facilitate genome discovery and correlate with Mash Distance, a proxy for Average Nucleotide Identity (ANI) [@doi:10.1186/s13059-019-1841-x; @doi:10.1186/s13059-020-02159-0].

Standardized genomic measures of relatedness such as ANI and its protein counterpart, Average Amino Acid Identity (AAI) have shown lasting utility for genome relatedness and phylogenomic analysis.
Traditional ANI and AAI describe the sequence similarity of all orthologous genes, either in nucleotide or protein space, respectively.
Both been shown to be robust measure of overall pairwise genome relatedness even for highly incomplete datasets, such as those comprised of only ~4% of the genome or 100 genes [@doi:10.1128/AEM.01398-06; @doi:10.1038/ismej.2017.113].
ANI has emerged as the most widely-accepted method for estimating pairwise similarity of microbial genomes and delimiting species boundaries [@doi:10.1073/pnas.0906412106].
Recent research appears to confirm 95% ANI species threshold for prokaryotic species, although there is some debate as to the universality of this threshold [@doi:10.1038/s41467-018-07641-9; @doi:10.1128/mSystems.00731-19; @doi:10.1101/2020.07.27.223511].
AAI thresholds have been proposed for higher taxonomic ranks, <45%, 45-65% and 65-95% for family, genus, and species [@doi:10.1016/j.mib.2007.08.006; @doi:10.1038/ismej.2017.113].
While traditional alignment-based estimation of ANI and AAI are computationally intensive, sketching-based estimates and sketching-facilitated estimates have permitted ANI calculations at the scale of whole-databases [@doi:10.1186/s13059-016-0997-x; @doi:10.1186/s13059-019-1841-x; @doi:10.1038/s41467-018-07641-9].

[Pierce-Ward et al., 2021 (tbd technical paper)] showed that Scaled MinHash containment estimates can be used to approximate both ANI (nucleotide k-mers) and Average Amino Acid Identity (AAI; protein k-mers), while accounting for the non-independence of mutated k-mers [@doi:10.1101/2021.01.15.426881].
Furthermore, Scaled MinHash containment estimates work well for genome pairs of varying lengths and for compositional analysis of metagenome samples.
Taken together, these properties enable robust assembly and alignment-free pairwise relatedness estimation that can be used on sequences separated by a wide range of evolutionary distances.
Here, we demonstrate that the utility of Scaled MinHash protein containment, both used directly and a an approximation of ANI and AAI, for taxonomic classification and phylogenomic reconstruction for species across the tree of life.


#### Notes

- AAI::phylogeny https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1236649/








## Results
_somewhat mixed results and methods for now_


### Scaled Minhash jaccard enables accurate distance estimation
_(Correlation between Scaled MinHash Jaccard/Containment and ANI, AAI)_

To assess the utility of Scaled MinHash techniques across evolutionary distance, we generated a series of "evolutionary paths" from the set of 31k representative GTDB genomes.
Each evolutionary path offers six genome similarity comparisons at a range of evolutionary distances. 
For each genome comparison, we estimated Average Nucleotide Identity (ANI) using fastANI [@doi:10.1038/s41467-018-07641-9] and Average Amino Acid Identity (AAI) using compareM [@url: https://github.com/dparks1134/CompareM].

![**Scaled MinHash ANI vs FastANI**
GTDB Evolpaths Dataset](images/gtdb95-evolpaths.ANI-concordance.png){#fig:evolpathsANIvsfastANI}

![**Scaled MinHash AAI vs CompareM**
GTDB Evolpaths dataset](images/gtdb95-evolpaths.AAI-concordance.png){#fig:evolpathsAAIvsCompareM}


- Scaled MinHash Containment facilitates taxonomic classification
- Scaled MinHash Containment is robust to genome completeness


### k-mer containment searches enable similarity detection at increased evolutionary distances (nucl AND protein)





### Benchmarking Taxonomic Classification

First, we benchmarked protein-based gather classification using the high quality, highly complete reference genomes within the GTDB representative genome set.
For each genus, we randomly selected one reference genome for inclusion in the benchmarking reference database (n=9428).
For each genus with at least two species clusters, we randomly selected a second species within that genus for the test set of genomes (n=3911).
Thus, each test genome shares genus-level taxonomy with one (and only one) genome in the reference database.
Since we know that no test genome shares species-level taxonomy with the reference database, we used the lowest/least common ancestor approach described above to report taxonomic classifications at the genus level.
To assess the impact of 6-frame translation of nucleotide sequence on classification accuracy, we compared classification accuracy between published proteome queries and (6-frame) translated genome queries.
Using the same reference database, we selected an environmental dataset [@doi:] to assess the impact of genome completeness on taxonomic classification.
We compared gather-LCA classification to GTDB-Tk, a tool 


### Protein-level Taxonomic Classification
We also generated nucleotide and protein Scaled MinHash reference databases for all GTDB representative genomes (release 95, n=31,910).




![**K-mer Based Sequence Identity by Lowest Common Taxon**
GTDB Evolpaths dataset](images/anchor-mcANI-AAI.boxen.protnucl.png){#fig:evolpathsANIAAI}

**(DNA vs Protein)**
- _(just containment, no ANI/AAI)_
- _include dayhoff or just protein?_

K-mer analysis methods enable similarity detection as low as a single shared k-mer between divergent genomes. As a result, exact matching long nucleotide k-mers can be used for taxonomic classification between closely related genomes, including at the strain, species, and genus level (k-mer lengths 51, 31, and 21, respectively). At larger evolutionary distances, accumulated nucleotide divergence limits the utility of exact nucleotide k-mer matching. 

As protein sequences are more conserved than their coding nucleotide sequences, exact matching of protein k-mers can detect sequence similarity in spite of synonymous nucleotide substitutions that may have accumulated across the two sequences.

Exact matching of k-mers has long been deemed a shortcoming for k-mer based analyses, limiting similarity detection power across larger evolutionary distances. However, protein k-mers (and k-mers leveraging reduced protein alphabets) 


Using nucleotide k-mers
This property allows for low-level homology detection at the n

Protein sequences are more conserved than their underlying DNA sequences. Whole-proteome MinHash sketches are more similar than whole-genome DNA sketches, enabling us to find protein-level similarity across divergent genomes. 

For , e.g. Pseudomonas, XX% of k-mers are 	shared within the chosen/published genomes within species. For all published genomes within the genus, a median of xx% of k-mers are shared between genomes of one species and genomes of the a different species in the same genus.

rankinfo ... 	at ksize of 10...
-xx% of DNA k-mers are shared within-species
-yy% of protein k-mers are shared within-species
- zz% of DNA k-mers are shared within-genus
... etc 
== median or mean containment at rank?
containent = % of a genome's k-mers that are shared
-- do using ALL of gtdb, BUT, start with just a single set of genomes.. e.g. Pseudomonas? == similar to "shared k-mers" paper [@doi:10.24072/pci.genomics.100001]

![**Protein k-mer containment facilitates genus-level comparisons**
10k pseudomonas genome sequences, median containment at each alphabet](images/pseudomonas_jaccard_vs_containment_prot10.png){#fig:evolpathsContain}


#### k-size selection for optimal comparisons / distance estimation

- num shared k-mers at different ksizes
- 	e.g. k=7 much more common -- share far more k-mers. I assumed this would hurt, rather than help classification. Check!
-   do rankinfo on each database??

because kmer size matters --> conversion to AAI is useful!?
conversion to AAI does two things: accounts for k-mer length, ...


![**Protein k-mers facilitate comparisons across species**
This currently uses the evolutionary paths dataset. Perhaps better to demonstrate with a different test set -- say, just the species, genus family level, using something like Pseudomonas that has a lot of published genomes. Also show jaccard to emphasize how it gets progressively worse when you start comparing genomes that are different sizes? Or separate figure for this...?](images/anchor-containment.nucl-prot.png){#fig:evolpathsContain}


![**Containment-based ANI, AAI estimates, evolpaths**](images/anchor-evoldistPC.nucl3-prot.png){#fig:evolpathsANI}


	** core vs accessory distances **
	ANI/AAI == really getting at _core_


### Scaled Minhash distance estimation is robust to completeness
(unlike standard minhash https://drep.readthedocs.io/en/latest/choosing_parameters.html#importance-of-genome-completeness)


### Protein containment searches enable Sensitive/fast/accurate taxonomic classification
_(just containment, no ANI/AAI)_

to do, classification:
0. fix thumper (refactor branch) --> working + tests
1. implement "leave one xx clade out classification check"
 --> instead of just ignoring exact matches, ignore any matches in same species/genus/family
2. prelim figure for tara classification vs GTDB-Tk vs BAT
  - classification of incomplete genomes
  - for "contaminated" genomes .. can we randomly add contigs from diff species, see the impact? Like classification still works until xx% contaminated with something present in our database?
3. ksize diffs for classification? k=7 vs k=10 vs k=11?
  - time, sensitivity, specificity
4. virus development! (could be separate paper)

While more protein k-mers are shared across genomes within the same genus (and different species), min-set-cov + LCA allows us to find/report the most similar genome.

#### benchmarking :: Leave one out classification
_leave one clade out version? see CAT/BAT paper )_

[protein vs dna]

![Protein classification sensitivity](images/protein-sensitivity.rep-genus.gather.png){#fig:classification_sensitivity}

include 6-frame translation works well for database search
(sensitivity/specificity of Prodigal-translated vs 6-frame translated)

CAT/BAT paper [@doi:10.1186/s13059-019-1817-x]
("cat" = contig annotation, "bat" = bin annotation)



main point: more k-mers are shared = more k-mers available for matching

#### Classification of incomplete and contaminated genomes

#### virus classification

#### euk classification?? Too much.


### Containment-AAI enable alignment-free phylogenomic reconstruction
_evolpaths analysis_


Containment searches enable similiarity estimation, especially between genomes of different lengths. 

Max containment normalizes the shared content by the smaller of the two genomes

![**Max Containment to ANI and AAI.** 
Containment calculation is guaranteed to be more similar to traditional calculation of Average Nucleotide Identity and Average Amino Acid Identity, which compared only the sections of genome that align. The shared k-mer content (containment numerator) can be thought of as the alignable sections of the genomes. 
The denominator of the Jaccard index is the alignable sections + the unalignable sections. 
The lower bound of the containment denominator will be the exact same as the numerator at 100% containment, where all k-mers are found within the comparison dataset. The upper bound will be the same as the Jaccard denominator, where all k-mers of the comparison dataset are found within the query dataset, and it is the query that contains any additional nonshared k-mers/unalignable sequence.
](images/containment-ANI-AAI.png){#fig:containmentANI}

### median AAI across GTDB?	



#### alphabet and k-size selection for optimal distance estimation

- num shared k-mers at different ksizes
- 	e.g. k=7 much more common -- do rankinfo on each database! 

### Comparison with other alignment-free methods (advantages, disadvantages, etc)


Alignment-based metrics are looking at the specific sequence variation of aligned regions, while k-mer based comparisons are comparing shared k-mers vs distinct k-mers. Since each nucleotide polymorphims generates mutated k-mers with an expected frequency, k-mer containment estimates can be used to accurately estimate both the Average Nucleotide Identity and Average Amino Acid Identity  [@doi:10.1101/2021.01.15.426881; @doi:10.1186/s13059-016-0997-x]
	

## Discussion

K-mer based estimation of sequence identity has been limited to nucleotide sequences of similar size with high sequence identity (>80%),outside of which MinHash Jaccard is less well correlated with sequence identity [@doi:10.1186/s13059-016-0997-x; @doi:10.1038/s41467-018-07641-9].

By leveraging the Containment Index of Scaled MinHash sketches with both nucleotide and protein k-mers, we can extend accurate k-mer sequence identity to sequences of different sizes and to >50% Amino Acid Identity.


Cricuolo [@doi:10.12688/f1000research.26930.1] (suggests w/ appropriate correction, nucl MinHash Jaccard can be used up to >65% ANI??)

Here, we utilize Scaled MinHash sketches with Containment to overcome size differences between sequences being compared. 

To accurately estimate sequence identity from sequence files of different sizes(genomes, metagenomes, etc), we employ Scaled Minhash sketches, which enables estimation of the Containment Index. 



## Conclusions

Containment-based pairwise distance estimation via Scaled Minhash enables accurate assembly-free and alignment-free phylogenomic reconstruction and taxonomic classification across a wide range of evolutionary distances.

## Methods

### Scaled MinHash Sketching with Sourmash

As implemented in sourmash [@https://dib-lab.github.io/2020-paper-sourmash-gather; @doi:10.12688/f1000research.19675.1; @doi:10.21105/joss.00027], Scaled MinHash is a MinHash variant that uses a scaling factor to subsample the unique k-mers in the dataset to the chosen proportion (1/`scaled`).
As k-mers are randomized prior to systematic subsampling, Scaled MinHash sketches are representative subsets that can be used for comparisons, as long as the k-mer size and chosen scaled value remain consistent. 
Unlike traditional MinHash sketches, Scaled MinHash sketches enable similarity estimation with containment, which permits more accurate estimation of genomic distance when genomes or datasets differ in size [@doi:10.1016/j.amc.2019.02.018;@doi:10.1186/s13059-019-1875-0]. 

Sourmash supports sketching from either nucleotide or protein input sequence.
All genome sequences were sketched with sourmash v4.0 using the `sourmash sketch dna` command, k-mer sizes of 21,31,51, a scaling factor of 1000. 
Sourmash also supports 6-frame translation of nucleotide sequence to amino acid sequence.
To assess the utility of these translated sketches, genome sequences were also sketched with the `sourmash sketch translate` command at protein k-sizes (_kaa-mer sizes?_) of 7-12 and a scaling factor of 100. 
All proteome sequences were sketched with sourmash v4.0 using the `sourmash sketch protein` command at protein k-sizes (_kaa-mer sizes?_) of 7-12 and a scaling factor of 100.
Where higher scaling factors were evaluated, these original sketches were downsampled using the sourmash `downsample` method prior to conducting sequence similarity comparisons.


### Sequence Identity Estimation from Scaled MinHash
_(very DRAFTy)_

Sourmash contains standard implementations of Jaccard Index [@doi:10.1186/s13059-016-0997-x] and Containment Index [@doi:10.1016/j.amc.2019.02.018] set comparisons.

**Estimating Sequence Similarity from Jaccard**
For a comparison between two genomes (genomeA, genomeB), the Jaccard Index represents the k-mers shared between the two genomes (sketch intersection) divided by the k-mers present in both sketches (sketch union).
Thus the Jaccard Index represents the percent of shared k-mers relative to all k-mers across both genomes (intersection/genomeA+genomeB).
MinHash Sketch Jaccard has been shown to correlate well with ANI at high sequence identities (>=90% sequence identity) [@doi:10.1186/s13059-016-0997-x]; (>=80% sequence identity [@doi:10.1038/s41467-018-07641-9].

**Estimating Sequence Similarity from Containment**
As the Jaccard Index utilizes the union of all k-mers in a dataset, it is greatly affected by differences in dataset size [@doi:10.1093/bib/bbz083].
The Containment Index instead represents the percent of a genome found in the comparison genome.
Containment is directional: while the number of shared k-mers is fixed for a pairwise comparison, the Containment of each dataset will depend on the unique k-mers found in that particular dataset. Containment for genomeA will be (intersection/genomeA), while Containment for genomeB will be (intersection/genomeB).

Alignment-based ANI represents the sequence similarity of the alignable fraction of two genomes. In this way, ANI only compares the shared sequences, and discounts/ignores all other sequence present in either genome.
Bidirectional containment comparisons use the same numerator (shared k-mers), but may contain different numbers of non-shared k-mers in the denominator.

In cases where both genomes are high-quality and highly complete, we can most closely approximate ANI by using the maximum value between the bidirectional containment values: that is, using the comparison that represents the shared sequence over the genome with the smallest number of non-shared k-mers.

In cases where one genome is more trusted (high quality and highly complete), Containment may be best calculated relative to the trusted genome.
This use case also allows us to estimate sequence identity from larger sequence collections, such as metagenomes.
By definition, metagenomes contain k-mers from many organisms.
We can take advantage of directional Containment by calculating the Containment Index of Reference genomes that share many k-mers with the Metagenome.
We have already shown the utility of Containment for metagenome classification [@https://dib-lab.github.io/2020-paper-sourmash-gather], but now we can report estimated average sequence identity between the matching sequence regions and the reference genome.

**Estimating Sequence Identity from Scaled MinHash**

**_TBD_**

Blanca et al, 2021 [@doi:10.1101/2021.01.15.426881] presented a method to estimate the mutation rate between MinHash sketches while accounting for the non-independence of mutated k-mers. Using [@https://github.com/KoslickiLab/mutation-rate-ci-calculator], we estimate Sequence Identity from Scaled MinHash Containment.

Estimating sequence similarity from Scaled MinHash requires a good estimate of the number of unique k-mers in the sketched sequencing dataset [@https:https://github.com/dib-lab/sourmash/pull/1270]...




### GTDB "Evolutionary Paths" Dataset

The Genome Taxonomy Database (GTDB) provides a genome-based taxonomy for bacterial and archaeal genomes [@doi:10.1038/s41587-020-0501-8].
To assess the utility of Scaled MinHash techniques across evolutionary distance, we generated a series of "evolutionary paths" from the set of 31k representative GTDB genomes.
For each genus with at least two species clusters, one representative genome was randomly selected as a path "anchor" genome.
To build the path, one additional genome was selected from the representative genomes matching the anchor's taxonomy at each higher taxonomic rank.
Each path thus consisted of seven genomes: an anchor genome, a genome matching anchor taxonomy down to the genus level, one matching anchor taxonomy to the family level, one matching to the order level, and so on.
This creates a gradient of similarity, where comparisons to the anchor genome range from genus-level to superkingdom-level.
Path selection using the representative genomes in GTDB release 95 resulted in 2957 paths comprised of 6690 unique genomes (6543 Bacteria, 237 Archaea).
These paths include genome comparisons across 33 phyla (29 Bacteria, 4 Archaea), covering roughly a quarter of the 129 phyla (111 Bacteria, 18 Archaea) in GTDB release 95.
While paths are limited to taxonomies with at least two GTDB representative genomes for each taxonomic rank, these paths provide a rich resource for comparisons at increasing evolutionary distances. 


### Scaled MinHash Sequence Identity Correlates with Standard Methods

FastANI v1.32 ([@doi:10.1038/s41467-018-07641-9]; run with default parameters)  was used to obtain Average Nucleotide Identity between the anchor genome and each additional genome in its evolutionary path.
FastANI is targeted at ANI values between 80%-100%, so only values in this range are considered "trusted" and used in **assessing the correlation between Scaled MinHash estimates and FastANI._(TBD)_**

CompareM v0.1.2 ([@url:https://github.com/dparks1134/CompareM]; run with `--sensitive` parameter for DIAMOND mapping) was used to obtain Average Amino Acid Identity between the anchor proteome and each additional proteome in its evolutionary path.
CompareM reports the mean and standard deviation of AAI, as well as the fraction of orthologous genes upon which this estimate is based.
Briefly, CompareM calls genes for each genome or proteome using PRODIGAL [@doi:10.1038/nmeth.3176] and conducts reciprocal best-hit mapping via DIAMOND [@doi:10.1186/1471-2105-11-119].
By default, CompareM requires at least 30% percent sequence identity and 70% percent alignment length to identify orthologous genes.
As DIAMOND alignment-based homology identification may correlate less well with BLAST-based homology under 60% sequence identity [@url:https://rodriguez-r.com/blog/aai-blast-vs-diamond/], **we also ran compareM with a percent sequence identity threshold of 60% to obtain a set of high-confidence orthologous genes for AAI estimation. We report correlation between Scaled MinHash AAI estimation and each of these compareM parameter sets in XX _(TBD)_**. _CompareM was also used to obtain AAI values directly from each genome, using PRODIGAL to translate sequences prior to gene calling. These results [were not significantly different from proteome-based AAI estimation??] (Supplemental XX)._


### Taxonomic Classification with Sourmash Gather

To take advantage of the increased evolutionary distance comparisons offered by protein k-mers, we apply compositional analysis with sourmash gather [@https://dib-lab.github.io/2020-paper-sourmash-gather] to protein sequences (amino acid input and 6-frame translation from nucleotides).
Sourmash gather is conducted in two parts: 
First (preselection), gather searches the query against all reference genomes, building all genomes with matches into a smaller, in-memory database for use in step 2.
Second (decomposition), gather does iterative best-containment decomposition, where query k-mers are iteratively assigned to the reference genome with best containment match.
In this way, gather reports the minimal list of reference genomes that contain all of the k-mers that matched any reference in the database.

For reference matches with high sequence identity (ANI) to the query, we classify the query sequence as a member of the reference taxonomic group, as in [@https://dib-lab.github.io/2020-paper-sourmash-gather].
**However, when ANI between the query and the top reference match exceeds the taxonomic rank threshold (e.g. species default 95%), we use a least/lowest common ancestor (LCA) approach to report likely taxonomy at a higher taxonomic rank _(TBD)_**.
Briefly, as gather reports non-overlapping genome matches, we can sum the k-mer matches for all genomes with shared taxonomies at the next higher taxonomic rank to report the best query containment at that rank.
As this gather-LCA approach first uniquely assigns k-mers to their best reference genome, it bypasses the impact of increasing database size on taxonomic assignment observed for other LCA-based k-mer classification approaches [@doi:10.1186/s13059-018-1554-6].


### Workflows and Computing Resources

Reproducible workflows associated with this paper are available at XX (gh link + doi for release), with datasets available at OSF (XX). All workflows were executed using snakemake >= 5.26 [@doi:10.12688/f1000research.29032.1)] on the FARM cluster at UC Davis, using practices outlined in [@doi:10.1093/gigascience/giaa140].













## Leftover Text


Here, we apply k-mer based sequence identity estimation to generate taxonomic classification from the compositional results.


apply k-mer based sequence identity estimation with known taxonomic thresholds to report the most likely taxonomy for a given query genome.



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
