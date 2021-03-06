# ViromicsWorkshop

August 19, 2020

Viromics Workshop

Workshop: a meeting at which a group of people engage in intensive discussion and activity on a particular subject or project.

To participate you need to complete the following requirements: 

1) Have a dataset to work with 

2) Have access to a server

3) Be able to use the command line

This is a good intro:
https://dev.to/awwsmm/101-bash-commands-and-tips-for-beginners-to-experts-30je#the-basics

4) Be able to move files between your computer and the server

5) Be able to download files from the web to the server

6) Be willing to share a figure of your analysis for this repository

## 0. Materials

  * DATASETS
  
Example metagenomes reads
`/home/SHARE/ViromicsWorkshop/example-metagenome`

Example bacteria genome reads
`/home/SHARE/ViromicsWorkshop/example-bacteria`

Example phage genome reads
`/home/SHARE/ViromicsWorkshop/example-phage`

  * DATABASES

Reference genome for bacteria assembly

Reference database: Viral RefSeq 
`/home/DATABASES/RefSeq/viral/all_viral_genomic.fna`

Reference database: Virulence Factors
`/home/DATABASES/VirulenceFactors/VFDB_setA_nt.fas`

## 1. What to do with my data after it's sequenced?

### 1.1 Download

  * To download files directly from a server with a username and password:

`wget --user user --password pass http://example.com/`

  * To copy files from a remote server
  
 `scp your_username@remotehost.edu:/home/examplefile.txt /some/local/directory`

### 1.2 Naming

  * Single end reads look like this:
```
sputumCF189mg_R1.fastq
```
  
  * Paired end reads look like this:
```
VIP_2015_ART_1A_BS_mg_RUN2_R1.fastq 
VIP_2015_ART_1A_BS_mg_RUN2_R2.fastq
```
  Or like this:
  
```
phiAxy06_S67_R1_001.fastq
phiAxy06_S67_R2_001.fastq
```

  * Single end reads from a single library, but with different barcodes look like this:
```
WCDNA-070617-45_S85_L004_R1_001.fastq.gz
WCDNA-070617-45_S85_L005_R1_001.fastq.gz
WCDNA-070617-45_S85_L006_R1_001.fastq.gz
```

> What is a paired end read? https://www.youtube.com/watch?v=WneZp3fSJIk

### 1.3 Quality filtering using prinseq++

prinseq++ paper: https://peerj.com/preprints/27553/

  * prinseq++ for single end files
  
`prinseq++ -fastq WCDNA-070617-45_S85_L004_R1_001.fastq.gz -ns_max 0 -derep -lc_entropy=0.5 -trim_qual_right=15 -trim_qual_left=15 -trim_qual_type mean -trim_qual_rule lt -trim_qual_window 2 -min_len 30 -min_qual_mean 20 -rm_header -out_name WCDNA-070617-45_S85_L004_R1_001 -threads 5 -out_format 1`

the output looks like this:

```
WCDNA-070617-45_S85_L004_R1_001_good_out.fasta
WCDNA-070817-45_S86_L004_R1_001_bad_out.fasta
```

  * prinseq++ for paired end files
  
> What is a fastq file? https://en.wikipedia.org/wiki/FASTQ_format

> What is a phred quality score? https://en.wikipedia.org/wiki/Phred_quality_score

### 1.4 (Optional) Subsampling of the reads

`perl ~/bin/random-sample-fasta.pl -i WCDNA-070617-45_S85_L004_R1_001_good_out.fasta -o subsample_100000_WCDNA-070617-45_S85_L004_R1_001_good_out.fasta -n 100000`

the output looks like this:

```
subsample_100000_WCDNA-070617-45_S85_L004_R1_001_good_out.fasta
```
## 2. Metagenomes to target databases using FRAP

> What is FRAP? https://github.com/yinacobian/frap

2.1 Metagenome to any database using FRAP 

https://github.com/yinacobian/FRAP-basic


## 3. How to create a FRAP database?

A FRAP database is any fasta or multifasta file with the following characteristics:

Each sequence has a unique ID

Each sequence header has the following format:

`>UNIQUEID Sequence name or description of the sequence`


## 4. Fragment Recruitment Plots 

4.1 Create Fragment Recruitment Plots: 

https://github.com/yinacobian/FRAP-tools

Examples:

  * Water column metagenome from Curacao recruited against a *Pelagibacter* genome, created by Jason Baer

![Palegibacter!](fragplot_subsample_100000_CSA229_S182_L008_R1_001_good_out_AZAL01000001.1.png)

  * Prophage induction: Achromophage lysate reads recruited against *Achromobacter xylosoxidans* genome, created by Ana Cobian
  
![Prophage](fragplot_LB5-V-cscl_good_out_R2_AchromobacterCF418.png)

## 5. Bacteria Genome Assembly

### 5.1 Denovo assemply with SPADes

> SPADes paper: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3342519/

Use SPADes

`spades.py -s reads.fasta --only-assembler -t 20 -o output_folder`

SPADes for paired-end reads

`spades.py -1 reads_R1.fasta -2 reads_R2.fasta --only-assembler -t 20 -o output_folder`

### 5.2 From contigs to a single chromosome, CONTIGUATOR

http://combo.dbe.unifi.it/contiguator

CONTIGUATOR paper: https://scfbm.biomedcentral.com/articles/10.1186/1751-0473-6-11

### 5.3 Bactetria genome annotation, PATRIC

https://www.patricbrc.org/

PATRIC paper: https://pubmed.ncbi.nlm.nih.gov/27899627/

## 6. Phage Genome Assembly 

6.1 Subsampling the reads

6.2 Denovo assembly with SPADes

6.3 Assembly visualization with BANDAGE

BANDAGE paper: https://academic.oup.com/bioinformatics/article/31/20/3350/196114

BANDAGE download: https://rrwick.github.io/Bandage/


