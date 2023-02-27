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
