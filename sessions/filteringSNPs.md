** Under construction **

# Filtering your SNPs

## Background
Congratulations! Over the last day you've learned how to use STACKS to generate a vcf file (and other file formats) containing variable SNPs derived from GBS/RADseq data. By tweaking some of the parameters of the STACKS pipeline (particularly m - the minimum read depth; M - the number of mismatches between alleles; and n - the number of mismatches between loci in the catalog), we can make it less likely that we've included problematic loci (e.g. paralogous loci smushed into one "super stack"). Other pipelines like [ipyrad](https://ipyrad.readthedocs.io/) also have similar parameters that can be tweaked.

Despite this, it is likely that a few problematic loci *are* going to sneak through into our dataset. These might include some paralogous loci, which will be more heterozygous than expected because of fixed differences between the different 'true' loci that have been co-assembled into one paralogous locus. It might also include loci that have null alleles, that is, where the restriction enzyme site for one allele has been eroded by a mutation. This can make individuals look homozoygous at that site (and that locus to look more homozygous than you might expect in general), even though they are truly heterozygous. The impact of these problematic loci will depend on what you are using your data for, but null alleles can be particularly problematic for parentage analysis, because if an offspring inherits one of the null alleles from a parent there will be no data at that locus to suggest that those two relatives are linked.

## Filtering out loci that are out of HWE
Fortunately, we can screen for loci that are out of [Hardy-Weinberg Equilibrium](https://en.wikipedia.org/wiki/Hardy%E2%80%93Weinberg_principle) i.e. loci that appear to be too heterozygous/homozygous based on allele frequencies in the population. One problem we can face, however, is that a lot of the programs (e.g. []() ) that filter out loci that aren't in HWE assume we've only got a single population in our dataset. Why is this a problem? Welp, loci with null alleles and paralogous loci are not the only reasons you can be out of HWE. One big reason is [population structure](https://en.wikipedia.org/wiki/Wahlund_effect)! That's right! If we have multiple populations present in our data set, and we filter on HWE, then we might actually be tipping out the SNPs that are the most informatic about population structure!




do downstream filtering based on things like Hardy-Weinberg Disequlibrium, and Linkage Disequlibrium


cs_1335.01, cs_1335.02, cs_1335.05, pcr_1211.04, pcr_1211.05,
            pcr_1211.06, stl_1274.33, stl_1274.35, stl_1274.37
