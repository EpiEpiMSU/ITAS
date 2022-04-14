In this document you can find short instructions for using databases of small non-coding RNAs (piRNA, miRNA (mature and precursors), tRNA, rRNA), published in article “ITAS: integrated transcript annotation for small RNA”. 

Archived databases gtf-files can be found in the directory https://github.com/EpiEpiMSU/ITAS 

Scripts, which were used to obtain this databases located in the directory https://github.com/EpiEpiMSU/ITAS_scripts 
Files HUMAN_DATABASES.R, MOUSE_DATABASE.R, RATS_DATABASE.R, CELEGANS_DATABASE.R, DROSOPHILA_DATABASE.R contain commands which were performed to process raw database files, to create consensus database, to search for conflicts in used database for each organism.
File exel_to_final_gtf.R contain script for creating presented gtf-files based on the tables, obtained on the prrevious step. 

Download the database and uncompress it
================

#downloading whole database
git clone https://github.com/EpiEpiMSU/ITAS 

#for unziping files we recommend you to use 7z-tool (commands unzip/gzip don’t work directly with multi-part archives)

sudo apt install p7zip-full

#extracting whole database
7z x -y -r ITAS -o./whole_database

#extracting specific database (mouse, for example)
7z x -y -r ITAS/Integrated_annotation/mouse/ -o./mouse_snRNA_databases

Examples of NGS-data analysis are presented below

Alignment
=========

#alignment to reference genome by hisat2 
hisat2 -x /path/to/reference -U ./path/to/fastq -S /path/to/sam/output -k 1 --no-spliced-alignment --no-softclip --summary-file /path/to/summary/output

#or by bowtie
bowtie -x /path/to/reference -q ./path/to/fastq -S /path/to/sam/output --large-index -v 1 -m 100 -k 1 --best --strata

#for our databases we have used follow versions of reference genomes: hg38 for human, #mm39 for mouse, rn7 for rat, ce11 for C.elegans and dm6 for drosophila. 

Calculating gene counts
=======================

#you can calculate gene counts based on our snRNA databases by r-function featureCounts
featureCounts(files=sample_file, annot.ext=database_file, isGTFAnnotationFile = TRUE, GTF.featureType = "exon", GTF.attrType = "transcript_id", minFragLength=15)

Stracture of gtf-files
======================

snRNAs sometimes have the number of loci across the genome.  Because of that we have used “exon” in the feuture fiel, the same transcript_id but different transcript_copy_id for genomic locies of the certain trancript.

For example:

NC_005089.1    pirnadb_v1_7_6    exon    2409    2432    .    +    .    transcript_id "mmu-piR-1563"; transcript_copy_id "mmu-piR-1563_1"; sequence "ACAATTAGGGTTTACGACCTCGA"

NC_005089.1    pirnadb_v1_7_6    exon    3844    3865    .    +    .    transcript_id "mmu-piR-8131"; transcript_copy_id "mmu-piR-8131_1"; sequence "AGTAAGGTCAGCTAATTAAGC"

chr2    pirnadb_v1_7_6    exon    10486586    10486608    .    +    .    transcript_id "mmu-piR-10017"; transcript_copy_id "mmu-piR-10017_1"; sequence "AGTTGTGTGTGCATGTTCATGT"

chr2    pirnadb_v1_7_6    exon    10481682    10481704    .    +    .    transcript_id "mmu-piR-10017"; transcript_copy_id "mmu-piR-10017_2"; sequence "AGTTGTGTGTGCATGTTCATGT"

chr2    pirnadb_v1_7_6    exon    10484140    10484162    .    +    .    transcript_id "mmu-piR-10017"; transcript_copy_id "mmu-piR-10017_3"; sequence "AGTTGTGTGTGCATGTTCATGT"
