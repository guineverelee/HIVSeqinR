# HIVSeqinR
Please download the latest version.  "HIVSeqinR" is an R-based pipeline that processes HIV near-full-genome sequences and classifies genomes into "intact" or into various "defective" categories.  Please see Wiki tab for more information.

#####################################
UPDATE & Bug Fixes History
#####################################

HIVSeqinR update, April 15, 2021.
1. Please make sure to include at least one reference sequence or positive control per run.  If there is no positive control in the sequencing batch, then please append Examples_8E5_HXB2.fasta to your input fasta.


HIVSeqinR update, March 27 ,2020.  
1. Please ensure your FASTA sequence names are unique.  
2. Please ensure the only special characters in your FASTA sequence names is "_".  HIVSeqinR will not take any sequence names with other special characters.


HIVSeqinR version 2.7.1 README.txt
Dec 16, 2019
Major bug fix:  Up until version 2.6.4, scramble-but-not-inverted viral genomes has been missed.  This feature is now fixed.  


HIVSeqinR version 2.6.4 README.txt
BugFix: Included cases in which after pasting Tat exon 1 and Tat exon 2, there are no stop codon.


HIVSeqinR version 2.6.3 README.txt
BugFix: I observed an unusual case of Rev starting with a stop codon.  It is now exported as having amino acid length == 0.


HIVSeqinR version 2.6.2 README.txt

Update:
Category "PrematureStop" has been renamed to "PrematureStop_OR_AAtooLong_OR_AAtooShort."  This bin includes cases in which HIV Gag, Pol and/or Env has/have abnormal amino acid (AA) length(s).  Cutoffs can be adjusted by users.


HIVSeqinR version 2.6.1 README.txt

ver2.6.1 update log:
1. relaxed max.match= from 0 to 1 when searching for primers in autotrim
2. add note about plasmid sequences noted above

#####################################

Dear users,

This script is meant for analyzing linear HIV genomes WITH FLANKING PRIMER binding sites at 5' and 3' ends. This script is made specifically for the analysis of post de novo derived consensus sequences that came from the MGH DNA core de novo assembly pipeline Ultracycler v1.0 (H Wang & B Seed to be published).  

This pipeline will NOT take plasmid sequences that contain HIV genomes. For this and other customized needs, please feel free to contact me at guinevere.q.lee@gmail.com.

Best, 
Guin



#####################################################
1.  System requirements
#####################################################
- HIVSeqinR can be run locally on any Mac and PC consumer computers.  It only has three dependencies (blast+ suite and R packages: Biostrings and muscle).  Run time per intact-sequence on a 2017 Macbook Pro i7 16GB is approximately 30 seconds.  HIVSeqinR also has an optional deep sequencing quality control arm.  For further documentation, please visit https://github.com/guineverelee/HIVSeqinR.
- Finalization of the pipeline development was performed in macOS High Sierra Version 10.13.6, R version 3.5.1, R library muscle 3.22.0, R library Biostrings 2.48.0, NCBI blast 2.7.1


#####################################################
2. Install guide and instructions for use
#####################################################

Welcome to the HIVSeqinR wiki!

HIVSeqinR is an R-based pipeline that processes HIV near-full-genome sequences and classifies genomes into "intact" or into various "defective" categories. For each sequence input, this pipeline will label it with a single verdict. There are 31 possible verdicts highlighted in yellow in the documentation (including “Intact,” “PrematureStop,” “Hypermut” etc). When a verdict contains the word “Check,” it is a flag to alert users that there is an abnormality. In these cases, I suggest users manually validate that the pipeline’s verdict is correct. The final MyVerdict for each sequence input can be found in the last column in output file "Output_MyBigSummary_DF_FINAL.csv."

It also translates all coding regions into amino acids where appropriate. It has minimal dependency (local NCBI blastn, R library(Biostrings), and R library(muscle). It has been optimized for RAM efficiency. Run time per intact-sequence on a 2017 Macbook Pro i7 16GB is approximately 30 seconds.

To run the script:

First, open R_HIVSeqinR_Combined_ver04.R in R studio. As long as this following section is user-verified to be ready, press CTRL-A, then CTRL-R to run all lines in the R script.

Dependencies

1. install library(Biostrings)
2. install library(muscle)
3. install blast+ suite, create HXB2 library installed in directory: MyBlastnDir <- "/Users/guin/" #change as appropriate Follow blast+ suite installation instructions at https://www.ncbi.nlm.nih.gov/books/NBK279671/ To create HXB2 library in blast+ suite, use commend: makeblastdb -in HXB2.fasta -parse_seqids -dbtype nucl Make sure to rename R_HXB2.fasta to HXB2.fasta after copying file into dir where blast+ suite is installed
4. Primer Settings: Currently Optimized for these two 2nd round PCR primers. NGS library prep method must be shearing and adaptor-ligation based so that post de novo assembled contig is flanked by both primers Primer2ndF_HXB2 <- "GCGCCCGAACAGGGACCTGAAAGCGAAAG" Primer2ndR_HXB2 <- "TAAGCCTCAATAAAGCTTGCCTTGAGTGC"
5. Copy and paste all raw *.seq files in folder RAW_FASTA. No dashes, *, or IUPAC mixture symbols are allowed (eg. N, R, S, Y etc) Optional: Copy and paste all raw *.csv files in folder RAW_QC
6. Final check: Dir should have four files and at least one folder: (1) HIV Genome RefSeq ver04 AA.fasta (2) HIV Genome RefSeq ver04 NUC.fasta (3) R_HXB2.fasta (4) R_HIVSeqinR_Combined_ver04.R (5) ./RAW_FASTA/ #folder containing fasta file(s) of post de novo assembled contigs (6) ./RAW_QC/ #optional, only if using the Massachusetts General Hospital CCDB Core service

Typical installation time and dependancies installation on a desktop computer should take about 30 minutes.  


#####################################################
3.  Demo
#####################################################
An experimentally single-genome amplified near-full-length HIV provirus (8E5LAV NIH AIDS Reagent Program #95) and the standard reference sequence HXB2 are provided here as a demo set.
1. Install R and dependencies as outlined above 
2. Download and unzip "HIVSeqinR_ver2.6_Guin_FINAL.zip"
3. Double click "R_HIVSeqinR_Combined_ver04.R"
4. No additional settings adjustments are needed.
5. Highlight all lines and run all
6. See results in folder "Results_Final"
7. For example, open "Output_HIVSeqinR_ver02.6.pdf" to see a graphical representation of each of the genes in the genomes translated, and whether the encoded protein are likely defective or not.  See full definitions in the documentation file.


#####################################################
Support
#####################################################
Please report all comments and/or bugs to guinevere.q.lee@gmail.com





Run time on a 2017 Macbook Pro i7 16GB was approximately 1 minute.

