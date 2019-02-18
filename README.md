# tasmark
A Bioinformatic Toolkit for DNA Methylation Sequencing  
v0.1.0 by Song Liyang  
https://github.com/Song-Liyang/tasmark  
This program was written by Song Liyang (songly@pku.edu.cn), Peking University.  
This program was built on source code from [Bismark 0.2.0](https://github.com/FelixKrueger/Bismark) by [Felix Krueger](https://github.com/FelixKrueger)  

## Usage
Download [tasmark](https://github.com/Song-Liyang/tasmark/blob/master/tasmark) file and execute(don't forget `chmod +x`) directly. Tasmark need `Perl`, [Bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/) and [Samtools](http://www.htslib.org/).  

USAGE: `tasmark [options] <genome_folder> --index <index_name> {-1 <mates1> -2 <mates2> | <singles>}`  

`<genome_folder>`  
    The path to the folder containing the reference genome `.fa` or `fa.gz`  

`--index <index_name>`  
    `path/to/bowtie2/index/your_basename` Tasmark will search for `your_basename.1.bt2`.Tasmark need existing bowtie2_builder index instead of extra "genome preparation" step.  

` <reads>`  or  `-1 <reads1> -2 <reads2>`  
    `fasta` file or `fastQ` file of single_end(read1 only) or paired_end sequencing data.  

`-o`    Output directoy (current directoy default).  
`--multicore <int>`   Run on multiple CPUs.  
`--non_directional`   Library prep with multiple rounds of random primming just after C->T conversion.  

Other options is almost same to `Bismark`. Use `--help` for detail.


## Output
Bismark style `sam` files with following info (tab separate).  

1.`QNAME` (seq-ID)  
2.`FLAG` ( `bowtie2` provid)  
3.`RNAME` (chromosome name)  
4.`POS` (start position)  
5.`MAPQ` (only calculated for Bowtie 2, always 255 for Bowtie)  
6.`CIGAR`  
7.`RNEXT`  
8.`PNEXT`  
9.`TLEN`  
10.`SEQ` (forward strand)  
11.`QUAL` (Phred33 scale)  
12.`NM-tag` (hemming distance to the reference)  
13.`MD-tag` (base-by-base mismatches to the reference)  
14.`XM-tag` (methylation call string,forward strand)  
15.`XR-tag` (read conversion state for the alignment,`NN` , `CT` or `GA`)  
16.`XG-tag` (genome conversion state for the alignment, always`NN`)  

For methylation call string (`XM-tag`), same like `Bismark`.  
*  z - C in CpG context - unmethylated  
*  Z - C in CpG context - methylated  
*  x - C in CHG context - unmethylated  
*  X - C in CHG context - methylated  
*  h - C in CHH context - unmethylated  
*  H - C in CHH context - methylated  
*  u - C in Unknown context (CN or CHN) - unmethylated  
*  U - C in Unknown context (CN or CHN) - methylated  
*  . - not a C or irrelevant position  

tasmark_methylation_extractor
extract methylation call to bed file, same function in bismark.
usage:
`./tasmark_methylation_extractor yoursample.sam `  
use `--bedgraph` to make a cov file (make sure tasmark2bedGraph has been downloaded).
