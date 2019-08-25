---
title: "Tree of life - Week 35"
date: "8/22/2019"
output: html_document
---


# Week 35 - Tree of life

![Representation of a nucleotide alignment](header-image-copy18.jpg)


Phylogenetic trees are diagramas that represents the evolutionary distance among organisms. The pattern of branching in a phylogenetic tree reflects how species or other groups evolved from a series of common ancestors. 
One of the first tasks one should do in order to construct a phylogenetic tree is to align the sequences between the different organisms one would like to compare. After alignment is produced then we can calculate the genetic distances and build a phyogenetic tree representation of the distance matrix. This week we will stop our exercises after calculating the genetic distance, but next week you will learn the possible algorithms used to build phylogenetic tree.

Therefore, in this week we will:

1. Install the MEGA7 program
2. Solve the first MEGA tutorial 2
3. Understand the use of GENBANK
4. Create your own influenza data set in Fasta format
5. Understand the use of BLAST 
6. Align sequences using MEGA’s implementation of Clustal
7. Solve MEGA tutorial 3 on estimating genetic distances.
8. Estimate transition transversion bias

## 1. Install MEGA
MEGA 7.0 is the most popular free phylogenetic program available. Go to [mega website](www.megasoftware.net) and request a download. You can choose versions for Macintosh, Windows and Linux.

## 2. Solving the first MEGA tutorial 
Now solve MEGA tutorial 2 that can be found [here](https://www.dropbox.com/s/w8bbp2i44b6d6mp/MEGA_Tutorial_2.pdf?dl=0):

After finishing this tutorial, you are now able to create a multiple sequence alignment! This step will be very important for constructing phylogenetic trees later.

## 3. Understanding the use of GENBANK
GenBank is a collection of useful databases that can be accessed through from Align/Show Web Browser  in MEGA. In order to use GenBank efficiently it is a good idea to use specific search fields. These are specified as e.g. [Author], [pdat] (publication time) and [Title] and use logical operators to combine search terms, e.g. AND, OR, NOT. For example, the search “Tataru [Author] AND Markov [Title]”in the Pubmed database should return two papers.
Solve the following questions:


1.	Find and download the paper by Craig Venter from 2001 describing sequencing of the first human genome. How many pages is the paper and where was it published? How can the sequence be obtained
2.	Find the paper on the high coverage archaic Denisovan sequence published by Svante Paabos group and answer the same questions. Who were the Denisovans?
3.	How many DNA sequences and protein sequences have been determined in the dolphin (you might want to use the latin name) 
4.	Find the Taxonomic position of Dolphins and find the number of DNA sequences deposited in GenBank for each of the dolphin species
5.	Find sequences from FOXP2, which is a protein involved in human speech. How many different species has the nucleotide sequence  been determined for? Try downloading the sequences (in FASTA format). Save them (or add sequences to the MEGA alignment editor). You should download equally sized sequences of the same kind (i.e. either genomic sequences, mRNA sequences or protein sequences, not a mixture). You are free to download either protein or nucleotide sequences. Create a file called foxp2.fas

## 4. Creating your own influenza dataset 

6.	Create your own influenza sequence data set from Genbanks flu database http://www.ncbi.nlm.nih.gov/genomes/FLU/Database/nph-select.cgi. Choose protein coding region, Type A, canine and cat, any region, HA protein, any H subtype, any N subtype and full length only. While this analysis can be carried out in MEGA own browser it may be more easy to do it from your own browser and then later import the results to MEGA
a.	How many sequences do you get ? Choose 10 of these from different species and from different subtypes and download them both as protein coding and protein in Fasta format as flucoding.fas and fluprotein.fas. We will use these for the alignment exercise and for phylogenetic exercises in the coming weeks


## 5. BLAST 
Blast stands for Basic Local Alignment Search Tool and is a way to search for homologous sequences in a database using a query sequence (for example if you have a gene and will look for orthologous genes in different species or members of the same gene family in the same species). It is probably the most widely used computational tool in (molecular) biology.
BLAST is also integrated in MEGA which now has a built in web browser interface. The advantage of browsing from MEGA being that you can also import directly the sequences you found in MEGA (using the big “ADD to alignment red button”)
  1. Use Genbank to retrieve the mitochondrial genome from the Neanderthal and then do a BLAST search to find the most closely related sequences

## 6. Alignment
You have downloaded  flu data sets and you should now align these within MEGA’s alignment explorer. If you doubleclick a file it may open directly in MEGA’s alignment explorer
First open your flucoding.fas.

  1.	Align this at the DNA level using Clustal. Look carefully at all the parameters and try to change them and see how that affects the alignment. Tip: Before you realign you should first remove all gaps. Try to judge the quality of your alignment by looking at it both at the DNA level and at the protein level. 
    a.	Try to see how you can manually edit your alignment afterwards. Export your best alignment in Megaformat as flucoding.meg for later use

  2.	Now remove gaps and choose to translate to amino acids before aligning. Aligning is now at the protein level so Clustal will show different options. Try different combinations and evaluate the alignment as before. Does it seem to be an advantage to align at the protein level and then translate back to nucleotide sequences? Export your best alignment in mega format
  3.	Repeat some of the previous questions using the Muscle alignment tool.
  4.	Perform alignment also of your FoxP2 data set and export in Mega format
  5.	Now open your fluprotein.fas dataset, align it and export it as fluprotein.meg

## 7. Estimating distances
First go carefully through [MEGA tutorial 3](https://www.megasoftware.net/webhelp/walk_through_mega/estimating_evolutionary_distances_from_nucleotide_sequences.htm)
If you are in doubt about what each function is doing, then go to the website:
https://www.megasoftware.net/web_help_10/index.htm#t=Preface.htm


First open flucoding.meg in MEGA. We now want to estimate pairwise distances between all 10 sequences. Choose this option and you will see that there are a lot of choices you can make. Make sure you understand all of these, e.g

  1.	what is complete versus pairwise deletion?
  2.	what is the variance estimation method?
  3.	what does it mean that transitions and transversions can be used?

You can now try to make distance matrices using p distances, Jukes Canter, Kimura 2 parameter and Tamura Nei models, more detailed information on these are found in the Book Chapters 2 and 3 of Nei and Kumar. Make sure you know what each of these models are doing, e.g.

  1.	What are the parameters in these models?
  2.	Which model estimates largest distances and why?

Now try on the same data to estimate the transition/transversion bias as well as the gamma parameter using maximum likelihood under the Models menu. 

  1.	What does the result tell you regarding which substitution model to use?
      a. How do you interpret the value of R, the ratio of transitions to transversions?
  2.	Does the gamma rate parameter suggest large variation in underlying substitution rate?
Now open fluprotein.meg instead and estimate distances at the protein level.
  1.	What differences do you see between p distance and Poisson corrected distance?
      a. What are the distances at the protein level compared to the distances at the nucleotide level?


