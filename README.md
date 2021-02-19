# SARS-CoV-2
Sequences and Tools for dealing with SARS-CoV-2

This is a blastn database created from cogconsortium.uk 
on Thursday February 18 before 6PM Pacific Time.

The following commands were used after loading all_sequences 
from the database:

cp /Downloads/cog_all.fasta /Volumes/SATA/SARS-CoV-2_cogconsortium
 
cd /Volumes/SATA/SARS-CoV-2_cogconsortium
# Use Brian Bushnell's famous bbmap ("bbmap can do that!") to clean the sequences
/Users/bgold/bbmap/reformat.sh in=cog_all.fasta out=trimmed_cog_all.fasta trd=t tossjunk
#####
#####java -ea -Xms300m -cp /Users/bgold/bbmap/current/ jgi.ReformatReads in=cog_all.fasta out=trimmed_cog_all.fasta trd=t tossjunk
#####Executing jgi.ReformatReads [in=cog_all.fasta, out=trimmed_cog_all.fasta, trd=t, tossjunk]
#####
#####Input is being processed as unpaired
#####Input:                  	271789 reads          	8122383081 bases
#####Low quality discards:   	7654 reads (2.82%) 	228884545 bases (2.82%)
#####Output:                 	264135 reads (97.18%) 	7893498536 bases (97.18%)
#####
#####Time:                         	82.103 seconds.
#####Reads Processed:        271k 	3.31k reads/sec
#####Bases Processed:       8122m 	98.93m bases/sec
/Users/bgold/ncbi-blast/bin/makeblastdb -in trimmed_cog_all.fasta -parse_seqids -title "SARS-CoV-2 GOGCONSORTIUM 02182021" -dbtype nucl
#####Building a new DB, current time: 02/18/2021 17:34:50
#####New DB name:   /Volumes/SATA/SARS-CoV-2_cogconsortium/trimmed_cog_all.fasta
#####New DB title:  SARS-CoV-2 GOGCONSORTIUM 02182021
#####Sequence type: Nucleotide
#####Deleted existing Nucleotide BLAST database named /Volumes/SATA/SARS-CoV-2_cogconsortium/trimmed_cog_all.fasta
#####Keep MBits: T
#####Maximum file size: 1000000000B
#####Adding sequences from FASTA; added 264135 sequences in 230.318 seconds.
#
# To Run, invoke:
blastn -query probe.fasta -db clean.dec22.fasta -out results.txt

