# Filtering your SNPs
**Developed by:** Alana Alexander

## Using GBS_SNP_filter
#### Getting the scripts for GBS_SNP_filter
[GBS_SNP_filter](https://github.com/laninsky/GBS_SNP_filter) is github repository. To get it on to the computer we will use `git clone`. First, make sure you are in your working directory: `/nesi/project/nesi02659/users/<yourusername>` then...
```
git clone https://github.com/laninsky/GBS_SNP_filter.git
```
If we run a `ls` we should now see a folder called `GBS_SNP_filter` - this folder has all the scripts from the GBS_SNP_filter github repository.

#### Loading required modules
[GBS_SNP_filter](https://github.com/laninsky/GBS_SNP_filter) requires some dependencies (other programs it needs to run), namely [VCFtools](https://vcftools.github.io/index.html), [PLINK](https://www.cog-genomics.org/plink/2.0/), and [R](https://www.r-project.org/). Luckily, these are installed on Mahuika already! We load them using the `modules` command:
```
module load VCFtools
module load PLINK
module load R
```
When you are working on other projects on Mahuika/NeSI, you can see what other modules are available to support your analyses by `module avail`, but VCFtools, PLINK and R are all we need for GBS_SNP_filter.


cs_1335.01, cs_1335.02, cs_1335.05, pcr_1211.04, pcr_1211.05,
            pcr_1211.06, stl_1274.33, stl_1274.35, stl_1274.37


## What if I want to filter on other stuff?
https://otagomohio.github.io/2019-06-11_GBS_EE/sessions/furtherfiltering.html

---
[Jump back to filtering SNPs intro](https://otagomohio.github.io/2019-06-11_GBS_EE/sessions/filteringSNPs.html)  
[Jump back to main workshop schedule](https://otagomohio.github.io/2019-06-11_GBS_EE/)
