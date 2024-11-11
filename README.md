# VSEARCH

## Overview
VSEARCH is an open-source command-line tool used for sequence analysis and manipulation. It is similar to software such as DADA2 and mothur. Its architecture is based on the proprietary software USEARCH.

## Installation
It can be installed with `conda install bioconda::vsearch`

## Common VSEARCH Commands
The following are a few commands demonstrating how to use VSEARCH to process and analyze sequence data.

### Analyze Quality Scores
`--fastq_chars filename` gives the number of occurrences of each nucleotide base and of each quality score in _filename_. These data are output to the terminal. 

### Merge Paired-End Reads
`--fastq_mergepairs forward --reverse reverse` merges paired-end sequence reads into one sequence. This command outputs to the terminal the pairs that failed to merge and why. There are a number of options to control whether read pairs are merged or not. `--fastq_minovlen int` discards merge pairs with an overlap region fewer than _int_ bases. `--fastq_maxdiffs int` discards sequences with greater than _int_ differences in the overlap region.

### Generate Quality Report
Read quality can be further interrogated via `--fastq_eestats filename`. This command gives stats on the quality of each nucleotide position across all reads in _filename_. This generates a table of tab-separated columns. This columns include, principally, the distribution of quality scores, error probabilities, and expected accumulated errors at each position. 

### Filtering Sequences
`--fastq_filter filename` filters sequences based on given parameters. `--fastq_maxee float` discards sequences with an expected accumulated error greater than _float_. `--fastq_minlen int` discards sequences with a length less than _int_. Conversely, `--fastq_maxlen int` discards sequences with a length greater than _int_. `--fastq_maxns int` discards sequences with greater than _int_ ambiguous nucleotides. There are a number of other options to determine which sequences are kept. The number of sequences kept and discarded is displayed in the terminal.

### Dereplication
`--derep_fulllength filename` clusters sequences that are identical, and merges them together. This reduces the number of sequences present in the file. The `--sizeout` flag writes the abundance of each sequence to the output fasta file. `--minuniquesize int` can also be specified to discard any sequences that have an abundance less than _int_. The number of unique sequences (and the number of clusters discarded if `--minuniquesize` is specified) is output to the terminal.

### Chimera Detection
Chimera detection can be done denovo with `--uchime_denovo filename` or against a reference database `--uchime_ref filename`. Chimera detection is based on a scoring function controlled by a few options. Increasing `--dn int` or `--xn float` reduces the likelihood of tagging a sequence as a chimera. `--mindiffs int` corresponds to the minimum differences per segment. `--mindiv float` determines the minimum divergence from the parent. `--minh float` sets the minimum score, and increasing this value reduces false positives.

### Cluster
VSEARCH employs a single-pass, greedy centroid-based clustering algorithm. `--cluster_size` sorts by decreaseing sequence abundance beforehand, whereas `--cluster_fast` sorts by decreasing sequence length. `--id float` clusters sequences with _float_ percent identity to the centroid.
