# Exercise II: de novo assembly of RAD tags without a genome

**Developed by:** Julian Catchen, Nicolas Rochette

**Adapted by:** Ludovic Dutoit

## Part 1: Running Stacks denovo

In this first exercise, we will be working on a subset of data from threespine
stickleback data from Oregon (Catchen et al, [2013](https://onlinelibrary.wiley.com/doi/10.1111/mec.12330)), on the
west coast of the United States.
These stickleback can be found in a
number of habitats from costal
marine and freshwater habitats, to
inland river habitats, to high
mountain lakes in the interior of
Oregon. We want to understand how
these populations relate to one
another and in this exercise, you will
examine three of these populations:
a coastal marine population, a costal
freshwater, and an inland river
population.

Without access to a reference genome, we
want to assemble the RAD loci and
examine population structure. However, before we can do that, we want to explore
the *de novo* parameter space in order to be confident that we are assembling our data
in an optimal way. Stack formation is controlled by three main
parameters: m (the minimum read depth); M (the number of mismatches between
alleles) and n (the number of mismatches between loci in the catalog). Here, we will
optimize M for the stickleback data using a subset of the full dataset provided. After
this, we can use the optimal value we have found for M in the *de novo* exercise below. We will be using the guidelines of parameter optimization as outlined in [Paris
et al. (2017)](https://besjournals.onlinelibrary.wiley.com/doi/epdf/10.1111/2041-210X.12775) to assess which value for M recovers the highest number of new polymorphic loci found across 80% of the individuals (r80 loci).

This approach is described more in [Paris et al. (2017)](https://besjournals.onlinelibrary.wiley.com/doi/epdf/10.1111/2041-210X.12775):
*"After putative alleles are formed, stacks performs a search to match alleles together into putative loci. This search is governed by the M parameter, which controls for the maximum number of mismatches allowed between putative alleles [...] Correctly setting **M** requires a balance – set it too low and alleles from the same locus will not collapse, set it too high and paralogous or repetitive loci will incorrectly merge together."*

1. Go to your ```/nesi/nobackup/nesi02659/<yourusername>/working``` workspace, create a directory called ```denovo``` to contain all the
data for this exercise. *Inside* that directory, create two additional directories:
```samples```, and ```opt```. 

   To save time, we have already cleaned and demultiplexed this
   data and will start from the cleaned samples stage. Inside the opt directory, create four
   additional directories: ```M4```, ```M5```, ```M6```   and ```M7```. 

   • Go to ```samples``` directory. Copy the dataset below in the ```samples``` directory: ```/nesi/nobackup/nesi02659/source_data/denovo/oregon_stickleback.tar```
    
   • Extract it. The unarchived dataset contains 30 stickleback
     samples (Catchen, et al., [2013](https://onlinelibrary.wiley.com/doi/10.1111/mec.12330)), but we will use only 3 of them (`cs_1335.01`,  `pcr_1211.04`, `stl_1274.33`) in this first part of the exercise as we will run denovo_map.pl just a few times for optimisation. 
     
2. We will run the Stacks’ ```denovo_map.pl``` pipeline program, each time changing the value for
```M```. `denovo_map.pl` will run ustacks, cstacks, and sstacks on the individuals in our
study as well as the ```population``` program. The set of instructions below should help you build your command.
    
   • Get back into the ```opt``` folder. (*Hint*:  Use```pwd``` if you don't know where you are anymore.
    
   • Load the ```Stacks``` module
    
   • Information on denovo_map.pl and its parameters can be found [online]( http://catchenlab.life.illinois.edu/stacks/comp/denovo_map.php)
    
   • We want Stacks to only use the 3 individuals in our parameter optimization (cs_1335.01,  pcr_1211.04, stl_1274.33).
   
   • To specify this, create a file in the opt directory called ```opt_popmap.txt```, using an editor.
        The file should be formatted like [indicated in the manual](http://catchenlab.life.illinois.edu/stacks/manual/#popmap).        
         Note: do not include the extension ```.fa.gz``` in the sample name.
    
   • Include samples in this file and **specify that all individuals belong to one
        single population** (e.g. give them all the same population code). You will need to supply this        ```opt_popmap.txt```population map to [denovo_map.pl](http://catchenlab.life.illinois.edu/stacks/comp/denovo_map.php) when you
        execute it for each parameter run.
    
   • To optimize for r80 loci you will need to tell denovo_map.pl to use the '''-r''' parameter to filter for loci in 80% of the
        samples) program. We will keep ```m``` at 3. Initially, we will set M to 4. We will also follow the general rule of ```M = n``` and we will tell [denovo_map.pl](http://catchenlab.life.illinois.edu/stacks/comp/denovo_map.php) to output to the M4 folder.
        
   • With this information, you should be able to launch the M4 run now. It will take a couple of minutes.
       
3. Once done, you should now see the denovo_map.pl output files in the directory M4.

    • After M4 is completed, do the same process for M = 5 through M = 7 (this should take around 10min total).    
    
    • While you are running M5 through m7, open a *new command window*, login to Mahuika and re-access       the reserved machine ```ssh -Y ga-vl01```. Then go to your ```working/denovo``` folder so that you can keep working while M5 through M7 are running.
    
    • To see how many r80 loci were assembled for each parameter run you will want to start looking at the                        ```populations.hapstats.tsv``` file using the [Stacks manual](http://catchenlab.life.illinois.edu/stacks/manual/#files)
    to inform you on the data
    contained in each of the columns. 

    • What is the number of the first locus assembled for M4?

    • What is the number of the last locus assembled for M4?
    
    • How many loci in total? (*Hint:* count the lines)
        
    • Using this technique, how many loci were assembled for M5 to M7 once they finish running?
    
    • Which iteration of M provided the highest number of r80 loci?   

You should now be able to choose your optimised parameters according to the Paris et al. (2017) method! ("select those values which maximize the number of polymorphic loci found in 80% of the individuals in your study")

## Part 2: Getting to population genetics analyses

1. In this second exercise we will now be working on the full set of threespine stickleback
data sampled from throughout Oregon, on the west coast of the United States. These
data consist of three populations: a coastal marine population, a coastal freshwater, and
an inland river population.
2. Now that we have optimized the assembly parameters, we will assemble loci and
determine population structure using the Structure program. For more information on
the background of this study, see Catchen, et al. 2013.
3. In your ```./working/denovo``` workspace, create a directory called stacks to contain
the assembled data for this exercise.
4. Run Stacks’ denovo_map.pl pipeline program according to the following set of instructions:
    
    • Get back in the ```working/denovo``` folder.
    
    • As for the previous exercise, information on denovo_map.pl and its parameters can be found [online](http://catchenlab.life.illinois.edu/stacks/comp/denovo_map.php)
    
    •We want Stacks to understand which individuals in our study belong to which
        population. To specify this, create a file ```complete_popmap.txt``` in the denovo directory called popmap, using
        an editor. The file should be formatted in 2 columns like [this](http://catchenlab.life.illinois.edu/stacks/manual/#popmap). Include all 30 samples in this file and specify which individuals            belong to which populations. You must supply the population map to denovo_map.pl when you execute it. You could for             example use ```ls -1 *fa.gz``` to see all the samples in a list before adding the populations. Add the populations as simple integers (i.e. 1, 2 and 3) to make it easier to use the program ```Structure``` that we will run downstream.
    
    • There are three important parameters that must be specified to denovo_map.pl, the
        minimum stack depth (`m`), the distance allowed between stacks (`M`), and the distance allowed
        between catalog loci (`n`). Use the values we determined for these parameters in the
        previous exercise, but do not restrict the loci to just those found in 80% like we did in the opt runs.
    
    • Also, you must set the stacks directory as the output, and use 6 threads (6 CPUs so your analysis finishes faster than 1!).
        
    • Finally, specify the path to the directory containing your sample files. The
        denovo_map.pl program will read the sample names out of the population map, and
        look for them in the samples directory you specify.
    
    • Execute the Stacks pipeline. That should take approximately 30min, ideal time for a break!
    
5. Examine the Stacks log and output files when execution is complete.
    
    • After processing all the individual samples through ustacks and before creating the catalog with cstacks, denovo_map.pl            will print a [table containing the depth of coverage](http://catchenlab.life.illinois.edu/stacks/manual/#cov) of       each sample. Find this table in the log, what were
        the depths of coverage?
    
    • Examine the output of the populations program in the log.
    
    • How many loci were identified?
    
    • How many were filtered and for what reasons?
    
    • Familiarize yourself with the population genetics statistics produced by the
        populations component of stacks populations.sumstats_summary.tsv
    
    • What is the mean value of nucleotide diversity (π) and FIS for each of the three
        populations? [HINT: The less -S command may help you view these files easily by avoiding the wrapping]

## Part 3: Populations genetics analyses from Stacks

Our goal now is to export a subset of loci for analysis in Structure, which analyzes the
distribution of multi-locus genotypes within and among populations in a Bayesian
framework to make predictions about the most probable population of origin for each
individual. The assignment of each individual to a population is quantified in terms of
Bayesian posterior probabilities, and visualized via a plot of posterior probabilities for
each individual and population.

A key user defined parameter is the hypothesized
number of populations of origin which is represented by *K*. Sometimes the value of *K* is
clear from from the biology, but more often a range of potential *K*-values must be
explored and evaluated using a variety of likelihood based approaches to decide upon
the ultimate *K*. In the interest of time we won’t be exploring different values of *K* here,
but this will be a key step for your own data sets. In addition, at the moment Structure
will take a long time to run on the number of loci generated in a typical RAD data set because of the MCMC algorithms involved in the Bayesian computations. We therefore want to randomly choose a random subset of loci that are well
represented in our three populations. Nonetheless, this random subset contains more
than enough information to define population structure:

 The final stage of the denovo_map.pl pipeline is to run the populations program. We want to execute just populations, rather than the full denovo_map.pl pipeline, to specify filters that will give us only the most well represented loci. [Populations](http://catchenlab.life.illinois.edu/stacks/comp/populations.php) is a very useful pice of software both for filtering and for outputting population genetics. It can work with non-stacks generated data too.

   • Since we won't be able to use all loci for our quick downstream analysis today, we will run [populations](http://catchenlab.life.illinois.edu/stacks/comp/populations.php) again, specifying that loci must be present in at least 80% of
        individuals in all three populations to cut down on the total number of loci. You will have to tell populations where to
        find the output of the Stacks pipeline (this should be in the stacks output
        directory). 
    
   • Make sure to output a structure file! Output a ```.vcf``` file as well. We will be combing back that `.vcf` file later today [later](https://otagomohio.github.io/2019-06-11_GBS_EE/sessions/filteringSNPs.html).

   • One final detail: Structure assumes that each SNP locus is independent, so we
        don’t want to output multiple SNPs from the same RAD locus, since they are not
        independent but are in linkage blocks within each RAD tag. We can achieve this
           behavior by specifying the `--write_single_snp` parameter to populations.

7. Now we want to select 1,000 loci randomly from the results and save these loci into a
file. We can easily do this using the shell given a list of catalog IDs output in the
previous step. The populations.sumstats.tsv file gives a list of all polymorphic
loci. Use the ```cat, grep, cut, sort, uniq, shuf, and head``` commands to generate a
list of 1000 random loci. Save this list of loci as  ```whitelist.txt```, that we can feed back into
populations. This operation can be done in a single shell command. That sounds challenging, but the instructions
below should help you create one command with several pipes to create that whitelist.txt. Create that command step by step:

   • First, use ``` cat``` to concatenante  ```stacks/populations.sumstats.tsv```.
    
   • Then, use ```grep``` with ```-v```  to exclude all headers (i.e. excluding "#")
    
   •  Select the first column with ```cut -f 1``` 
     
   •  Then use `sort` before using `uniq`. `uniq` will collapse succesive identical lines into single lines, so that you have one            line per locus. Lucky us, those two commands don't require any arguments.
   
   • Now try adding ```shuf``` which will mix all these lines all over.
    
   • Select the first one thousand lines with head and put it all into whitelist.txt.
    
   •  You got this! If you are new to bash, I am sure that seemed impossible yesterday, so take a minute to congratulate               yourself on the progress made even if you required a little help!

8. Now execute populations again, this time feeding back in the whitelist you just
generated. This will cause populations to only process the loci in the ```whitelist.txt```.
Specify that a Structure output file be included this time and again insist that only a
single SNP is output from each RAD locus. Finally, you will need to again specify the
population map that you generated above to populations so that this information is
passed into the Structure output file. You might also want to output a vcf file: this format is handy for all kind of population genetics applications.

   •  We've run commands to generate the structure file several times, but how many structure files are there in the stacks directory? If you wanted to save several different vcf and structure files generated using different `populations` options, what would you have to do?

9. Create a new directory called ```structure``` within the denovo folder and copy the Structure output file that
Stacks generated to this directory. `cd` into your new structure directory.
    
   • Edit the Structure output file to remove the comment line (first line in the file, starts with
        “#”).  
   • The parameters to run Structure (with value of *K*=3) have already been
        prepared, you can find them here:
            `/nesi/nobackup/nesi02659/source_data/denovo/mainparams`
        and
            `/nesi/nobackup/nesi02659/source_data/denovo/extraparams`  
   • Copy them into your structure directory as well.  
     
10. So far, when we've gone to run programs, we've been able to use `module spider` to figure out the program name, and then `module load program_name` to get access to the program and run it. However, structure is not an available module on Mahuika. Instead, we've done a local installation of the progam into /```nesi/nobackup/nesi02659/source_data/structure```.  Run Structure:

```     
 /nesi/nobackup/nesi02659/source_data/structure
```  

The program should ive you some information as it runs. If the program immediately finishes, something has gone wrong!  Do a `less` on populations.structure.console. Do you see `WARNING! Probable error in the input file.`? In our mainparams file it says that we have 1000 loci, but due to filters, it is possible that the populations module of Stacks actually output less than the 1000 loci we requested in ```whitelist.txt```. In the output of ```populations.log``` in your stacks directory, how many variant sites remained after filtering? This is the number of loci actually contained in your structure file. You will need to adjust the number of loci in the mainparams file to
match this exact Stacks output.

11. You will need to download  [Structure with the graphical front end](https://web.stanford.edu/group/pritchardlab/structure_software/release_versions/v2.3.4/html/structure.html) and use `scp` to download the populations.structure.out_f [file from the cluster](https://support.nesi.org.nz/hc/en-gb/articles/360000578455-File-Transfer-with-SCP). You can then load this file into the graphical interface for Structure on your local computer. Select the ```File``` menu
and then ```Load structure results``` to load the Structure output. Choose the ```Barplot```
menu and then ```Show```.
    
    • Are the three Oregon threespine stickleback populations related to one another? How
        can you tell?
        
Congrats, you just finished our tutorial for denovo RAD-Seq. If you have plenty of time, you could try different parameters for the populations module of Stacks or familiarise yourself with the idea of a reference based approach: [ref_map.pl](http://catchenlab.life.illinois.edu/stacks/comp/ref_map.php). You could also play with your own data. Finally, you could use the ```vcf``` you generated into the ```stacks``` folder in the R package ```adegenet``` to create [other visualisations](http://adegenet.r-forge.r-project.org/files/tutorial-basics.pdf) if you are comfortable with ```R```

***

[Jump to filtering SNPs intro](https://otagomohio.github.io/2019-06-11_GBS_EE/sessions/filteringSNPs.html)  
[Jump back to Exercise I](stacks_exerciseI_dataprep)  
[Jump back to main workshop schedule](https://otagomohio.github.io/2019-06-11_GBS_EE/)
