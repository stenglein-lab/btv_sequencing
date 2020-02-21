# btv_sequencing

This repository contains scripts used to generate consensus sequences for newly-sequenced bluetongue virus (BTV) isolates. 

The entry point to the pipeline is the `run_mapping_pipeline_one_sample` bash script, which runs a series of commands to 
generate consensus sequences for newly-sequenced bluetongue virus (BTV) isolates.

It assumes as input Illumina paired end data in 2 files named like this:

```
<isolate_name>_R1.fastq
<isolate_name>_R2.fastq
```

You pass in the `<isolate_name>` as a command line argument to the script

It works by mapping trimmed reads to a set of existing BTV reference sequences downloaded from Genbank
using bowtie2.  

It then uses the `identify_best_segments_from_sam` script to identify the best matching existing reference
sequence, which is defined as the reference sequence with the most reads aligned to it.  
It does this for all 10 segments.

It then uses a series of samtools and bcftools commands to create new consensus sequences for each of the
10 segments and finally remaps reads to these new draft consensus sequences.

Dependencies:

- bowtie2
- samtools
- bcftools
- the other scripts in this repository
- An existing set of btv reference sequences and associated bowtie2 index (also in this repo.).  Note that the fasta sequence names are pre-pended with their corresponding segment number E.g.: >s1_AY493686  is a segment 1 reference sequence with NCBI accession AY493686


Mark Stenglein, Dec, 2015


