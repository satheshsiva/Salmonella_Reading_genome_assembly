---
Title:  "Genome assembly for 10 Salmonella Reading strains"
Author: "Sathesh K. Sivasankaran"
Date:   "Nov 27, 2019"
---
# Genome assembly of 10 Salmonella Reading strains

## Methods

### Fetching FSIS Illumina short reads from SRA.
SRA ids for each strain were obtained form Shawn. Files were downloaded to local system using SRA-ToolKit (https://www.ncbi.nlm.nih.gov/sra/docs/toolkitsoft/). Finally, files were downloaded and formatted to fastq format.

```
prefetch -v SRR5043211
fastq-dump --outdir /home/sathesh/Documents/Reading_Assem/SRA/ --split-files /home/sathesh/Documents/SRA/sra/SRR5043211.sra --gzip
```
Reads were stored in location: //.

### In-house short and long sequenced reads.
MiSeq short reads: //.
Nanopore long reads: //.

### Sequence QC.
The quality of the sequenced read sets (FSIS short, inhouse short and long) were analyzed using FastQC (version v0.11.8) [https://www.bioinformatics.babraham.ac.uk/projects/fastqc/]. Jobs were submitted in SciNet using below mentioned bash script which uses the parallel function.
For long Nanopore reads, FastQC was run on both before and after demultiplexing steps. For FastQC, jobs were submitted in SciNet using below mentioned bash script which uses the parallel function.

```
module purge
module load fastqc
module load parallel
parallel -j 7 "fastqc {} -t 5 -o FQC/1-5/" ::: 1394/1394_1-5/20190815_1545_GA10000_FAK20224_452920c1/fastq_pass/*.fastq
parallel -j 7 "fastqc {} -t 5 -o FQC/6-10/" ::: 1394/1394_6-10/20190815_1545_GA20000_FAK11356_7c955fe5/fastq_pass/*.fastq
```

The FastQC results are located: -----.  
Results were stored in one location and combined using MultiQC (https://multiqc.info/) using the below mentioned command. MultiQC results can be viewed in attached HTML files: Notebook/Lane1_FQC.html, /Lane2_FQC.html and /Lane3_FQC.html (please download the html file alone with the supporting folder to view the results).

```
module load python_2
multiqc .
```

### Demultiplexing.
Long Nanopre reads were demultiplex using qcat (https://github.com/nanoporetech/qcat).
```
cat 1394/1394_1-5/20190815_1545_GA10000_FAK20224_452920c1/fastq_pass/*.fastq | qcat -b 1_5/ --trim
Adapters detected in 1081672 of 1137149 reads
  NBD104/NBD114 1081672: |  ################### |  95.12 %
           none  47736: |                      |   4.20 %
Barcodes detected in 1081672 of 1137149 adapters
      barcode01 143052: |                   ## |  12.58 %
      barcode02 210241: |                  ### |  18.49 %
      barcode03 181589: |                  ### |  15.97 %
      barcode04 246529: |                 #### |  21.68 %
      barcode05 299680: |                ##### |  26.35 %
      barcode06     88: |                      |   0.01 %
      barcode07    108: |                      |   0.01 %
      barcode08     83: |                      |   0.01 %
      barcode09    169: |                      |   0.01 %
      barcode10     81: |                      |   0.01 %
      barcode12      1: |                      |   0.00 %
      barcode13      8: |                      |   0.00 %
      barcode14      2: |                      |   0.00 %
      barcode15     17: |                      |   0.00 %
      barcode16     14: |                      |   0.00 %
      barcode18      2: |                      |   0.00 %
      barcode20      4: |                      |   0.00 %
      barcode22      1: |                      |   0.00 %
      barcode23      2: |                      |   0.00 %
      barcode24      1: |                      |   0.00 %
           none  47736: |                      |   4.20 %
7741 reads were skipped due to the min. length filter.
```
```
cat 1394/1394_6-10/20190815_1545_GA20000_FAK11356_7c955fe5/fastq_pass/*.fastq | qcat -b 6_10/ --trim
Adapters detected in 1142277 of 1198093 reads
  NBD104/NBD114 1142277: |  ################### |  95.34 %
           none  55775: |                      |   4.66 %
Barcodes detected in 1142277 of 1198093 adapters
      barcode01     32: |                      |   0.00 %
      barcode02     11: |                      |   0.00 %
      barcode03      2: |                      |   0.00 %
      barcode05     12: |                      |   0.00 %
      barcode06 194201: |                  ### |  16.21 %
      barcode07 191506: |                  ### |  15.98 %
      barcode08 194161: |                  ### |  16.21 %
      barcode09 363899: |               ###### |  30.37 %
      barcode10 198398: |                  ### |  16.56 %
      barcode11      1: |                      |   0.00 %
      barcode12      1: |                      |   0.00 %
      barcode13      6: |                      |   0.00 %
      barcode14      3: |                      |   0.00 %
      barcode15     11: |                      |   0.00 %
      barcode16      2: |                      |   0.00 %
      barcode17      8: |                      |   0.00 %
      barcode18      6: |                      |   0.00 %
      barcode19      2: |                      |   0.00 %
      barcode20      1: |                      |   0.00 %
      barcode21      8: |                      |   0.00 %
      barcode22      6: |                      |   0.00 %
           none  55775: |                      |   4.66 %
41 reads were skipped due to the min. length filter.
```

Short reads from FSIS and in-house were merged into one file. 
