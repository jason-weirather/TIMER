# TIMER
Fork of Li, Bo, et. al. Genome Biology https://doi.org/10.1186/s13059-016-1028-7

### This is not the official distribution of the TIMER software.  This is a fork for pipeline incorperation.  

Visit http://cistrome.org/TIMER/download.html for the official distribution and cite:

Li T, Fan J, Wang B, Traugh N, Chen Q, Liu JS, Li B, Liu XS. TIMER: A Web
Server for Comprehensive Analysis of Tumor-Infiltrating Immune Cells. Cancer Res.
2017 Nov 1;77(21):e108-e110. doi: 10.1158/0008-5472.CAN-17-0307. PubMed PMID:
29092952.

## TIMER readme

Thank you for using TIMER!!

TIMER source codes were written in R, any question should be addressed to Bo Li (bli@jimmy.harvard.edu). This file is intended to instruct a skilled bioinformatician to repeat the analysis of TIMER on a local computer. If you are not familiar with bioinformatics analysis, and interested in looking at the clinical associations of tumor infiltrating immune cells, please ignore this webpage and directly use the TIMER website.

1. Prepare required datasets.

TIMER analaysis was all performed on the Cancer Genome Atlas (TCGA) samples. The gene expression data profiled by RNA-seq or Affymetrix arrays are accessible through GDAC firehose (https://gdac.broadinstitute.org). Please first download all the data matrices (preferrably RSEM, if not available, then RPKM) and transform them into XXXX.Rdata format (where XXXX is the cancer abbreviation, in lower case, same below), then deposit into a folder named "RNAseq". Clinical data for all cancers should be downloaded from TCGA public ftp: https://tcga-data.nci.nih.gov/tcgafiles/ftp_auth/distro_ftpusers/anonymous/tumor/XXXX/bcr/nationwidechildrens.org/bio/clin/. Replace "XXXX" with the desired cancer abbreviation and select the latest version of the clinical file ending with "patient_XXXX.txt". Please put all the clinical data files into a folder named "Clinical". TIMER requires tumor purity information for acurate estimation of immune-related genes. Purity is available in the Related data files. After downloading the zip file, please unzip the purity estimation files into a folder named "AGP". TIMER also uses reference immune cell expression files to estimate the immune infiltration levels. These files are available in the Related data files 1-3. Please download these files and put them into a folder named "immune_datasets". Please also download the Supplementar Table S5 from Rooney et al., 2015, Cell and convert it to a text file (mmc5.txt) and place it into a folder named "virus". 

2. Prepare required R packages.
TIMER analysis requires a number of R packages, including: ggplot2, ppcor, reshape2, survival, qvalue and CHAT. Make sure you have installed these packages before running the R codes.

3. Data depository structure.
Please put all the folders in step 1 into one folder named "data". Download the R codes and put both .R files at the same level of folder 'data'. Create a new folder at this level, named 'results/'. Under results/, create 23 folders, each with the name of the cancer abbreviation in lowercase. The analysis results for each cancer will be written in the corresponding folder. Please download Related data file 5 and put on the same level as the R codes. Upon finishing this step, your current folder should have 2 folders (data and results), 1 Rdata file and 2 R codes.

4. Running TIMER.
If you are interested in one cancer, please open an R console, type:
cc='XXXX'	## replace XXXX with your desired cancer abbreviation
cur.dir='Path_to_your_current_directory'
source('CancerImmunePipeline.R')

5. Running TIMER in batch mode
Open R console, type:
setwd("Path_to_your_current_directory")
source('SummarizeResults.R')

The R code will iteratively analyze each cancer and put the statistical results as well as diagnostic figures into the results/XXXX/ folders.

Note: the second half of SummarizeResults.R contains a number of R functions for making plots. These codes are not automatically run and requires a pre-designed color scale file. Please download Related data file 6 and change the corresponding file path in these R functions. 
