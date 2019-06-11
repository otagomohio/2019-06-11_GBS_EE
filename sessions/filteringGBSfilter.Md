# Filtering your SNPs
**Developed by:** Alana Alexander

## Using GBS_SNP_filter  

***

### Getting the scripts for GBS_SNP_filter
[GBS_SNP_filter](https://github.com/laninsky/GBS_SNP_filter) is a github repository. To get it on to the computer we will use `git clone`. 

First, make sure you are in your working directory: `/nesi/nobackup/nesi02659/users/<yourusername>`. To clone the folder as it is on github, use:

```
git clone https://github.com/laninsky/GBS_SNP_filter.git
```

List the contents of your directory. You should now see a folder called `GBS_SNP_filter` - this folder has all the scripts from the ```GBS_SNP_filter``` github repository.  

***

### Loading required programs
[GBS_SNP_filter](https://github.com/laninsky/GBS_SNP_filter) requires some dependencies (other programs it needs to run), namely [VCFtools](http://vcftools.sourceforge.net/man_latest.html), [PLINK](https://www.cog-genomics.org/plink/2.0/), and [R](https://www.r-project.org/). Luckily, a working version of VCFtools and R are installed on Mahuika already! We load them using the `module load` command:
```
module load VCFtools
module load R
```

Remember, when you are working on other projects on Mahuika/NeSI, you can see what other modules are available to support your analyses by `module avail`, but VCFtools, PLINK and R are all we need for GBS_SNP_filter.  

The PLINK version on Mahuika has some conflicts with the other programs we are using, so I've downloaded a 'clean' version. When we recently ran another program that also doesn't have a module available, `structure`, we provided an absolute path so Mahuika knew where it was located. Here, we are going to show you a slightly different way to get Mahuika to find a locally installed program. To do this, we need to run a little bit of code to add the location where PLINK is to our $PATH. Your $PATH is a list of all the places the computer looks for programs to run. You can have a look at your path by running:

```
echo $PATH
```

When you run any piece of software, the computer looks into all the places mentioned in your $PATH. Even the `ls` command that you just ran is somewhere on your computer. You can find it by typing:

``` which ls ```

The ```plink``` executable is located in the `source_data` folder, so we are adding this location on to the beginning of our $PATH:

```
export PATH=/nesi/nobackup/nesi02659/source_data:$PATH
```

You will now be able to access ```plink```

*Note*: If you log out of ```ga-vl01``` and log back again, you'll need to re-load these programs following the instructions above.

***

### Getting together the files we need to run GBS_SNP_filter
**vcf file**: First up, we need the vcf file we want to filter! For this, we will use the `populations.snps.vcf` file we created for the stickleback data in our [2nd STACKS exercise](https://otagomohio.github.io/2019-06-11_GBS_EE/sessions/stacks_exerciseII_denovo.html).

Let's copy that into the GBS_SNP_filter folder (e.g. if you are located in the `working` folder, 'above' GBS_SNP_filter:

```
cp ../working/denovo/stacks/populations.snps.vcf GBS_SNP_filter
```

Have a look at the ```vcf``` file  using ```less``` and try to understand its structure. You can use [this](https://en.wikipedia.org/wiki/Variant_Call_Format) to help. VCF is by far the most common way to store variant calls in population genetics, so take a bit of time to familiarise yourself with it.

**popmap.txt file**: The next thing we need is a ```popmap.txt``` file with one individual per line, with the sample name separated from the population code by whitespace (i.e. either a space or a tab): 
```
sample_name  population_code
```

Luckily we already created a popmap file recently! Copy it into the GBS_SNP_filter folder and name it popmap.txt (you can use ```mv``` or ```cp``` to rename it).

No matter what directory you are currently located in, it is now time to get into the ```GBS_SNP_filter``` folder.

```
cd GBS_SNP_filter
```


**GBS_SNP_filter.txt**: We have now put our ```vcf``` and our ```popmap``` file into the GBS_SNP_filter folder. The final file we need is ```GBS_SNP_filter.txt```. This eight line long file contains the options that we want to use to filter our SNPs. The [GBS_SNP_filter](https://github.com/laninsky/GBS_SNP_filter#gbs_snp_filtertxt) repository has a lot of background on some of the options, but briefly the lines should be as follows:
1. the name of the vcf file (in our case, populations.snps.vcf)
2. the SNP missingness threshold (e.g. 0.85 = SNP needs to be found in 85% or more of samples) 
3. the sample missingness threshold (e.g. 0.9 = a sample can have up to 90% missing data before it is removed from the dataset)
4. the p-value used for determining whether something is out of HWE (e.g. 0.05, larger values will remove more loci, smaller values less)
5. the r^2 cut-off used for determining whether loci are in LD with each other (e.g. 0.5, smaller values will remove more loci, larger values less)
6. the number of populations that a locus has to be out of HWE/in LD across in before that locus is discarded (e.g. 3, smaller values will remove more loci, larger values less)
7. the column header in the vcf file that has the locus ID (in our case, #CHROM)
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
We can create this file by `nano GBS_SNP_filter.txt` (don't forget the blank line on line 8!).

***

### Running GBS_SNP_filter
Alright, we are pretty much ready to run GBS_SNP_filter.txt! Our final checklist:
- [ ] We've used `git clone` to clone the GBS_SNP_filter github repository
- [ ] We've loaded the modules we need (VCFtools and R)
- [ ] We've edited the $PATH variable so Mahuika can find PLINK
- [ ] We've copied the vcf file into the GBS_SNP_filter folder
- [ ] We've created a popmap.txt and GBS_SNP_filter.txt file and placed them in the GBS_SNP_filter folder
- [ ] We are inside the GBS_SNP_filter folder

After doing all that, we are ready to run the filter by:
```
bash GBS_SNP_filter.sh
```

The script is going to go through the following steps:
* Filtering for bi-allelic variants 
* Filtering down to one SNP per locus
* Filtering out SNPs that don't pass the missingness filter
* Filtering out individuals with too much missing data
* Filtering out SNPs that are out of HWE in too many populations
* Filtering out SNPs that are in linkage across too many populations 

If you want more detail that's going on in each step, please check out the [detailed workflow](https://github.com/laninsky/GBS_SNP_filter#detailed-workflow).

Note: If you get the following message, it is [safe to ignore](https://github.com/laninsky/GBS_SNP_filter#troubleshooting):
```
Warning message:
Missing column names filled in: 'X8' [8] 
```

***

### How can a monitor how GBS_SNP_filter is going?
Although GBS_SNP_filter will print out some messages to screen, the real detail of how it is going is written out to a log file in the GBS_SNP_filter folder. To monitor the log while GBS_SNP_filter is running, we need to log in to Mahuika using a different terminal window, and then get to the bit of Mahuika we are running the analyses on by:
```
ssh -Y ga-vl01
```
After heading to our GBS_SNP_filter folder:
```
cd /nesi/nobackup/nesi02659/users/<yourusername>/GBS_SNP_filter
```
We can peek into our log file by:
```
less populations.snps.log
```
If we type `Shift+F` after opening the file using `less`, the log file will update when GBS_SNP_filter adds more info.

Alternatively, we can also monitor our job by using the `top` command. First, we have to get out of `less`. To do this we need to do `Ctrl+c` to interrupt `less` waiting for data, and then `q` to exit  `less`. To use top, we then simply type:
```
top
```
Can you see your user name and a process using a good whack of %CPU? If so, cool!

Once GBS_SNP_filter completes, a large number of files will be present. The final output vcf file will have ".ld.vcf" as a suffix, and the rest of the files are described [here](https://github.com/laninsky/GBS_SNP_filter#detailed-workflow). The log file will detail how many SNPs were filtered out at each step.
* How many SNPs were present in the final data set? 
* How many SNPs were filtered out at each step? 
* If some of the filters did not remove any SNPs, why do you think this might be?  

***

### Comparing different parameter choices
After GBS_SNP_filter completes, have a go tweaking the parameters and rerun it to see how it affects the number of SNPs retained. Keep line 1 (populations.snps.vcf), line 7 (#CHROM), and line 8 (blank line) the same, but play around with the other filters. How does this affect the number of SNPs left at the end? Are there any combinations that cause GBS_SNP_filter to fail? Why do you think that might be? The log can get a bit unwieldy after multiple runs, so it might be a good idea to note down the number of SNPs for each parameter combination on your desktop.

**Some known ways to make GBS_SNP_filter fail**:
* setting line 3 to extremely low values (i.e. allowing hardly any missing data for any individuals) - this causes the code to fail because no samples are left in the data set!
* setting line 6 to 0 (i.e. if any HWE/r^2 value occurs in any population, remove that locus!) - this causes the code to fail because no SNPs are left in the data set!

***

### What if I want to learn more about GBS_SNP_filter and/or filter on other stuff?
The [README](https://github.com/laninsky/GBS_SNP_filter) for GBS_SNP_filter provides additional detail on this set of scripts, and the repository also has further utility scripts for calculating multi-locus heterozygosity for your individuals, and observed/expected heterozygosity for your populations.

In addition, there are yet more potential filters you can use on your data, and other useful programs for further filtering of data that you should check out [here](https://otagomohio.github.io/2019-06-11_GBS_EE/sessions/furtherfiltering.html).

---

[Jump back to filtering SNPs intro](https://otagomohio.github.io/2019-06-11_GBS_EE/sessions/filteringSNPs.html)  
[Jump back to main workshop schedule](https://otagomohio.github.io/2019-06-11_GBS_EE/)
