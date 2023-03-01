# CompBio-PipelineProject 
Pipeline Project Track 2 -- Genome Assembly 

Setup: 

Download SRRs from NCBI using wget. 

Run fastq-dum -I --split-files (SRR) 

output names are _#.fastq 

Project: 
1. Which strains are most similar to the patient samples? 
   
   -Use Bowtie2 to create an index for HCMV (NCBI accession NC_006273.2). 
   
   **bowtie2-build (downloaded fasta file) (output name_1)** 
      
      output names are .bt2
   
   -then... 
   
   **bowtie2 --quiet -x (output name_1) -1 (SRR#1) -2 (SRR#2) -S HCMVmap.sam**
      
      output names are .sam
      
   -Save only the reads that map to the HCMV index for use in assembly. 
   
   **bowtie2 -x (output name_1) -1 (fasta_1 name) -2 (fasta_2 name) -S (corresponsing fasta.sam file) --al-conc-gz            (output name_2)**  
   
Results:
   
   **Donor 1 (HCMV30) had 2259287 read pairs before Bowtie2 filtering and 1480440 read pairs after**
   
   **Donor 2 (HCMV33) had 2004530 read pairs before Bowtie2 filtering and 1437516 read pairs after**
   
   **Donor 3 (HCMV44) had 2730258 read pairs before Bowtie2 filtering and 1797601 read pairs after**
   
   **Donor 4 (HCMV45) had 2476889 read pairs before Bowtie2 filtering and 1858964 read pairs after**
   
   2. Using the Bowtie2 output reads, assemble all four transcriptomes together to produce 1 assembly via SPAdes.
   Write the SPAdes command you used to the log file.

**spades.py -k 77,99,127 -t 2 --only-assembler --pe-1 1 HCMV30_mapped_1.fq.gz --pe-2 1 HCMV30_mapped_2.fq.gz  --pe-1 2 HCMV33_mapped_1.fq.gz --pe-2 2 HCMV33_mapped_2.fq.gz --pe-1 3 HCMV44_mapped_1.fq.gz --pe-2 3 HCMV44_mapped_2.fq.gz --pe-1 4 HCMV45_mapped_1.fq.gz --pe-2 4 HCMV45_mapped_2.fq.gz -o HCMV2-SRR_assembly**

   3. Write python code to calculate the number of contigs with a length > 1000 and write the number log files: 
   
   **There are # contigs > 1000 bp in the assembly**
   
   Write python code to calculate the length of the assembly (total number of bp in all the contigs > 1000 bp in length) and write this # to the log file: 
   
   **There are # bp in the assembly**
   
