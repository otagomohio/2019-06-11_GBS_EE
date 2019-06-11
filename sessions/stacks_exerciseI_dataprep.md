# Exercise I. Data preparation    

**Developed by:** Julian Catchen, Nicolas Rochette

**Adapted by:** Ludovic Dutoit


## Datasets

• Dataset 1 (DS1) - This data set comprises just a small proportion of a lane of single-end
standard RAD data.

• Dataset 2 (DS2) - A fragment of a lane of paired-end RAD sequences that have been
double-digested with two restriction enzymes.
       You will use these first two data sets to become familiar with the structure of RAD
        sequences, as well as to become proficient with the pre-processing (i.e. cleaning
        and de-multiplexing) of data before alignment or assembly. DS1 consists of two samples of single-end RAD data from the         same set of samples, but constructed in two different libraries and sequenced independently.

## Part 1: Single-end reads

The first step in the analysis of all short-read sequencing data, including RAD-seq
data, is removing low quality sequences and separating out reads from different
samples that were individually barcoded. This **‘de-multiplexing’** serves to associate
reads with the different individuals or population samples from which they were
derived.

Before doing anything, open a text file in your favorite plain text editor e.g. Notepad on Windows/TextWrangler on Mac/Sublime on all platforms (avoid editors like MS Word that have fancy formatting, because they can format your text in a way that the command line can't understand). You will write your commands in your plain text editor and then paste them into the terminal. By saving these commands, you'll remember how and why you did things later today, but also in the future.

1. Let's organise our space, get comfortable moving around and copy our data :
    
    • Log in to NeSI/Mahuika, and from there, log in to our reserved machine by:
       
       ssh -Y ga-vl01
    
    • For each exercise, you will set up a directory structure on the remote server that will hold your data and the different          steps of your analysis. We will start by making the directory ```working``` in your working space, so let's `cd` (change directory) to your working location:

       cd /nesi/nobackup/nesi02659/users/<yourusername>

    • Once there, create the directory: ```/nesi/nobackup/nesi02659/users/<yourusername>/working``` (by using `mkdir working`) and then `cd` into `working`
        so we can create more subdirectories to hold our analyses. Be careful that you are reading and writing files to the appropriate directories within
        your hierarchy. You’ll be making many directories, so stay organized!
    
    •Each step of your analysis goes into the hierarchy of the workspace, and each step of  
        the analysis takes its input from one directory and places it into another directory, this
        is known as a ‘waterfall workspace’. We will name the directories in a way that
        correspond to each stage and that allow us to remember where they are. A well
        organized workspace makes analyses easier and prevents data from being overwritten.
    
    • First let's make a few directories. In ```working```, create a directory called ```dataprep``` to contain all the data        for this exercise. Inside that directory create two additional directories: ```lane1``` and ```samples```. 
    
    • As a check that we've set up our 'waterfall workspace' correctly, go back to your ```<username>``` directory (*hint*: `cd ..`) and use the `ls -R` (the `ls` command with the recursive flag). It should show you the following:
    
    ```
    working/:
    dataprep

    working/dataprep:
    lane1  samples

    working/dataprep/lane1:

    working/dataprep/samples:
    
    ```
    
    • Copy the data set 1 (DS1) to your ```lane1``` directory. The data set is in the file
       `/nesi/nobackup/nesi02659/source_data/clean/lane1.tar` 
       (*hint*: `cp /path/to/what/you/want/to/copy /destination/you/want/it/to/go`)          
    
    • `cd` to your ```lane1``` folder to extract/unzip the content of this ```tar``` archive. We realise that we have not told you how         to do so! But a quick look to a friendly search engine will show you how easy it is to find this kind of information           on basic bash commands (your instructors *still* spend a lot of time doing this themselves!).     

2. Have a look at what is there now. These gz-compressed fastq files have millions of reads in them, too many for you to examine in a
spreadsheet or word processor. However, we can examine the contents of the set of files in the terminal
(the ```less``` command may be of use).
    
    • You should see multiple different lines in each file: some starting with @, lines that only have +, lines with nucleotides (e.g. A, C, G, T), and lines with weird combinations of other ascii characters.
    
    • How does this FASTQ file format work? (*hint*: your friendly search engine may come in handy!)
    
    • How are quality scores for the reads encoded?
    
    • How could you tell by eye which type of encoding your data are using (i.e. PHRED33 or PHRED64)?
    

3. Let's have a closer look at this data. [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) is a common software to quality-control a fastq file. 

    • Let's run ```fastqc``` on one of our fastq files. To do so, you will first need to find fastqc. This program is available on the          server but it is not *loaded*. If all the softwares installed on the server were accessible at the same time it would          be one happy mess. Therefore, we load modules for specific programs when we actually need to use them.
    
    • To ```find``` and ```load``` our first module
       
       #To see all the modules
       module avail
                                       
       #The below command can help find a module
       module spider fastqc
                     
      That command should present you with some information about 
      modules that have a closely matching name.
      You can then load your module of interest, in our case FastQC
                     
       module load FastQC # Case-sensitive, so get the capitalization right!
       module list # View your loaded modules
       
     This list resets every time you log off Mahuika, so you will need to remember to reload the module(s) you need when you log in again.
     
    • Use the ```--help``` of ```fastqc``` to run it on any single fastq file of your choice (note, the name of the executable `fastqc` is all lower case...welcome to the club of frustration at capitalization of program names not matching up to their documentation!).
                         
    • Run `ls` in your lane1 directory: what outputs did fastqc create?
    
    • Let's try to copy the html file that fastqc created to your local computer in order to visualise it.
       
    • Open a new terminal window **without closing the current one** and stay on your local computer (i.e. do **not** login to mahuika). 
    
    • Check out [how to copy files](https://support.nesi.org.nz/hc/en-gb/articles/360000578455-File-Transfer-with-SCP). (*Hint:* To identify the path to the file on Mahuika,          use the ```pwd``` command in the lane1 directory on the terminal window that is logged into Mahuika...but don't forget to add the name of the file you want to copy to the end of this path).
       
    • Once you have this file on your local computer, just double-click on it to open it with your favorite browser.

    • What is this weird thing in the base-pair content from base 7 to 12-13?

      You probably noticed that not all of the data is high quality. In general, you will want
      to remove the lowest quality sequences from your data set before you proceed.
      However, the stringency of the filtering will depend on the final application. In
      general, higher stringency is needed for *de novo* assemblies as compared to
      alignments to a reference genome. However, low quality data can
      affect downstream analysis for *de novo* and reference-based approaches, producing false positives, such as errant SNP predictions.

4.We will use the Stacks’s program **process_radtags** to remove low quality sequences (also known as cleaning data) and to demultiplex our
samples. Take advantage of the Stacks [manual](http://catchenlab.life.illinois.edu/stacks/manual/) as well as the specific [manual page for
process_radtags](http://catchenlab.life.illinois.edu/stacks/manual/#procrad) on the Stacks website to find information         and examples. Do not run the commands you figure out just yet, but first follow through the points below:
    
  • Get back into your ```dataprep``` folder
    
  • It is time to load the ```stacks``` module to be able to access the ```process_radtags``` command. Find it, load it.
          
   • You will need to specify the set of barcodes used in the construction of the RAD library.
        Remember, each P1 adaptor in RAD has a particular DNA sequence (an inline
        barcode) that gets sequenced first, allowing data to be associated with samples such as
        individuals or populations.
    
   • Enter the following barcodes into a file called lane1_barcodes.txt in your dataprep
        directory (*Hint:* `nano`). 
        
        AAACGG AACGTT AACTGA AAGACG
        AAGCTA AATGAG ACAAGA ACAGCG
        ACATAC ACCATG ACCCCC ACTCTT
        ACTGGC AGCCAT AGCGCA
        
   Make sure you enter them in the [right format](http://catchenlab.life.illinois.edu/stacks/manual/#specbc) (e.g. one per line).
        Assign a sample name for each barcode. Normally, these sample names would
        correspond to the individuals used in a particular experiment (e.g. individual ID etc), but for this exercise, we
        will name the samples in a simple way, say indv_01, indv_02, etc. e.g.
        
        AAACGG       indv_01
        AACGTT       indv_02
    
   • Append the remaining barcodes for this lane of samples from `/nesi/nobackup/nesi02659/source_data/clean/lane1_barcodes.txt` (*Hint:* `cat` and `>>`)
    
   • Based on the barcode file, how many samples were multiplexed together in this
        RAD library? (*Hint:* count the lines.)
       
   • You will need to specify the restriction enzyme used to construct the library (SbfI), the
        directory of input files (the ```lane1``` directory), the list of barcodes, the output directory
        (```samples```), and specify that process_radtags ```clean, discard, and rescue reads.```
    
   • You should now be able to run the command from the ```dataprep``` directory. It will take a couple of minutes to run. 
   
      -   If you find that something is possibly missing from your process_radtags
                input, correct the error and give running process_radtags another try.

   • The process_radtags program will write a log file into the output directory. Have a look in there.
        Examine the log and answer the following questions:
    
    -   How many reads were retained?
    
    -   Of those discarded, what were the reasons? 
    
    -   In the process_radtags log file, what can the list of “sequences not recorded” tell
                you about the barcodes analyzed and about the sequencing quality in general?

##  Part 2: Paired-end reads

1. We will now work with the second data set. These data contain paired-end reads that
have been double-digested and dual barcoded. Each set of paired reads contains an
inline barcode on the first read, and an indexed barcode on both reads. These are
known as combinatorial barcodes as many unique combinations can be made from
pairs of barcodes. 
    
   • In ```working/dataprep```, create a directory called ```lane2``` to contain the raw data for this
        exercise and create the directory ```ddsamples``` to contain the cleaned output.
    
   •  Copy the dataset 2 (DS2):
        `/nesi/nobackup/nesi02659/source_data/clean/lane2.tar`
        into the ```lane2``` directory.
        
   •  Extract the lane2.tar file
    
2. Examine the contents of the pairs of files in the terminal again.
   
   • How are the FASTQ headers related between pairs of files?
   
   • Can you identify the indexed barcode in the FASTQ header?
    
3. We will again use the Stacks’ program process_radtags to clean and demultiplex
our samples.
   
   • Get back into the ```dataprep``` folder
   
   • You will need to specify the set of barcode pairs used in the construction of the RAD
        library.
   
   • Enter the following pairs of barcodes into a file called `lane2_barcodes.txt` in your dataprep
        directory (make sure you enter them in the [right format](http://catchenlab.life.illinois.edu/stacks/manual/#specbc) ). 
        
            AACCA    ATCACG 
            CATAT    ATCACG 
            GAGAT    ATCACG
            TACCG    ATCACG 
            AAGGA    CGATGT 
            CAACC    CGATGT
            GACAC    CGATGT 
            TACGT    CGATGT
        
   As we saw in the previous exercise, the sample names would normally coincide with your particular experimental design. Here, for simplicity, we can just use indv_01, indv_02, etc.
        
            AACCA    ATCACG indv_01 
            CATAT    ATCACG indv_02
           
   • Append the remaining barcodes for this lane of samples from the file:
        ```/nesi/nobackup/nesi02659/source_data/clean/lane2_barcodes.txt```
        to your barcodes file in your dataprep directory 
   
   • How many samples were multiplexed together in this RAD library? (*Hint:* count the lines.) 
   
   • Similarly to what we saw above, you will need to specify the two restriction enzymes used to construct the library
        (```NlaIII``` and ```MluCI```), the directory of input files (the lane2 directory), the list of
        barcodes, the output directory (ddsamples) and specify that process_radtags
        clean, discard, and rescue reads. Do not forget to specify the inline index and the fact that you are providing               paired-end reads. Your command should now be ready but don't run it just yet!
        
        

4.Running the commands directly on the screen is not common practice. You now are on ```ga-vl01``` which is a reserved amount of resources for this workshop and this iallows us to run pur command directly. On a day to day basis, you would be evolving on the *logi*n node (i.e. The place you reach when you login). All the [resources](https://support.nesi.org.nz/hc/en-gb/articles/360000204076-Mahuika-Slurm-Partitions) are tucked away from the login node. You generally run your commands as jobs that are *sent* to this [resources](https://support.nesi.org.nz/hc/en-gb/articles/360000204076-Mahuika-Slurm-Partitions), not on the login node itself. We will use this process_radtags command as a perfect example to run our first job.

   • copy an example jobfile into this directory. The example is at : '''/nesi/nobackup/nesi02659/source_data/example_job.sh'''

   • Open it with nano, have a look at what is there. As you can see, the first bit is parameters for the *job . system*            informing on who you are, which type of ressources you need and for how long

   •  Once you are done, save it and run it using 

```
sbatch examplejob.sh
```

   • You can check what is the status of your job using 

```
squeue -u <yourusername>
```

   • Once this place is empty, your job ran and what would have printed to your screen is into *prcoessrads.out*. You should also have recieved an email!

       
   
5. The process_radtags program has written a log file into the output directory.
        Examine the log and answer the following questions:
    
    -   What is the purpose of the four different output files for each set of barcodes?
    
    -   How many raw reads were there?
    
    -   How many reads were retained?
    

*Congratulations, you reached the end of Exercise 1. Have a breathe, help your fellow attendees, grab a coffee and we will be back shortly*

[Jump to exercise II](stacks_exerciseII_denovo)  
[Jump back to Stacks intro](stacks.md)  
[Jump back to the main workshop schedule](https://otagomohio.github.io/2019-06-11_GBS_EE/)
