**In construction

# Bash genomics

Over the last few lessons, we learnt the every day tools that will allow you to work in the command line environment.
In this exercise, we will try to **reinforce our skills, touch base with genomics and appreciate the power of the command line**.


For this exercise we will work with the human genome.

It is currently stored on your computer at:

```
PATH TO THE GENOME # WRITE PROTECT IT CALL it hgenome.fa
```

1. Create a directory called *human_genome_exercise/*. 

2. Copy the human genome *hgenome.fa* in the newly created *human_genome_exercise/*. .


The fasta format DESCRIPTION

```
>CHROM 1
ATGAGAGCGGTCTGAGAGTCTTAGAGGAGCGGATTATTA
GAGAGGGAGAGATCTATAGAGCTA
>GENE HYPOXIA 2
GAGAGCTATSTCGATATCTGAGGAGA
```

3. Can you print all the sequence names to the screen ?

4. Can you tell me the total length of the genome?


Hint: Can you find eveything BUT the sequence names? You only have to count the characters now, can you remember how to count the lines?


5. Since we will look for restrinction enzymes. Can you tell me how many cut sites there are for :

	* Pst1 CTGCAG
	* X X
	* Pst1 CTGCAG

	4 cutters are much more frequents than  6 cutters.


6. Bonus question: Take into account the reverse strand when calculateing the number of sites!

TODO: TRY TO INCROPORATE SOME of the commands zcat etc that we need for the rest


In this challenging exercise you played around with some basics data using pre-existing programs and the available help you could find (i.e. the instructors, colleagues, --help and Google). This is very much like real-life genomics!


