# Genetic and genomic analyses using RAD-seq and Stacks
## Credits
**Developed by:** Julian Catchen, Nicolas Rochette   
**Adapted by:** Ludovic Dutoit



### Plan

Throughout the day, we will work through the following plan:  

•   [Recap: A small bash for genomics exercise](bashgenomics.md)

•   Mini-Lecture Part 1A: What is RAD?  
•   Mini-Lecture Part 1B: Phred scores and the *process_radtags* cleaning algorithm.  
•   [Exercise I](stacks_exerciseI_dataprep.md): Data preparation.  
•   Mini-Lecture 2: Stacks, primary/secondary reads, and parameters.  
•   [Exercise II](stacks_exerciseII_denovo.md): *de novo* assembly of RAD tags without a genome  
•   [Further filtering](filteringSNPs.md): further filtering of the SNPs we obtain from the Stacks pipeline.  

### Objectives
The goal of this exercise is to familiarize ourselves with the use of next generation sequence
data produced from Reduced Representation Libraries (RRL) approaches such as
Restriction site Associated DNA (RAD-tags). These libraries are often used for genotyping
by sequencing, and can provide a dense set of single nucleotide polymorphism (SNP)
markers that are spread evenly across a genome. These markers are useful for a variety of
genetic and genomic analyses in model and non-model organisms. Students will gain
experience with a computational pipeline called Stacks that was designed for the analysis
of such data. Data will be analyzed *de novo* to perform a population analysis without the
aid of a reference genome. Stacks can also be used with a reference genome, as well as for many other analyses of RAD-seq data
such as constructing genetic maps and phylogeography, however, here we'll be focussing on population genomics.

### Introduction
The advent of short-read sequencing technologies has revolutionized the study of genomic
variation, leading to complete genomes of both model and non-model organisms. In addition, the long-standing dream of biologists of
having complete genomic information from numerous individuals from different
populations - both in the lab and wild - has become a
possibility for a variety of ecological and evolutionary studies, leading to the field of population genomics.

Until just a few years ago acquiring complete genomic information from
numerous individuals across many populations was out of reach for all but a small number of
model organisms. For example, producing a high density genetic map for an organism
required an immense investment of resources to first produce and then type the large
number of genetic markers needed to adequately cover the genome. Furthermore,
identifying genomic regions associated with phenotypic variation, or involved in the
adaptation of organisms to novel conditions, was restricted to organisms for which resequencing
projects produced a dense battery of genetic markers at a significant cost.

The limits to using whole genome sequencing for population genomic studies will gradually fade as the costs of sequencing continue to drop. However, using complete genome
re-sequencing is currently not feasible for many studies because costs are still significant and analysis remains challenging. Luckily, many
population genomic studies can use an alternative
approach called genotype-by-sequencing that occurs by the sequencing of reduced
representation libraries (RRL), and subsequent identification and scoring of SNPs and
inference of haplotypes. Although they do not provide complete genomic information,
these approaches provide data on hundreds of thousands of SNPs
and haplotypes spread across a genome at a fraction of the cost of complete resequencing.

One such RRL approach is Restriction-site Associated DNA sequencing
(RAD-seq), which has been used to identify signatures of selection, produce high density
genetic maps, help assemble genomes, and be useful for studies of allelic specific
transcriptional profiling. Because these data are relatively new, and the sample sizes of sequences
often so massive, a critical related breakthrough has been the development of algorithms
and software pipelines for the analysis of such data. Catchen et al. have produced Stacks for the
analysis of RAD-seq data. Today you will learn how to analyze RAD data with Stacks (without a
use of a reference genome, although this program can also make use of a reference genome if you have one available for your study organism) with the goal of identifying population structure. Through the completion of these
tasks you will learn how to process RAD-seq data and use the software programs `Stacks`
and `Structure.`

For more information on RAD genotyping and related methods, in particular conceptual
and statistical issues, see the papers listed at the end of this document. These papers will
help you better understand both the molecular biology, computational analyses, and
conceptual framework for the analysis of RRL data such as RAD.

### Software 
**Everything isopen source software**

• [Stacks](http://catchenlab.life.illinois.edu/stacks/) - A set of interconnected open
source programs designed initially for the *de novo* assembly of RAD sequences into
loci for genetic maps, and extended to be used more flexibly in studies of organisms
with and without a reference genome. The pipeline has a Perl wrapper allowing sets
of programs to be run. However, the software is modular, allowing it to be applied to
many scenarios.

• [Structure](http://pritch.bsd.uchicago.edu/structure.html) - A software program
originally written by Jonathan Pritchard and colleagues that uses Bayesian stochastic
models of multi-locus genotype data. The package was written to estimate the
distribution and abundance of genetic variation within and among populations.

• [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) - FastQC aims to provide a simple way to do some quality control checks on raw sequence data coming from high throughput sequencing pipelines. It provides a modular set of analyses which you can use to give a quick impression of whether your data has any problems of which you should be aware before doing any further analysis.

### Citations and Readings
**Protocols for running a Stacks analysis**

•Paris, J. R., Stevens, J. R., & Catchen, J. M. (2017). Lost in parameter space: a road map for stacks.
Methods in Ecology and Evolution, 188, 799–14.

•Rochette, N. C., & Catchen, J. M. (2017). Deriving genotypes from RAD-seq short-read data
using Stacks. Nature Protocols, 12(12), 2640–2659.

**Sources for data sets in the tutorial**

•Catchen, J. et al. 2013a. The population structure and recent colonization history of Oregon
threespine stickleback determined using restriction-site associated DNA-sequencing.
Molecular Ecology, 22:2864–2883.

•Nelson, T. C. and Cresko, W. A. 2018. Ancient genomic variation underlies repeated ecological
adaptation in young stickleback populations. Evolution Letters, 2: 9-21.

•McCluskey, B. M., & Postlethwait, J. H. (2015). Phylogeny of zebrafish, a "model species," within
*Danio*, a "model genus". Molecular Biology and Evolution, 32(3), 635–652.

**Core readings**

•Amores, A., et al. 2011. Genome evolution and meiotic maps by massively parallel DNA
sequencing. Genetics 188:799-808.

•Andrews, K. R., Good, J. M., Miller, M. R., Luikart, G., & Hohenlohe, P. A. (2016). Harnessing
the power of RADseq for ecological and evolutionary genomics. Nature Reviews Genetics 1–
12.

•Arnold, B. et al. 2013. RADseq underestimates diversity and introduces genealogical biases due
to nonrandom haplotype sampling. Molecular Ecology 22: 3179–3190.

•Catchen, J. et al. 2011. Stacks: building and genotyping loci *de novo* from short-read sequences.
G3: Genes, Genomes and Genetics 1:171-182.

•Catchen, J. et al. 2013b. Stacks: an analysis tool set for population genomics. Molecular Ecology
22:3124–3140.

•Davey, J. W., et al. 2011. Genome-wide genetic marker discovery and genotyping using nextgeneration
sequencing. Nature Reviews Genetics 12:499-510.

•Davey, J. W. et al. Special features of RAD Sequencing data: implications for genotyping.
Molecular Ecology 22: 3151–3164.

•Etter, P. D., et al. 2011. SNP Discovery and Genotyping for Evolutionary Genetics using RAD
sequencing. in Molecular Methods in Evolutionary Genetics, Rockman, M., and Orgonogozo,
V., eds.

•Ekblom, R., and J. Galindo. 2010. Applications of next generation sequencing in molecular
ecology of non-model organisms. Heredity 107:1-15.

•Hohenlohe, P. A. et al. 2010. Population genomics of parallel adaptation in threespine
stickleback using sequenced RAD tags. PLoS Genetics 6: 1-23.

•Lescak, E. A., Bassham, S. L., Catchen, J., gelmond, O., Sherbick, M. L., Hippel, von, F. A., &
Cresko, W. A. (2015). Evolution of stickleback in 50 years on earthquake-uplifted islands.
Proceedings of the National Academy of Sciences 112(52), E7204–12.
Population genomics background, concepts and statistical considerations

•Cariou, M. et al. 2013. Is RAD-seq suitable for phylogenetic inference? An *in silico* assessment
and optimization. Ecol Evol 3, 846–852.

•Gompert, Z., and C. A. Buerkle. 2011a. A hierarchical Bayesian model for next-generation
population genomics. Genetics 187:903-917.

•Hohenlohe, P. A., et al. 2010. Using population genomics to detect selection in natural
populations: Key concepts and methodological considerations. International Journal of Plant
Sciences 171:1059-1071.

•Luikart, G.,et al. 2003. The power and promise of population genomics: from genotyping to
genome typing. Nature Reviews Genetics 4:981-994.

•Lynch, M. 2009. Estimation of allele frequencies from high-coverage genome-sequencing
projects. Genetics 182:295-301.

•Nielsen, R., et al. 2005. Genomic scans for selective sweeps using SNP data. Genome Research
15:1566-1575.

•Nielsen, R., et al. 2011. Genotype and SNP calling from next-generation sequencing data.
Nature Reviews Genetics 12:443-451.

•Rubin, B. E. R. et al. 2012. Inferring Phylogenies from RAD Sequence Data. PLoS ONE 7,
e33394–e33394.

•Stapley, J., et al. 2010. Adaptation genomics: the next generation. Trends in Ecology and
Evolution 25:705-712.

**Empirical studies using RRL and RAD sequencing**

•Altshuler, D., et al. 2000. An SNP map of the human genome generated by reduced
representation shotgun sequencing. Nature 407:513-516.

•Baxter, S. W., et al. 2011. Linkage mapping and comparative genomics using next-generation
RAD sequencing of a non-model organism. PLoS ONE 6:e19315.

•Chutimanitsakun, Y., et al. 2011. Construction and application for QTL analysis of a Restriction
Site Associated DNA (RAD) linkage map in barley. BMC Genomics 12: 1-13.

•Emerson, K. J., et al. 2010. Resolving postglacial phylogeography using high-throughput
sequencing. Proceedings of the National Academy of Sciences 107:16196-16200.

•Gore, M. A., et al. 2009. A first-generation haplotype map of maize. Science 326:1115-1117.

•Richards, P. M. et al. 2013. RAD-Seq derived markers flank the shell colour and banding loci of
the Cepaea nemoralis supergene. Molecular Ecology 22, 3077–3089.

**RAD-seq genotyping methodology**

•Baird, N. A., et al. 2008. Rapid SNP discovery and genetic mapping using sequenced RAD
markers. PLoS ONE 3:e3376.

•Etter, P. D., et al. 2011. Local De Novo Assembly of RAD Paired-End Contigs Using Short
Sequencing Reads. PLoS ONE 6:e18561

•Hohenlohe, P. A., et al. 2011. Next-generation RAD sequencing identifies thousands of SNPs for
assessing hybridization between rainbow and westslope cutthroat trout. Molecular Ecology
Resources 11 Suppl 1:117-122.

•Miller, M. R., et al. 2007. Rapid and cost-effective polymorphism identification and genotyping
using restriction site associated DNA (RAD) markers. Genome Research 17:240-248.

•Willing, E. M., et al. 2011. Paired-end RAD-seq for de novo assembly and marker design without
available reference. Bioinformatics 27:2187-2193.

**Related reduced representation library (RRL) methodologies**

•Andolfatto, P., et al. 2011. Multiplexed shotgun genotyping for rapid and efficient genetic
mapping. Genome Research 21:610-617.

•Elshire, R. J., et al. 2011. A Robust, Simple Genotyping-by-Sequencing (GBS) Approach for High
Diversity Species. PLoS ONE 6:e19379.

•Peterson, B. K. et al. 2012. Double digest RADseq: an inexpensive method for de novo SNP
discovery and genotyping in model and non-model species. PLoS ONE 7, e37135.

•Rigola, D., et al. 2009. High-Throughput Detection of Induced Mutations and Natural Variation
Using KeyPoint™ Technology. PLoS ONE 4:e4761.

•van Orsouw, N. J., et al. 2007. Complexity reduction of polymorphic sequences (CRoPS): a
novel approach for large-scale polymorphism discovery in complex genomes. PLoS ONE
2:e1172.

•van Tassell, C. P., et al. 2008. SNP discovery and allele frequency estimation by deep sequencing
of reduced representation libraries. Nature Methods 5:247-252

•Wang, S. et al. 2012. 2b-RAD: a simple and flexible method for genome-wide genotyping.
Nature Methods 9, 808–810.

***

[Jump to Exercise I](stacks_exerciseI_dataprep)  
[Jump back to main workshop schedule](https://otagomohio.github.io/2019-06-11_GBS_EE/)
