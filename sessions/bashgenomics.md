# Bash genomics
**Developed by:** Ludovic Dutoit

Over the last few lessons, we learnt the every day tools that will allow you to work in the command line environment.
In this exercise, we will try to **reinforce our skills, touch base with genomics, and appreciate the power of the command line**.


For this exercise we will work with the chicken genome.


1. Create a directory called *chicken_genome_exercise/*. [Hint](hints/bash_genomics_1.md)

2. Copy the chicken genome *chicken.fa* from: 

```
/nesi/nobackup/nesi02659/source_data/chicken.fa
```

to your newly created *chicken_genome_exercise/* directory. [Hint](hints/bash_genomics_2.md)


The *.fa* extension denotes the fasta format. 

The [Zhang Lab](https://zhanglab.ccmb.med.umich.edu/FASTA/) has a good description of the fasta format:  
"The fasta format is a text-based format for representing either nucleotide sequences or peptide sequences, in which base pairs or amino acids are represented using single-letter codes. A sequence in FASTA format begins with a single-line description, followed by lines of sequence data. The description line is distinguished from the sequence data by a greater-than (">") symbol in the first column."

```
>CHROM 1
ATGAGAGCGGTCTGAGAGTCTTAGAGGAGCGGATTATTA
GAGAGGGAGAGATCTATAGAGCTA
>GENEHPC 2
GAGAGCTATSTCGATATCTGAGGAGA
```

3. Can you print all the sequence names to the screen ? [Hint](hints/bash_genomics_3.md)


4. Can you tell the total length of the genome? This command can take a little bit of time to run! [Hint](hints/bash_genomics_4.md)


5. Since we are doing GBS we are interested in knowing how frequent restriction enzyme cut sites are. Can you tell me how many cut sites there are for:

	* PstI CTGCAG
	* ecoRI CTTAAG	
	* SbfI CCTGCAGG
	
	[Hint](hints/bash_genomics_5.md)
	

6. Bonus question: Take into account the reverse strand when calculating the number of sites!



In this challenging exercise you played around with some basic data using pre-existing programs and the available help you could find (i.e. the instructors, colleagues, `--help` and Google). This is very much like real-life genomics!




[Jump back to Introduction to the command line](https://otagomohio.github.io/2019-06-11_GBS_EE/sessions/Introcommandline.html)  
[Jump back to main workshop schedule](https://otagomohio.github.io/2019-06-11_GBS_EE/)
