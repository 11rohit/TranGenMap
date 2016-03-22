# TranGenMap

An attempt to map the denovo transcripts to the denovo genome in-order to find chimeric regions of the genome. The limitation being that the transcript itself must not be Chimeric.


I. Mapping of the Transcripts onto the genome
1) Just take the longest transcript from an isoformic group and then use GMP-GSNAP to map the transcript onto the genome. A simple bash script can be used to remove the redundancy from the whole list of transcripts.

2) Make an index of the genome from the species with gmap_index.

3) Align the longest transcripts to the genome with gmap at high identity, look for single path in the beginning (n=1) so that we do not make errors either from the low identity regions due to sequencing errors in genome/transcriptome OR the multiple paths of the transcripts which are due to paralogs or duplications.

4) We have to look into the transcripts which have no paths from n=1, since thse might be chimeric or low identity ones due to sequencing errors.

5) Extract the transcript sequences for those with no paths using the log-file of the mapping step - use shell script for extracting names and support from samtools for sequences.

6) Re-map the ones with no paths at low identities at n=1 (since our genome assembly is from PacBio we expect it to be 80% but we use 70 to be least stringent), if there are paths available then the sequencing errors might be the culprit.

7) For those after the step 6 with no paths, go for low identity alignments with chimeric option n=0 of GMAP.

