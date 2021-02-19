# SARS-CoV-2
Sequences and Tools for dealing with SARS-CoV-2 Spike Protein

This is a blastp database created from NCBI 
on Friday February 19 before 9AM Pacific Time.

The following commands were used after loading all_sequences 
from the database:

The 44,027 sequences were downloaded from this webpage, indicating downloads for "all hosts"

https://www.ncbi.nlm.nih.gov/datasets/coronavirus/genomes/

cd /Volumes/SATA/NCBI_sars
# an awk command was used to reformat the uncompressed file:
awk '/^>/ {printf("\n%s\n",$0);next; } { printf("%s",$0);}  END {printf("\n");}' < SARSprotein.faa > SARSproteinformat.faa
# the following was invoked to build the blastp database:
/Users/bgold/ncbi-blast/bin/makeblastdb -in SARSproteinformat.faa -parse_seqids -title "SARS-CoV-2 PROTEIN 02192021" -dbtype prot
#The output then included
#####Building a new DB, current time: 02/19/2021 07:30:30
#####New DB name:   /Volumes/SATA/NCBI_sars/SARSproteinformat.faa
#####New DB title:  SARS-CoV-2 PROTEIN 02192021
#####Sequence type: Protein
#####Keep MBits: T
#####Maximum file size: 1000000000B
#####Near line 11620, the sequence id string contains 'comma' symbol, which has been replaced with 'underscore' symbol. Please correct the sequence id string.
#####Near line 11696, the sequence id string contains 'comma' symbol, which has been replaced with 'underscore' symbol. Please correct the sequence id string.
#####etc.
#The query was then made:
/Users/bgold/ncbi-blast/bin/blastp -query sprotein.faa -db SARSproteinformat.faa -show_gis -matrix BLOSUM45 -max_hsps 1574836 -max_target_seqs 1574836 -num_threads 32 -out sprotein_blastresults.txt
#The resulting table was viewed from the bottom up using ultraedit
