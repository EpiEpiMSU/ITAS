Updates:
* 09.2023 - added data from MirGeneDB 2.1, duplicate records removed


In this document you can find short instructions for using databases of small non-coding RNAs published in article `ITAS: integrated transcript annotation for small RNA` (https://doi.org/10.3390/ncrna8030030). 


Integrated annotation was created for precursors and mature miRNA, piRNA, rRNA, tRNA and tRNA fragments for human, mouse, rat, C.elegans and D.melanogaster. 


Archived databases gtf-files can be found in the directory https://github.com/EpiEpiMSU/ITAS/tree/main/Integrated_annotation 


Scripts, which were used to obtain this databases located in the directory https://github.com/EpiEpiMSU/ITAS_scripts 


Structure of gtf-files
======================


One small noncoding RNA often has many loci across the genome. Because of that we have used “exon” in the feature field, the same transcript_id, but different transcript_copy_id for genomic loci of the certain transcript.


For example:


chr2    pirnadb_v1_7_6    exon    10486586    10486608    .    +    .    transcript_id "mmu-piR-10017"; transcript_copy_id "mmu-piR-10017_1"; sequence "AGTTGTGTGTGCATGTTCATGT"


chr2    pirnadb_v1_7_6    exon    10481682    10481704    .    +    .    transcript_id "mmu-piR-10017"; transcript_copy_id "mmu-piR-10017_2"; sequence "AGTTGTGTGTGCATGTTCATGT"


chr2    pirnadb_v1_7_6    exon    10484140    10484162    .    +    .    transcript_id "mmu-piR-10017"; transcript_copy_id "mmu-piR-10017_3"; sequence "AGTTGTGTGTGCATGTTCATGT"


Download and uncompress the database 
================


#downloading whole database


git clone https://github.com/EpiEpiMSU/ITAS 


#for unziping files we recommend you to use 7z tool (commands unzip/gzip don`t work directly with multi-part archives)


sudo apt install p7zip-full


#extracting whole database


7z x -y -r ITAS -o./whole_database


#extracting specific database (mouse, for example)


7z x -y -r ITAS/Integrated_annotation/mouse/ -o ./mouse_snRNA_databases


________________