# Exercise I. Data preparation    

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

Before doing anything, open a text file in your favorite text editor. You will write your commands in there and then paste them into the terminal. You want to remember how and why you did things later today but also in the future.

1. Let's organise our space, get comfortable moving around and copy our data :
    
    • If you have not done it yet, do not forget to log on our reserved machine
       ```ssh -Y ga-vl01```
    
    • For each exercise, you will set up a directory structure on the remote server that will hold your data and the different          steps of your analysis. We will start by making the directory ```working``` in your working space:
           ```/nesi/project/nesi02659/users/<yourusername>```
    
    • Create the directory: ```/nesi/project/nesi02659/users/<yourusername>/working``` and get in there
        to hold these analyses. Be careful that your are reading and writing files to the appropriate directories within
        your hierarchy. You’ll be making many directories, so stay organized!
    
    •Each step of your analysis goes into the hierarchy of the workspace, and each step of  
        the analysis takes its input from one directory and places it into another directory, this
        is known as a ‘waterfall workspace’. We will name the directories in a way that
        correspond to each stage and that allow us to remember where they are. A well
        organized workspace makes analyses easier and prevents data from being overwritten.
    
    • First let's make a few directories. In ```working```, create a directory called ```dataprep``` to contain all the data        for this exercise. Inside that directory create two additional directories: ```lane1``` and ```samples```. We will
     refer to the clean directory as the working directory.
    
    • As a check, go back to your ```working``` directory and use the '''ls''' command with the ```-R``` flag 
        (i.e.recursive), it should show you sthe following:
    
    ```
    working/:
    dataprep

    working/dataprep:
    lane1  samples

    working/dataprep/lane1:

    working/dataprep/samples:
    
    ```
    
    • Copy the data set 1 (DS1) to your ```lane1``` directory. The data set is in the file
       /nesi/project/nesi02659/source_data/clean/lane1.tar          
    
    • From your ```lane1``` folder to extract the content of this ```tar``` archive. We realise that we have not told you how         to do so! But a quick look to a friendly search engine will show you how easy it is to find this kind of information           on basic bash commands. 
    
    • Get back in your ```dataprep``` directory
    

2. Have a look at what is there now. Your decompressed files have millions of reads in it, too many for you to examine in a
spreadsheet or word processor. Examine the contents of the set of files in the terminal
(the ```less``` command may be of use).
    
    • You should see multiple different lines with different encodings.
    
    • How does the FASTQ file format work?
    
    • How are quality scores encoded?
    
    • How could you tell by eye which type of encoding your data are using (i.e. PHRED33 or PHRED64)?
    

3. Let's have a better look at this data. [FastQC] is a common software to quality-control a fastq file. 

    • Run the ```fastqc``` on any one of the fastq files. To do so, you will first need to find fastqc. It is available on the          server but it is not *loaded*. If all the softwares installed on the server were accessible at the same time it would          be one happy mess.
    
    • To ```find``` and ```load``` our first module
    
                                       
       #The below command can help find any module
       module spider fastqc
                     
       #The command should present you with some inforation about the module that have a closely matching name.
       #You can then load your module of interest, i our case fastqc
                     
       module load FastQC # Be careful with the case
    
    • Use the ```---help``` of ```fastqc``` to run it on any single fastq file of your choice..
                         
    • List the content of your directory, what did fastqc create?
    
    • Let's try to copy this file to your local computer in order to visualise it
       
    • Open a new terminal window **without closing the current one** and stay on your local computer, do not login to mahuika. 
    
    • Check out [how to copy files](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/). To identify out your path,          use the ```pwd``` command.
       
    • Once you have this file on your local computer, just double-click on it to open it with your favorite browser.

    • What is this weird thing in the base-pair content from base 7 to 12-13?

You probably noticed that not all of the data is high quality. In general, you will want
to remove the lowest quality sequences from your data set before you proceed.
However, the stringency of the filtering will depend on the final application. In
general, higher stringency is needed for de novo assemblies as compared to
alignments to a reference genome. However, low quality data will almost always
affect downstream analysis, producing false positives, such as errant SNP predictions.

4. We will use the Stacks’s program **process_radtags** to clean and demultiplex our
samples. Take advantage of the Stacks manual as well as the individual [manual page for
process_radtags](http://catchenlab.life.illinois.edu/stacks/manual/#procrad) on the Stacks website to find information         and examples. Do not run it yet but follow through the points below:
    
    • Get back into your ```dataprep``` folder
    
    • It is time to load the ```stacks``` module to be able to access the ```process_radtags``` command. Find it, load it.
     
     
    • You will need to specify the set of barcodes used in the construction of the RAD library.
        Remember, each P1 adaptor in RAD has a particular DNA sequence (an inline
        barcode) that gets sequenced first, allowing data to be associated with samples such as
        individuals or populations.
    
    • Enter the following barcodes into a file called lane1_barcodes.txt in your working
        directory. Make sure you enter them in the [right format](http://catchenlab.life.illinois.edu/stacks/manual/#specbc).
        Assign a sample name for each barcode below. Normally, these sample names would
        correspond to the individuals used in a particular experiment, but for this exercise, we
        could name the samples in a simple way, say indv_01, indv_02, etc.
            AAACGG AACGTT AACTGA AAGACG
            AAGCTA AATGAG ACAAGA ACAGCG
            ACATAC ACCATG ACCCCC ACTCTT
            ACTGGC AGCCAT AGCGCA
    
    • Copy the remaining barcodes for this lane of samples from ``` /nesi/project/nesi02659/source_data/clean/lane1_barcodes.txt```
    
    • Based on the barcode file, how many samples were multiplexed together in this
        RAD library? (Hint: count the lines.)
       
    • You will need to specify the restriction enzyme used to construct the library (SbfI), the
        directory of input files (the ```lane1``` directory), the list of barcodes, the output directory
        (```samples```), and specify that process_radtags ```clean, discard, and rescue reads.```
    
    • You should now be able to run the command from the ```dataprep``` directory. It will take a couple of minutes to run. 
    
    • The process_radtags program will write a log file into the output directory. Have a look in there.
        Examine the log and answer the following questions:
    
    -   How many reads were retained?
    
    -   Of those discarded, what were the reasons? 
    
    -   In the process_radtags log file what can the list of “sequences not recorded” tel
                you about the barcodes analyzed and about the sequencing quality in general?
    
    -   If you found that something is possibly missing from your process_radtags
                input, correct the error and re-run the process_radtags.


##  Part 2: Paired-end reads

1. We will now work with the second data set. These data contain paired-end reads that
have been double-digested and dual barcoded. Each set of paired reads contains an
inline barcode on the first read, and an indexed barcode on both reads. These are
known as combinatorial barcodes as many unique combinations can be made from
pairs of barcodes. 
    
    • In ```working/dataprep```, create a directory called ```lane2``` to contain the raw data for this
        exercise and create the directory ```ddsamples``` to contain the cleaned output.
    
    •  Copy the dataset 2 (DS2):
        /nesi/project/nesi02659/source_data/clean/lane2.tar
        into the ```lane2``` directory.
    •  Extract the lane2.tar
    
2. Examine the contents of the pairs of files in the terminal again.
   
   • How are the FASTQ headers related between pairs of files?
   
   • Can you identify the indexed barcode in the FASTQ header?
    

3. We will again use the Stacks’ program process_radtags to clean and demultiplex
our samples.
   
   • Get back into the ```dataprep``` folder
   
   • You will need to specify the set of barcode pairs used in the construction of the RAD
        library.
   
   • Enter the following pairs of barcodes into a file called *lane2_barcodes.txt* in your working
        directory (make sure you enter them in the [right format]                         (http://catchenlab.life.illinois.edu/stacks/manual/#specbc) ). As
        we saw in the previous exercise, the sample names would normally coincide with
        your particular experimental design. Here, for simplicity, we can just use ```indv_01```,
        ```indv_02```, etc.    
            AACCA/ATCACG CATAT/ATCACG GAGAT/ATCACG
            TACCG/ATCACG AAGGA/CGATGT CAACC/CGATGT
            GACAC/CGATGT TACGT/CGATGT
   
   • Copy the remaining barcodes for this lane of samples from the file:
        ```/nesi/project/nesi02659/source_data/clean/lane2_barcodes.txt```
        and append them to your barcodes file in your working directory.
   
   • How many samples were multiplexed together in this RAD library? (Hint: count the lines.) 
   
   • Similarly to what we saw aboveou will need to specify the two restriction enzymes used to construct the library
        (```NlaIII``` and ```MluCI```), the directory of input files (the lane2 directory), the list of
        barcodes, the output directory (ddsamples) and specify that process_radtags
        clean, discard, and rescue reads. Do not forget to specify the inline index and the fact that you are providing               paired-end reads.
   
   • The process_radtags program will write a log file into the output directory.
        Examine the log and answer the following questions:
    
    -   What is the purpose of the four different output files for each set of barcodes?
    
    -   How many raw reads were there?
    
    -   How many reads were retained?
    

*Congratulations, you reached the end of Exercise 1. Have a breathe, help your fellow attendees, grab a coffee and we will be back shortly for [Exercise II](https://github.com/otagomohio/2019-06-11_GBS_EE/blob/master/sessions/stacks_exerciseII_denovo.md).*
