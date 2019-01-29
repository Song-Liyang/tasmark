# tasmark
A Bioinformatic Toolkit for DNA Methylation Sequencing
v0.1.0 by Song Liyang

This program was written by Song Liyang (songly@pku.edu.cn), Peking University.
This program was built on source code from Bismark 0.2.0 by Felix Krueger.

## Installation
Download "tasmark" file and execute(don't forget "chmod +x") directly. Tasmark need Perl, Bowtie2 and Samtools.

USAGE: tasmark [options] <genome_folder> --index <index_name> {-1 <mates1> -2 <mates2> | <singles>}

<genome_folder>          The path to the folder containing the reference genome .fa or fa.gz
--index <index_name>     "path/to/bowtie2/index/your_basename" Tasmark will search for "your_basename.1.bt2".
                         Tasmark need existing bowtie2_builder index instead of extra "genome preparation" step.
<reads>                  Fasta file or fastQ file of single_end sequencing data.
-1 <reads1> -2 <reads2>  Fasta file or fastQ file of paired_end sequencing data.

-o                       Output directoy (current directoy default).
--multicore <int>        Run on multiple CPUs
--non_directional        Library prep with multiple rounds of random primming just after C->T conversion.

Other options is same to Bismark. Use --help for detail.

## Output
Bismark style .sam files with following info (tab separate).
  QNAME (seq-ID)
  FLAG (bowtie2 provid)
  RNAME (chromosome name)
  POS (start position)
  MAPQ (only calculated for Bowtie 2, always 255 for Bowtie)
  CIGAR
  RNEXT
  PNEXT
  TLEN
  SEQ (forward strand)
  QUAL (Phred33 scale)
  NM-tag (hemming distance to the reference)
  MD-tag (base-by-base mismatches to the reference)
  XM-tag (methylation call string,forward strand)
  XR-tag (read conversion state for the alignment,NN or CT or GA)
  XG-tag (genome conversion state for the alignment,NN)

For methylation call string (XM-tag), same like bismark.
  z - C in CpG context - unmethylated
  Z - C in CpG context - methylated
  x - C in CHG context - unmethylated
  X - C in CHG context - methylated
  h - C in CHH context - unmethylated
  H - C in CHH context - methylated
  u - C in Unknown context (CN or CHN) - unmethylated
  U - C in Unknown context (CN or CHN) - methylated
  . - not a C or irrelevant position
