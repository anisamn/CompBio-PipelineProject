# CompBio-PipelineProject 
Pipeline Project Track 2 -- Genome Assembly 

Setup: 
Download SRRs from NCBI using wget. 
Run fastq-dum -I --split-files (SRR) 
   output names are _#.fastq 

Project: 
1. Which strains are most similar to the patient samples? 
   -Use Bowtie2 to create an index for HCMV (NCBI accession NC_006273.2). 
   
   **bowtie2-build (downloaded fasta file) (output name)** 
      output names are .bt2
   
   -then... 
   
   **bowtie2 --quiet -x (output name) -1 (SRR#1) -2 (SRR#2) -S HCMVmap.sam**
      output names are .sam
      
   -Save only the reads that map to the HCMV index for use in assembly. 
   
   
   
   **Donor 1 (HCMV30) had 2,259,287 read pairs before Bowtie2 filtering and 4,518,577 read pairs after**
   
2. Using the Bowtie2 output reads, assemble all four transcriptomes together to produce 1 assembly via SPAdes.
Write the SPAdes command you used to the log file.

**spades.py -k 77,99,127 -t 2 --only-assembler --pe-1 1 SRR5660030_1.fastq --pe-2 2 SRR5660030_2.fastq --pe-1 1 SRR5660033_2.fastq --pe-2 2 SRR5660033_2.fastq --pe-1 1 SRR5660044_2.fastq --pe-2 2 SRR5660044_2.fastq --pe-1 1 SRR5660045_2.fastq --pe-2 2 SRR5660045_2.fastq -o HCMV-SRR_assembly/**
