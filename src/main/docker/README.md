### RNApeg 2.6.0

RNApeg is an RNA junction calling, correction, and quality-control package.  Its use is discussed in this paper:

https://rnajournal.cshlp.org/content/24/8/1056.short

Invoke the RNApeg wrapper as 
```
RNApeg.sh [-h] -b bamfile -r refflat -f fasta
```
Where
* -b is a BAM file of transcriptome reads mapped to whole-genome coordinates
* -r is an uncompressed refFlat.txt file from the UCSC genome annotation database
* -f is a FASTA file with a .fai-format index (generated by "samtools faidx genome.fa")

See 'Downloading reference files' to learn how you can obtain the most up to date reference files.

### Output

Output is written in the Docker container to the directory /results.  This path  must be mounted at runtime, i.e. either to a volume or bind-mounted to a directory on your local computer.

### Example

The following example:

* mounts the volume "myvolume" to "/results", where output file will be written
* bind-mounts the local PC directory /c/Users/myuid/docker_rnapeg to /mny/mydata in the counter
* specifies refFlat and genome files stored on the PC

```
docker run --mount source=myvolume,target=/results -v /c/Users/myuid/docker_rnapeg:/mnt/mydata rnapeg RNApeg.sh -g GRCh37-lite -b /mnt/mydata/demo/rna_demo_TP53.bam -r /mnt/mydata/refFlat.txt -f /mnt/mydata/reference/Homo_sapiens/GRCh37-lite/FASTA/GRCh37-lite.fa
```

### Docker notes
* This software was originally written to run in a cluster computing environment, and has substantial RAM requirements (~8+ gb, still TBD).  On a PC, the Docker virtual machine memory allocation almost certainly needs to be increased from the default values.  Use of a computer with 16 gb of RAM is recommended, an 8 gb system may not be sufficient.

### Dependencies

* [GNU parallel](https://www.gnu.org/software/parallel/)
* [Picard 2.6.0](https://github.com/broadinstitute/picard/releases/tag/2.6.0)
* Java 1.8.0
* Perl 5.10.1 with libraries:
    - [Data::Compare](https://metacpan.org/pod/Data::Compare)
    - [DBI](https://metacpan.org/pod/DBI)

### Downloading reference files

The [UCSC genome annotation database](http://hgdownload.cse.ucsc.edu/goldenPath/hg19/database/) provides genomic mappings of NCBI refSeq transcripts for various genomes.  The refFlat file for hg19 is:

http://hgdownload.cse.ucsc.edu/goldenPath/hg19/database/refFlat.txt.gz

This file must be decompressed before use.

### To Do
* provide copy of RNApeg wiki docs?
