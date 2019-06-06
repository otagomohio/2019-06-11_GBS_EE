** Under construction **

# Filtering your SNPs

## Background
Congratulations! Over the last day you've learned how to use [STACKS](http://catchenlab.life.illinois.edu/stacks/) to generate a vcf file (and other file formats) containing variable SNPs derived from GBS/RADseq data. By tweaking some of the parameters of the STACKS pipeline (particularly m - the minimum read depth; M - the number of mismatches between alleles; and n - the number of mismatches between loci in the catalog), we can make it less likely that we've included problematic loci (e.g. paralogous loci smushed into one "super stack"). Other RADseq assembly pipelines like [ipyrad](https://ipyrad.readthedocs.io/) and [dDocent](http://www.ddocent.com/) also have similar parameters that can be tweaked.

Despite this, it is likely that a few problematic loci *are* going to sneak through into our dataset. These might include some [paralogous loci](https://en.wikipedia.org/wiki/Sequence_homology), which will be more heterozygous than expected because of fixed differences between the different 'true' loci that have been co-assembled into one paralogous locus. It might also include loci that have [null alleles](https://en.wikipedia.org/wiki/Null_allele#Evidence), that is, where the restriction enzyme site for one allele has been eroded by a mutation. This can make individuals look homozoygous at that site (and that locus to look more homozygous than you might expect in general), even though they are truly heterozygous. The impact of these problematic loci will depend on what you are using your data for, but null alleles can be particularly problematic for parentage analysis, because if an offspring inherits one of the null alleles from a parent there will be no data at that locus to suggest that those two relatives are linked.

## Filtering out loci that are out of HWE
Fortunately, we can screen for loci that are out of [Hardy-Weinberg Equilibrium](https://en.wikipedia.org/wiki/Hardy%E2%80%93Weinberg_principle) i.e. loci that appear to be too heterozygous/homozygous based on allele frequencies in the population. One problem we can face, however, is that a lot of the programs (e.g. []() ) that filter out loci that aren't in HWE assume we've only got a single population in our dataset. Why is this a problem? Welp, loci with null alleles and paralogous loci are not the only reasons you can be out of HWE. One big reason is [population structure](https://en.wikipedia.org/wiki/Wahlund_effect)! That's right! If we have multiple populations present in our data set, and we filter on HWE, then we might actually be tipping out the SNPs that are the most informatic about population structure!

## Solution? Only filter out loci that are out of HWE across multiple populations


## Oh, and we shouldn't forget about linkage disequilbrium either!



do downstream filtering based on things like Hardy-Weinberg Disequlibrium, and Linkage Disequlibrium


cs_1335.01, cs_1335.02, cs_1335.05, pcr_1211.04, pcr_1211.05,
            pcr_1211.06, stl_1274.33, stl_1274.35, stl_1274.37


## Other filtering parameters
There are a boat load of additional filters you have on your data set, and also a boatload of differing opinions on why and how you should further filter your SNP set! Some filters you might consider:
* overall sequencing depth i.e. chucking out low depth loci. This might reduce the likelihood of calling the wrong genotype at a locus because of low depth (e.g. hard to call a heterozygote when you only have one read at a locus!), but 

If you are interested in any of these further filtering steps, I'd highly encourage you to check out the following tutorial, which walks through several of these steps:
http://www.ddocent.com/filtering/

## Do I even need to filter at all?
Instead of filtering at the genotype level, other alternatives include using pipelines that can handle low depth data (e.g. [ANGSD](http://www.popgen.dk/angsd/index.php/ANGSD)) and conducting your analyses at a population level rather than individual level (e.g. [Genotype‐free estimation of allele frequencies reduces bias and improves demographic inference from RADSeq data](https://onlinelibrary-wiley-com.ezproxy.otago.ac.nz/doi/full/10.1111/1755-0998.12990))
