# Dose response RNA seq analysis 

# 0. Seting up to run the pipeline

## 0.1 Make two directories for pcb and bkf snakemake directories 

## 0.2 Upload fastq files

## 0.3 Set up sample names

create file with all sample names within each directory

```
ls | awk '{print substr($0, 1, 18)}' > sample_names.txt
```

this didn't totally work and had to be checked manually
also it doubles the names--shouldnt really matter bc 

## 0.3 Clone snakemake repository into each snakemake directory

```
git clone https://github.com/JoannaGriffiths/RNASeq-snakemake-pipeline.git
```

## 0.4 Set up references

```
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/011/125/445/GCF_011125445.2_MU-UCD_Fhet_4.1/GCF_011125445.2_MU-UCD_Fhet_4.1_rna.fna.gz
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/011/125/445/GCF_011125445.2_MU-UCD_Fhet_4.1/GCF_011125445.2_MU-UCD_Fhet_4.1_genomic.fna.gz
```

make file references.txt with file names of reference genome and transcriptome

# 1. Changes to the pipeline

## 1.1 Alter snakemake.sh

change home directory, email to my own

change output files to pcb and bkf directory

change working directory to pcb and bkf directory

delete line `module load deprecated/fastp/0.20.1`

change `source activate snakemake` to `source activate snakemake2`

## 1.2 Clone conda environment and install nondeprecated fastp

```
module load conda/base/latest
conda create --name snakemake2 --clone snakemake
conda install -n snakemake2 -c bioconda fastp
```

# Problems

## File corruption

pcb snakemake job failed due to file corruption (061C_NB_4_S79_L007_R1_001.fastq.gz) from the source. I will remove from analysis for now and try to recover it. Ran md5sum on forward and reverse reads of 061C

```
md5sum /Volumes/easystore/CRios_RNAseq_7-2024/18048-200-06242024_155635-422764342/BaseSpace_CLI_2024-06-24_15_57_14Z-741985279/001C_SC_0_S3_L007_R1_001.fastq.gz_-ds.58edd8311b0a458faee27cc2ca23bbe9/061C_NB_4_S79_L007_R1_001.fastq.gz
```

```
md5sum: WARNING: 13231642 lines are improperly formatted
```
