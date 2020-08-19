#create a directory for your programs
cd ~
mkdir bin
#copy the subsampling program 
cd bin
cp /home/SHARE/ViromicsWorkshop/bin/random-sample-fasta.pl .
#make the viromics folder for the workshop
cd ~
mkdir viromics
#make a folder for the datasets
cd viromics
mkdir reads
cd reads
#copy the metagenomes to your folder
cp /home/SHARE/ViromicsWorkshop/example-metagenome/single-end/WCDNA-070617-45_S85_L004_R1_001.fastq.gz .

#run prinseq++
prinseq++ -fastq WCDNA-070617-45_S85_L004_R1_001.fastq.gz -ns_max 0 -derep -lc_entropy=0.5 -trim_qual_right=15 -trim_qual_left=15 -trim_qual_type mean -trim_qual_rule lt -trim_qual_window 2 -min_len 30 -min_qual_mean 20 -rm_header -out_name WCDNA-070617-45_S85_L004_R1_001 -threads 5 -out_format 1

#run a subsampling of 100,000 reads
perl ~/bin/random-sample-fasta.pl -i WCDNA-070617-45_S85_L004_R1_001_good_out.fasta -o subsample_100000_WCDNA-070617-45_S85_L004_R1_001_good_out.fasta -n 100000

#do the same for other 2 metagenomes

cp /home/SHARE/ViromicsWorkshop/example-metagenome/single-end/WCDNA-070817-45_S86_L004_R1_001.fastq.gz .
prinseq++ -fastq WCDNA-070817-45_S86_L004_R1_001.fastq.gz -ns_max 0 -derep -lc_entropy=0.5 -trim_qual_right=15 -trim_qual_left=15 -trim_qual_type mean -trim_qual_rule lt -trim_qual_window 2 -min_len 30 -min_qual_mean 20 -rm_header -out_name WCDNA-070817-45_S86_L004_R1_001 -threads 5 -out_format 1
perl ~/bin/random-sample-fasta.pl -i WCDNA-070817-45_S86_L004_R1_001_good_out.fasta -o subsample_100000_WCDNA-070817-45_S86_L004_R1_001_good_out.fasta -n 100000

cp /home/SHARE/ViromicsWorkshop/example-metagenome/single-end/WCDNA-071017-45_S87_L004_R1_001.fastq.gz .
prinseq++ -fastq WCDNA-071017-45_S87_L004_R1_001.fastq.gz -ns_max 0 -derep -lc_entropy=0.5 -trim_qual_right=15 -trim_qual_left=15 -trim_qual_type mean -trim_qual_rule lt -trim_qual_window 2 -min_len 30 -min_qual_mean 20 -rm_header -out_name WCDNA-071017-45_S87_L004_R1_001 -threads 5 -out_format 1
perl ~/bin/random-sample-fasta.pl -i WCDNA-071017-45_S87_L004_R1_001_good_out.fasta -o subsample_100000_WCDNA-071017-45_S87_L004_R1_001_good_out.fasta -n 100000

#get FRAP-basic
git clone https://github.com/yinacobian/FRAP-basic.git
cd FRAP-basic
#make database directory
mkdir DB
cd DB
cp /home/SHARE/ViromicsWorkshop/reference-Nitrogen/NitrogenBacteria.fasta .
cd ..
#make datasets directory
mkdir DS
cd DS
cp /home/acobian/viromics/reads/subsample* .
cd ..
#run FRAP
perl jmf4.pl /home/acobian/viromics/FRAP-basic/DB/NitrogenBacteria.fasta /home/acobian/viromics/FRAP-basic/DS /home/acobian/viromics/FRAP-basic/results smalt 50000


#make a folder for FRAP-tools
cd /home/acobian/viromics
mkdir FRAP
cd FRAP
#get FRAP-tools
git clone https://github.com/yinacobian/FRAP-tools.git
cd FRAP-tools
#make database folder
mkdir DB
cd DB
cp /home/SHARE/ViromicsWorkshop/reference-Nitrogen/NitrogenBacteria.fasta .
cd ..
#make dataset folder
mkdir DS
cd DS
cp /home/acobian/reads/WCDNA-070817-45_S86_L004_R1_001_good_out.fasta .
cd ..
#run FRAP-tools
bash fragplot2.sh /home/acobian/viromics/FRAP-tools/DB NitrogenBacteria.fasta /home/acobian/viromics/FRAP-tools/DS /home/acobian/viromics/FRAP-tools/results WCDNA-070617-45_S85_L004_R1_001_good_out


