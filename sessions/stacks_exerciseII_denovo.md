# Exercise II: de novo assembly of RAD tags without a genome

## Part 1: Your first stacks run!**


2. In the first part of the second exercise we will be constructing stacks in two separate
samples. These samples are from the same (anonymous) populations, however their
analysis results in two quite different outcomes.

3. In your ./working workspace, create a directory called ustacks to contain all the
data for this exercise. 

    *   Inside that directory, create two additional directories: ```samples```, and ```stacks```. To save time, we have                already cleaned and demultiplexed
this data and will start from the cleaned samples stage.
Copy data set 3 (DS3):
/opt/data/denovo/lib01_samp01.fq.gz
and
/opt/data/denovo/lib02_samp01.fq.gz
into the samples directory and decompress them.
4. While these data are from the same biological population, they have very different
characteristics when stacks are assembled from them. Your goal is to explore these two
samples and understand how they are interacting with ustacks.
5. First, using UNIX commands, determine how many reads are present in each sample
and the length of those reads.
6. Run ustacks on each sample, choosing the appropriate parameters for the length
and number of reads.
• Be sure to capture the output from ustacks in an external file. In the UNIX
exercises we learned to use the “>” symbol to redirect stdout to a file. In this
case you will need to redirect STDOUT and STDERR to a file, to do so, use
“&>” as the redirect symbol in your command.
Do not allow more than two mismatches between stacks for this exercise.
7. Examine the output from ustacks. What characteristics are different between the two
samples? What could potentially be causing these differences?
```

## Part 2: approach the parameter space**

1. In this second exercise we will be working on a subset of data from threespine
stickleback data from Oregon, on the
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
Without a reference genome, we
want to assemble the RAD loci and
examine population structure. However, before we can do that, we want to explore
the de novo parameter space in order to be confident that we are assembling our data
in an optimal way. As you have seen, stack formation is controlled by three main
parameters: m (the minimum read depth); M (the number of mismatches between
alleles) and n (the number of mismatches between loci in the catalog). Here, we will
optimize M for the stickleback data using a subset of the full dataset provided. After
this, we can use the optimal value we have found for M in the de novo exercise below
(part 3). We will be using the guidelines of parameter optimization as outlined in Paris
et al. (2017), and will create a ‘hockey stick’ plot to assess which value for M recovers
the highest number of new polymorphic loci (r80 loci).
2. In your ./working workspace, create a directory called denovo to contain all the
data for this exercise. Inside that directory, create two additional directories:
samples, and opt. To save time, we have already cleaned and demultiplexed this
data and will start from the cleaned samples stage. Inside the opt directory, create six
additional directories: M2, M3, M4, M5, M6 and M7. We have already prepared
the clean samples for this exercise.

    •   Unarchive dataset 2 (DS2):
        ```/opt/data/denovo/oregon_stickleback.tar```
        into the samples directory. The unarchived dataset contains 30 stickleback
        samples, and we will use 9 of them in this exercise:
            cs_1335.01, cs_1335.02, cs_1335.05, pcr_1211.04, pcr_1211.05,
            pcr_1211.06, stl_1274.33, stl_1274.35, stl_1274.37 Stickleback populations sampled from Oregon, USA in Catchen, et             al., 2013. Populations in red are sampled for this tutorial. ADRESS THE RED ISSUE

3. We will run the Stacks’ denovo_map.pl pipeline program, each time changing the value for
M. This program will run ustacks, cstacks, and sstacks on the individuals in our
study as well as the populations program.
*Once you get denovo_map.pl running, it will take approximately 10 minutes.*
    
    • Information on denovo_map.pl and its parameters can be found online:
        http://catchenlab.life.illnois.edu/stacks/comp/denovo_map.php
    
    • We want Stacks to only use the nine individuals in our parameter optimization. To
        specify this, create a file in the working directory called opt_popmap, using an editor.
        The file should be formatted like this:
            ```<sample file prefix><tab><population ID>```
    
    • Include samples in this file and specify that all individuals belong to one
        population. You must supply the population map to denovo_map.pl when you
        execute it for each parameter run.
    
    • To optimize for r80 loci you will need to tell denovo_map.pl to use an
        “Arbitrary command line option” so it will pass additional options to the
        populations (we want to use the -r parameter to filter for loci in 80% of the
        samples) program. Run iterations for M=2, M=3, M=4, M=5, M=6 and M=7.
        Change the corresponding value for n so that we follow the n=M rule.

4 . You should now see the denovo_map.pl output files in each directory (M2, M3,
M4, M5, M6 and M7). To obtain how many r80 loci were assembled for each
parameter run you will want to look at the populations.hapstats.tsv file.

    • Take a look at this file and use the Stacks manual to inform you on the data
        contained in each of the columns.

    • http://catchenlab.life.illinois.edu/stacks/manual/#files

    • What is the number of the first locus assembled for M2?

    • What is the number of the last locus assembled for M7?

    • Use UNIX to count how many loci were assembled for M2. Now use this code
        to count how many r80 loci were assembled for M3, M4, M5, M6 and M7. Record
        the number of r80 loci for each iteration of M.

    • Which iteration of M provided the highest number of r80 loci?

5. We now want to explore how many new r80 loci were found between each iteration
for M. Using the number of r80 loci from the populations.hapstats.tsv file, count
how many new loci were assembled with each iteration of M and record them in a
text file like so:
```
    M2/M3<tab>xxx
    M3/M4<tab>xxx
    M4/M5<tab>xxx

    M5/M6<tab>xxx
    M6/M7<tab>xxx
```

Save this file as ```r80_loci.tsv.```

6. Copy the Gnuplot script to the opt directory:
    ```/opt/data/denovo/hockey_stick.gnuplot```

    • Cat the file to see what it does.

7. Put the r80_loci.tsv file in the same directory as the hockey_stick.gnuplot
script.
    
    • Execute Gnuplot:
    ```
    % gnuplot < hockey_stick.gnuplot
    ```
    
    • Open the PDF to examine the hockey stick plot. Based on the plot and the
        number of r80 loci, which value for M do you think is most appropriate for the
        Oregon stickleback data?

## Part 3: Getting to opulation genetics analyses

1. In this third exercise we will now be working on the full set of threespine stickleback
data sampled from throughout Oregon, on the west coast of the United States. These
data consist of three populations: a coastal marine population, a costal freshwater, and
an inland river population.
2. Now that we have optimized the assembly parameters, we will assemble loci and
determine population structure using the Structure program. For more information on
the study this data originated with, see Catchen, et al. 2013.
3. In your ./working/denovo workspace, create a directory called stacks to contain
the assembled data for this exercise.
4. Run the Stacks’ denovo_map.pl pipeline program. This program will run ustacks,
cstacks, and sstacks on the individuals in our study as well as the populations
program.
*Once you get denovo_map.pl running, it will take approximately 30 minutes.*
    
    • Information on denovo_map.pl and its parameters can be found online:
    
    • http://catchenlab.life.illnois.edu/stacks/comp/denovo_map.php
    
    •We want Stacks to understand which individuals in our study belong to which
        population. To specify this, create a file in the working directory called popmap, using
        an editor. The file should be formatted like this:
        <sample file prefix><tab><population ID>
        Include all 30 samples in this file and specify which individuals belong to which
        populations. You must supply the population map to denovo_map.pl when you
        execute it.
    
    • There are three important parameters that must be specified to denovo_map.pl, the
        minimum stack depth, the distance allowed between stacks, and the distance allowed
        between catalog loci. Use the values we determined for these parameters in the
        previous exercise.
    
    • Also, you must set the stacks directory as the output, and use all the threads
        available on your instance.
    
    • Finally, specify the path to the directory containing your sample files. The
        denovo_map.pl program will read the sample names out of the population map, and
        look for them in the samples directory you specify.
    
    • Execute the Stacks pipeline.

5. Examine the Stacks log and output files when execution is complete.
    
    • After processing all the individual samples, denovo_map.pl will print a table
        containing the depth of coverage of each sample. Find this table in the log, what were
        the depths of coverage?
    
    • Examine the output of the populations program in the log.
    
    • How many loci were identified?
    
    • How many were filtered and for what reasons?
    
    • Familiarize yourself with the population genetics statistics produced by the
        populations component of stacks:
    
    • populations.sumstats.tsv, populations.sumstats_summary.tsv
    
    • What is the mean value of nucleotide diversity (π) and FIS for each of the three
        populations? [HINT: The less -S command may help you view these files easily.]
  
6. Our goal now is to export a subset of loci for analysis in Structure, which analyzes the
distribution of multi-locus genotypes within and among populations in a Bayesian
framework to make predictions about the most probable population of origin for each
individual. The assignment of each individual to a population is quantified in terms of
Bayesian posterior probabilities, and visualized via a plot of posterior probabilities for
each individual and population. A key user defined parameter is the hypothesized
number of populations of origin which is represented by k. Sometimes the value of k is
clear from from the biology, but more often a range of potential k-values must be
explored and evaluated using a variety of likelihood based approaches to decide upon
the ultimate k. In the interest of time we won’t be exploring different values of k here,
but this will be a key step in any data analysis. In addition, at the moment Structure
can only handle a small number of loci because of the MCMC algorithms involved in
the Bayesian computations, usually many fewer than are generated in a typical RAD
data set. We therefore want to randomly choose a random subset of loci that are well
represented in our three populations. Nonetheless, this random subset contains more
than enough information to define population structure.

    • The final stage of the denovo_map.pl pipeline is to run the populations program to
        calculate population genetic statistics for our data. We want to execute this program by
        hand again, specifying filters that will give us only the most well represented loci.

    • Run populations again, specifying that loci must be present in at least 80% of
        individuals in all three populations. You will have to tell populations where to
        find the output of the Stacks pipeline (this should be in the stacks output
        directory).

    • One final detail: Structure assumes that each SNP locus is independent, so we
        don’t want to output multiple SNPs from the same RAD locus, since they are not
        independent but are in linkage blocks within each RAD tag. We can achieve this
        behavior by specifying the --write_single_snp parameter to populations.

7. Now we want to select 1,000 loci randomly from the results and save these loci into a
file. We can easily do this using the shell given a list of catalog IDs output in the
previous step. The populations.sumstats.tsv file gives a list of all polymorphic
loci. Use the ```zcat, grep, cut, sort, uniq, shuf, and head``` commands to generate a
list of 1000 random loci. Save this list of loci as a whitelist, that we can feed back into
populations. This operation can be done in a single shell command. ADD  A LINK TO DESCRIPTION OF THOSE COMMANDS

8. Now execute populations again, this time feeding back in the whitelist you just
generated. This will cause populations to only process the loci in the whitelist.
Specify that a Structure output file be included this time and again insist that only a
single SNP is output from each RAD locus. Finally, you will need to again specify the
population map that you generated above to populations so that this information is
passed into the Structure output file.
9. Create a new directory called structure and copy the Structure output file that
Stacks generated to this directory.
    
    • Edit the Structure output file to remove the comment (first line in the file, starts with
        “#”).
    • You may need to edit your Structure output file to change the alphanumeric
        population names to be numbers. This can be done using sed.
    • The parameters to run Structure (including a value of k=3) have already been
        prepared, you can find them here:
            /opt/data/denovo/mainparams
        and
            /opt/data/denovo/extraparams
     • Copy them into your structure directory as well.
10. Execute Structure, saving the data into this new directory:
    ```structure > populations.structure.console```
[A common STRUCTURE error happens when your population output contains less
than 1000 loci. You may need to adjust the number of loci in the mainparams file to
match your exact Stacks output.]

11. You will need to download the populations.structure.console and
populations.structure.out_f files from the cluster!!!. You can then load them into
the graphical interface for Structure on your local computer. Select the “File” menu
and then “Load structure results…” to load the Structure output. Choose the “Barplot”
menu and then “Show”.
    
    • *Are the three Oregon threespine stickleback populations related to one another? How
        can you tell?*


ADD PCA EXERCISE
