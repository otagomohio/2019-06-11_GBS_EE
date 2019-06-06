IN CONSTRUCTION

# Genetic and genomic analyses using RAD-seq and Stacks
## Credits
**Developed by:** Julian Catchen, Nicolas Rochette   
**Adapted by:** Ludovic Dutoit

## Objectives
The goal of this exercise is to familiarize ourselves with the use of next generation sequence
data produced from Reduced Representation Libraries (RRL) approaches such as
Restriction site Associated DNA (RAD-tags). These libraries are often used for genotyping
by sequencing, and can provide a dense set of single nucleotide polymorphism (SNP)
markers that are spread evenly across a genome. These markers are useful for a variety of
genetic and genomic analyses in model and non-model organisms. Students will gain
experience with a computational pipeline called Stacks that was designed for the analysis
of such data. Data will be analyzed de novo to perform a population analysis without the
aid of a reference genome. Stacks can be used with a reference genome as well as for many other analyses of RAD-seq data
such as constructing genetic maps and phylogeography, although those are beyond the
scope of this exercise.

## Introduction
The advent of short-read sequencing technologies has revolutionized the study of genomic
variation from complete sequences in model organisms such as nematode worms, fruit
flies, zebrafish, mice and humans. In addition, the long-standing dream of biologists of
having complete genomic information from numerous individuals from different
populations in the lab and wild, the field of population genomics, is becoming a
possibility for a variety of ecological and evolutionary studies.
Until just a few years ago the goal of acquiring complete genomic information from
numerous individuals in many populations was out of reach for all but a small number of
model organisms. For example, producing a high density genetic map for an organism
required an immense investment of resources to first produce and then type the large
number of genetic markers needed to adequately cover the genome. Furthermore,
identifying genomic regions associated with phenotypic variation, or involved in the
adaptation of organisms to novel conditions, was restricted to organisms for which resequencing
projects produced a dense battery of genetic markers at a significant cost.
The limits to population genomic studies will gradually fade as the costs of second
generation sequencing continue to drop. However, many studies using complete genome
re-sequencing will not be feasible for a while because costs are still significant, high
quality read lengths are still too short, and analysis remains challenging. Luckily, many
population genomic studies can now efficiently be performed by using an alternative
approach called genotype-by-sequencing that occurs by the sequencing of reduced
representation libraries (RRL), and subsequent identification and scoring of SNPs and
inference of haplotypes. Although they do not provide complete genomic information,
these approaches provide a sufficient picture via data on hundreds of thousands of SNPs
and haplotypes spread across a genome at a fraction of the cost of complete resequencing.
We developed one such approach called Restriction-site Associated DNA sequencing
(RAD-seq), which has been used to identify signatures of selection, produce high density
genetic maps, help assemble genomes, and be useful for studies of allelic specific
transcriptional profiling. Because these data are so new, and the sample sizes of sequences
often so massive, a critical related breakthrough has been the development of algorithms
and software pipelines for the analysis of such data. We have produced Stacks for the
analysis of RAD-seq data. You will learn how to analyze RAD data with and without the
use of a reference genome with the goal of identifying population structure in one case
and identifying signatures of selection in a second case. Through the completion of these
tasks you will learn how to process RAD-seq data and use the software programs ```Stacks,
BWA and Structure.```

For more information on RAD genotyping and related methods, in particular conceptual
and statistical issues, see the [papers](https://github.com/otagomohio/2019-06-11_GBS_EE/blob/master/sessions/stacks.md#citations-and-readings) listed at the end of this document. These papers will
help you better understand both the molecular biology, computational analyses, and
conceptual framework for the analysis of RRL data such as RAD.

## Datasets and Software
### Datasets
*Short description of the dataset TOCOME *

### Software 
**All are open source software**

• [Stacks](http://catchenlab.life.illinois.edu/stacks/) - A set of interconnected open
source programs designed initially for the de novo assembly of RAD sequences into
loci for genetic maps, and extended to be used more flexibly in studies of organisms
with and without a reference genome. The pipeline has a Perl wrapper allowing sets
of programs to be run. However, the software is modular, allowing it to be applied to
many scenarios. You will use the Perl wrapper in class and the modules on your own.

• [Structure](http://pritch.bsd.uchicago.edu/structure.html) - A software program
originally written by Jonathan Pritchard and colleagues that uses Bayesian stochastic
models of multi-locus genotype data. The package was written to estimate the
distribution and abundance of genetic variation within and among populations,
patterns that are now commonly called the genetic structure of populations.

• [BWA](bio-bwa.sourceforge.net/) - BWA is a very fast and efficient software package
used for aligning sequences against a reference genome. We will use BWA to align
RAD reads against the stickleback reference genome, and then analyze these reads
within the Stacks pipeline. Although we will use BWA for this exercise, many other
algorithms and software exist for aligning against a reference genome, and these
could be used in conjunction with Stacks as well.

• [Samtools](www.htslib.org/) - A program that manipulates SAM and BAM files (the
primary file format that read alignments are stored) in very useful ways.

• [RAxML](http://sco.h-its.org/exelixis/web/software/raxml/index.html) - A software
program written by the Exelixis Lab for the construction of maximum likelihood
phylogenetic trees.


### Plan

Throughout the day, we will work through two main exercises:

•   Mini-Lecture 1: What is RAD?

•   Mini-Lecture 2: Phred scores and the *process_radtags* cleaning algorithm.

•   [Exercise I](stacks_exerciseI_dataprep.md): Data preparation.

•   Mini-Lecture 3: Stacks, primary/secondary reads, and parameters.

•  [Exercise II](stacks_exerciseII_denovo.md): de novo assembly of RAD tags without a genome

