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

## 1. What to do with my data after it's sequenced?

1.1 Download

  * To download files directly from a server with a username and password:

`wget --user user --password pass http://example.com/`

  * To copy files from a remote server
  
 `scp your_username@remotehost.edu:/home/examplefile.txt /some/local/directory`

1.2 Naming

  * Single end reads look like this:
```
sputumCF189mg_R1.fastq
```
  
  * Pair end reads look like this:
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
WCDNA-070617-45_S85_L006_R1_001.fastq.gz
WCDNA-070617-45_S85_L005_R1_001.fastq.gz
```

1.3 Quality filtering using prinseq++

prinseq++ paper: https://peerj.com/preprints/27553/

`prinseq++ -fastq $2/P00_raw/{fileID}_R1.fastq -ns_max 0 -derep -lc_entropy=0.5 -trim_qual_right=15 -trim_qual_left=15 -trim_qual_type mean -trim_qual_rule lt -trim
_qual_window 2 -min_len 30 -min_qual_mean 20  -rm_header -out_name $2/P01_prinseq_output/{fileID} -threads $3 -out_format 1`

## 2. Bacteria Genome Assembly

2.1 Denovo assemply with SPADes

SPADes paper: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3342519/

2.2 From contigs to a single chromosome, CONTIGUATOR

http://combo.dbe.unifi.it/contiguator

CONTIGUATOR paper: https://scfbm.biomedcentral.com/articles/10.1186/1751-0473-6-11

2.3 Bactetria genome annotation, PATRIC

https://www.patricbrc.org/

PATRIC paper: https://pubmed.ncbi.nlm.nih.gov/27899627/

## 3. Phage Genome Assembly 

3.1 Subsampling the reads

3.2 Denovo assembly with SPADes

3.3 Assembly visualization with BANDAGE

BANDAGE paper: https://academic.oup.com/bioinformatics/article/31/20/3350/196114

BANDAGE download: https://rrwick.github.io/Bandage/

## 4. Metagenomes to target databases using FRAP

https://github.com/yinacobian/frap

4.1 Metagenome to viral refseq using FRAP 


## 5. HeatMaps from FRAP output


## 6. Fragment Recruitment Plots 

https://github.com/yinacobian/FRAP-tools

## 7. How to create a FRAP database?


## 8. I have a host-associated metagenome, how can I remove the host reads from the analysis?
