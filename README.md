## ddSeeker
A tool for processing single cell RNA-seq ddSEQ data.

### Description
**ddSeeker** identifies cellular and molecular identifiers from single cell RNA sequencing experiments.

Users must provide one unmapped BAM file
[(uBAM)](https://gatkforums.broadinstitute.org/gatk/discussion/11008/ubam-unmapped-bam-format)
from a paired-end read experiment and a text file with a set of barcode blocks,
one per line (if you don't have such file run `ddSeeker_barcodes.py` to generate one).

The program returns a new unmapped BAM file with tagged reads.

### Notes
- FASTQ files can be converted using [picard FastqToSam](https://broadinstitute.github.io/picard/command-line-overview.html#FastqToSam).
- **ddSeeker** [tags](https://genome.sph.umich.edu/wiki/SAM#What_are_TAGs.3F)
  are "XB" and "XU" for cell and molecular identifiers respectively, and "XE" 
  to highlight why the identification has failed.
- Use `-s/--summary` to generate a summary of unique barcodes
  and error count.
- By default **ddSeeker** outputs to stdout: use `-o` to specify output file name.

### Examples
#### Generate barcodes files
    ddSeeker_barcodes.py *.bam

#### Convert Fastq with Picard
    java -jar picard.jar FastqToSam F1=read1.fastq.gz F2=read2.fastq.gz O=unmapped.bam SORT_ORDER=queryname

#### Run ddSeeker
    ddSeeker.py unmapped.bam -o tagged.bam -s unmapped_summary -n 10

#### Run full ddSeeker-"drop-seq tools" pipeline
    ddSeeker_alignment.sh [options] unmapped.bam

### Dependencies
- [Python](https://www.python.org/downloads/release/python-365/) (>= 3.5)
- [Biopython](http://biopython.org/wiki/Download) (>= 1.71)
- [pysam](https://pysam.readthedocs.io/en/latest/index.html) (>= 0.14)
- [Drop-seq_tools](http://mccarrolllab.com/dropseq/) (>= 1.13)
- [STAR](https://github.com/alexdobin/STAR) (>= 2.5)
