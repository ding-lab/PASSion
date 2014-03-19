PASSion
===========
PASSion uses the mapped read in a pair as anchor and then uses a high resolution algorithm, 
pattern growth, to remap the proximal and distal fragments of the unmapped read to a local region of the reference
indicated by the mate. It is capable of identifying both known and novel canonical and non-canonical junctions 
with SNP or sequencing error tolerance. In addition, our package can discover differential and shared splicing 
patterns among multiple samples. 

Installation
============
 PASSION requires gcc >=4.3, SMALT, perl, and SAMtools to be pre-installed.

Go to PASSION directory to compile the component

	cd  path_to_passion/PASSION
	sh compile.sh

Go to SMALT directory, set the right binary version of smalt (according to your system)  smalt-0.5.7

	cp smalt_version smalt
	(example:) cp smalt_x86_64 smalt

Install Samtools

Set SMALT, SAMtools and PASSION directory to PATH

Index the Reference
-------------------
	smalt index -k 13 -s 6 refindex reference.fa
	samtools faidx reference.fa
	
Run PASSion
-----------
    passion.pl -s insert_size -r read1.fq -f read2.fq -R reference.fa -I refindex   

Find differential splicing patterns in multiple samples 

step1: edit a configure file. For example sample.txt 

	./s8_passion_output	s8
	./s1_passion_output	s1
	./s2_passion_output	s2
	
step2: run passion_diff.pl
	passion_diff.pl -f sample.txt

Example: discovery of junctions at chromosome 17 (sample.txt needs to be edited) 	
	cd  path_to_testset/testset
	smalt index -k 13 -s 6 17 17.fa
	samtools faidx 17.fa
	passion.pl -s 200 -r read1.50.fq -f read2.50.fq -R 17.fa -I 17 -o s1_passion_output
	passion.pl -s 300 -r read1.75.fq -f read2.75.fq -R 17.fa -I 17 -o s2_passion_output
	passion.pl -s 500 -r read1.100.fq -f read2.100.fq -R 17.fa -I 17 -o s8_passion_output
	passion_diff.pl -f sample.txt
	Install

LINK
-------
	https://trac.nbic.nl/passion/

