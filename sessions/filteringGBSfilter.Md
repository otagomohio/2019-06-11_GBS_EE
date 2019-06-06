# Filtering your SNPs
**Developed by:** Alana Alexander

## Using GBS_SNP_filter  

***

#### Getting the scripts for GBS_SNP_filter
[GBS_SNP_filter](https://github.com/laninsky/GBS_SNP_filter) is github repository. To get it on to the computer we will use `git clone`. First, make sure you are in your working directory: `/nesi/project/nesi02659/users/<yourusername>` then...
```
git clone https://github.com/laninsky/GBS_SNP_filter.git
```
If we run a `ls` we should now see a folder called `GBS_SNP_filter` - this folder has all the scripts from the GBS_SNP_filter github repository.  

***

#### Loading required modules
[GBS_SNP_filter](https://github.com/laninsky/GBS_SNP_filter) requires some dependencies (other programs it needs to run), namely [VCFtools](https://vcftools.github.io/index.html), [PLINK](https://www.cog-genomics.org/plink/2.0/), and [R](https://www.r-project.org/). Luckily, these are installed on Mahuika already! We load them using the `modules` command:
```
module load VCFtools
module load PLINK
module load R
```
When you are working on other projects on Mahuika/NeSI, you can see what other modules are available to support your analyses by `module avail`, but VCFtools, PLINK and R are all we need for GBS_SNP_filter.  

***

#### Getting together the files we need to run GBS_SNP_filter
**vcf file**:First up, we need the vcf file we want to filter! For this, we will use the `populations.snps.vcf` file we created for the stickleback data in our [2nd STACKS exercise](https://otagomohio.github.io/2019-06-11_GBS_EE/sessions/stacks_exerciseII_denovo.html). Let's copy that into the GBS_SNP_filter folder:
```
cp /path/to/populations.snps.vcf /path/to/GBS_SNP_filter
```

**popmap.txt file**: The next thing we need is a popmap.txt file. This file (also described [here](https://github.com/laninsky/GBS_SNP_filter#popmaptxt)) has sample names (exactly the same as they appear in the populations.snps.vcf file) in the left hand column, and the population they map to on the right (separated by white space) e.g.
```
cs_1335.01 csl
cs_1335.02 csl
cs_1335.05 csl
pcr_1211.04 pcr
pcr_1211.05 pcr
pcr_1211.06 pcr
stl_1274.33 stl
stl_1274.35 stl
stl_1274.37 stl
```
We can create this file in nano:
```
nano popmap.txt
```
(remember to get out of nano use Ctrl+O to write the file, and then Ctrl+X to exit it)

**GBS_SNP_filter.txt**: The final file we need is GBS_SNP_filter.txt. This eight line long file contains the options that we want to use to filter our SNPs. The [GBS_SNP_filter](https://github.com/laninsky/GBS_SNP_filter#gbs_snp_filtertxt) repository has a lot of background on some of the options, but briefly:
1. the name of the vcf file (in our case, populations.snps.vcf)
2. the SNP missingness threshold (e.g. 0.85 = SNP needs to be found in 85% or more of samples) 
3. the sample missingness threshold (e.g. 0.9 = a sample can have up to 90% missing data before it is removed from the dataset)
4. the p-value used for determining whether something is out of HWE (e.g. 0.05, larger values will remove more loci, smaller values less)
5. the r^2 cut-off used for determining whether loci are in LD with each other (e.g. 0.5, smaller values will remove more loci, larger values less)
6. the number of populations that a locus has to be out of HWE/in LD across in before that locus is discarded
7. the column header in the vcf file that has the locus ID
8. the locus ID regex pattern (we don't have to worry about this for our example, but we do need to leave a blank line here).

Let's start off with the following info in our GBS_SNP_filter.txt file. After our first run we can play around with this to see how it affects our results (and see whether we can break [GBS_SNP_filter](https://github.com/laninsky/GBS_SNP_filter) by choosing some crazy values while we are at it!):
```
populations.snps.vcf
0.85
0.9
0.05
0.5
3
#CHROM

```



***

#### Running GBS_SNP_filter



* Bi-allelic variants 
* One SNP per locus
* SNPs that have genotypes across most of the individuals (i.e. completeness)
* Individuals that have genotypes across most of the SNPs (i.e. filtering out individuals with high levels of missing data)
* SNPs in Hardy Weinberg Equilibrium (LWE)
* Unlinked SNPs (based on LD) 

If you want more detail that's going on in each step, please check out the [detailed workflow](https://github.com/laninsky/GBS_SNP_filter#detailed-workflow).

## What if I want to filter on other stuff?
https://otagomohio.github.io/2019-06-11_GBS_EE/sessions/furtherfiltering.html

---
[Jump back to filtering SNPs intro](https://otagomohio.github.io/2019-06-11_GBS_EE/sessions/filteringSNPs.html)  
[Jump back to main workshop schedule](https://otagomohio.github.io/2019-06-11_GBS_EE/)
