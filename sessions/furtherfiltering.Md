# Filtering your SNPs
**Developed by:** Alana Alexander

## Other filtering parameters
There are a boat load of additional filters/options you could apply to your data set, and also a boatload of differing opinions on why and whether you should further filter your SNP set! Some filters you might consider (credit to the creators of [ipyrad](https://ipyrad.readthedocs.io/faq.html#tuning-assembly-parameters) for references for these):
* overall sequencing depth (i.e. chucking out loci covered by too few reads). This might reduce the likelihood of calling the wrong genotype at a locus because of low depth (e.g. hard to call a heterozygote when you only have one read at a locus!), but also see 'Do I even need to filter at all?', below.
* to reference genome or not to reference genome. For some folks, this will be an easy one to answer. If you don't have a reference genome for your organism, you won't be able to make use of it! However, evidence suggests if you do have a reference genome available, that will assist with your analyses (see: [Bioinformatic processing of RAD‐seq data dramatically impacts downstream population genetic inference](https://academic.oup.com/sysbio/article/65/3/357/2468879))
* a MAF (minor allele frequency) filter. Recent research suggests for Structure/PCA analyses, that singleton SNPs being filtered out increases the ability to detect population structure, but that more stringent MAFs might actually reduce the ability to detect population structure ([Minor allele frequency thresholds strongly affect population structure inference with genomic data sets](https://onlinelibrary.wiley.com/doi/abs/10.1111/1755-0998.12995)). For coalescent analyses (e.g. [CubSFS](https://github.com/blwaltoft/CubSFS), [dadi](https://bitbucket.org/gutenkunstlab/dadi/src/master/), [fastsimcoal2](http://cmpg.unibe.ch/software/fastsimcoal2/)) avoid filtering on MAF - the low frequency variants in a population are hugely informative about demographic processes impacting the population!

If you are interested in any of these further filtering steps, I'd highly encourage you to check out [this tutorial](http://www.ddocent.com/filtering/) from the [dDocent](http://www.ddocent.com) folks for using VCFtools, which walks through several of these filtering steps (any filtering steps that aren't covered in this tutorial, will be covered in the extensive VCFtools [documentation](https://vcftools.github.io/man_latest.html))

## Do I even need to filter at all?
Instead of filtering at the genotype level, other alternatives include using pipelines that can handle and calculate population-level statistics for low depth data at a population level rather than individual level (e.g. [ANGSD](http://www.popgen.dk/angsd/index.php/ANGSD), [Genotype‐free estimation of allele frequencies reduces bias and improves demographic inference from RADSeq data](https://onlinelibrary-wiley-com.ezproxy.otago.ac.nz/doi/full/10.1111/1755-0998.12990)), or incorporate the biases from low-depth in individual level calculations e.g. [KGD](https://github.com/AgResearch/KGD).

---
[Jump back to using GBS filter](https://otagomohio.github.io/2019-06-11_GBS_EE/sessions/filteringGBSfilter.html)  
[Jump back to filtering SNPs intro](https://otagomohio.github.io/2019-06-11_GBS_EE/sessions/filteringSNPs.html)  
[Jump back to main workshop schedule](https://otagomohio.github.io/2019-06-11_GBS_EE/)
