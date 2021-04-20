# Background

Complete phasing using Hi-C data is sometimes difficult owing to the low genetic divergence between haplotypes. For example, ALLHiC might group homologous contigs into a big cluster (Fig. 1a). Although these contigs could be further adjusted manually, the placement of small contigs is always boring and time-consuming (Fig. 1b).

![Fig1](https://github.com/zengxiaofei/small-contig-repartition/blob/master/figs/Fig1.jpg)

# Aim & Strategy

Here is a simple strategy to reassign these small contigs after manual grouping (see Fig. 2a): (1) just remove small contigs using ` remove_small_contigs.py` provided in this repo; (2) run `ALLHiC_rescue` to rescue removed contigs (reassignment); (3) run `allhic optimize` to determine the ordering and orientation.

This strategy may also have the poteintial for general global refinement.

![Fig2](https://github.com/zengxiaofei/small-contig-repartition/blob/master/figs/Fig2.jpg)

# Result

As shown in Fig. 1c, after running this pipeline, further manual work is dramatically reduced.

# Usage of `remove_small_contigs.py`

## Help message:

```Bash
$ ./remove_small_contigs.py -h
usage: remove_small_contigs.py [-h] [--fasta FASTA] [--counts COUNTS]
                               [--len_cutoff LEN_CUTOFF]
                               assembly

positional arguments:
  assembly              *.review.assembly (output file of juicebox manual
                        grouping), used to generate new prunning.clusters.txt

optional arguments:
  -h, --help            show this help message and exit
  --fasta FASTA         input fasta file of contigs, this parameter will
                        remove contigs not in .review.assembly, optional
  --counts COUNTS       input prunning.counts_RE.txt, this parameter will
                        remove contigs not in .review.assembly, optional
  --len_cutoff LEN_CUTOFF
                        length cutoff, default: 100 Kbp
```

## Command:

```Bash
$ ./remove_small_contigs.py groups.manual.review.assembly --fasta seq.fasta --counts prunning.counts_GATC.txt
```

