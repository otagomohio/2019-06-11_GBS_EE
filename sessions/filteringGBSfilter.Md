# Filtering your SNPs
**Developed by:** Alana Alexander

## Using GBS_SNP_filter
---
#### Getting the scripts for GBS_SNP_filter
[GBS_SNP_filter](https://github.com/laninsky/GBS_SNP_filter) is github repository. To get it on to the computer we will use `git clone`. First, make sure you are in your working directory: `/nesi/project/nesi02659/users/<yourusername>` then...
```
git clone https://github.com/laninsky/GBS_SNP_filter.git
```
If we run a `ls` we should now see a folder called `GBS_SNP_filter` - this folder has all the scripts from the GBS_SNP_filter github repository.
---
#### Loading required modules
[GBS_SNP_filter](https://github.com/laninsky/GBS_SNP_filter) requires some dependencies (other programs it needs to run), namely [VCFtools](https://vcftools.github.io/index.html), [PLINK](https://www.cog-genomics.org/plink/2.0/), and [R](https://www.r-project.org/). Luckily, these are installed on Mahuika already! We load them using the `modules` command:
```
module load VCFtools
module load PLINK
module load R
```
When you are working on other projects on Mahuika/NeSI, you can see what other modules are available to support your analyses by `module avail`, but VCFtools, PLINK and R are all we need for GBS_SNP_filter.
---
#### Getting together the files we need to run GBS_SNP_filter
**vcf file**:First up, we need the vcf file we want to filter! For this, we will use the `populations.snps.vcf` file we created for the stickleback data in our [2nd STACKS exercise](https://otagomohio.github.io/2019-06-11_GBS_EE/sessions/stacks_exerciseII_denovo.html). Let's copy that into the GBS_SNP_filter folder:
```
cp /path/to/populations.snps.vcf /path/to/GBS_SNP_filter
```

**popmap.txt file**: The next thing we need is a popmap.txt file. This file (also described [here](https://github.com/laninsky/GBS_SNP_filter#popmaptxt)) has sample names (exactly the same as they appear in the populations.snps.vcf file) in the left hand column, and the population they map to on the right (separated by white space). We can create this file in nano:
```
nano popmap.txt
```
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
(remember to get out of nano use Ctrl+O to write the file, and then Ctrl+X to exit it)

**GBS_SNP_filter.txt**: The final file we need is GBS_SNP_filter.txt. This file contains the options that we want to use to filter our SNPs. The [GBS_SNP_filter](https://github.com/laninsky/GBS_SNP_filter#gbs_snp_filtertxt) repository has a lot of background on thi



On the first line you need to give the name of your original vcf file that will be processed. On the second line you should give the proportion of samples that has to be equalled or exceeded for a SNP to be retained in the dataset (e.g 0.85 = a SNP needs to be found in 85% or more of total samples to be retained). On the third line you need to give the proportion of missing loci that will be tolerated for individual samples before they will be removed from the dataset (e.g. 0.9 = a sample can have up to 90% missing data before it is removed from the dataset). On the fourth line you need to give the p-value cut-off for determining whether a locus is out of HWE within a population. On the fifth line you need to give the r^2 cut-off for determining whether SNPs are in LD with each other within a population. On the sixth line you need to give the number of populations a locus has to be out of HWE/in LD across in before that locus is discarded. On the seventh line you need to give the column header for where the locus id you wish to use resides. 






---
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
