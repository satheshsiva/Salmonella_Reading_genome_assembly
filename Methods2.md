Title:  "Genome assembly for 10 Salmonella Reading strains"
Author: "Sathesh K. Sivasankaran"
Date:   "Nov 27, 2019"
---
# Genome assembly of 10 Salmonella Reading strains

## Methods
### Genome assembly.
Genome assembly was performed using two different toolkits parallelly.
1. Unicycler (https://github.com/rrwick/Unicycler). Here, both short and long reads were submitted together for assembly.
```
unicycler-runner.py -1 ../SRA/SRR5045041_1.fastq.gz -2 ../SRA/SRR5045041_2.fastq.gz -l ../1_5/barcode01.fastq -o ../unicyc/SX440/ -t 38
unicycler-runner.py -1 ../SRA/SRR5139868_1.fastq.gz -2 ../SRA/SRR5139868_2.fastq.gz -l ../1_5/barcode02.fastq -o ../unicyc/SX442/ -t 38
unicycler-runner.py -1 ../SRA/SRR8832242_1.fastq.gz -2 ../SRA/SRR8832242_2.fastq.gz -l ../1_5/barcode03.fastq -o ../unicyc/SX444/ -t 38
unicycler-runner.py -1 ../SRA/SRR8865139_1.fastq.gz -2 ../SRA/SRR8865139_2.fastq.gz -l ../1_5/barcode04.fastq -o ../unicyc/SX445/ -t 38
unicycler-runner.py -1 ../SRA/SRR8856823_1.fastq.gz -2 ../SRA/SRR8856823_2.fastq.gz -l ../1_5/barcode05.fastq -o ../unicyc/SX448/ -t 38
unicycler-runner.py -1 ../SRA/SRR5043211_1.fastq.gz -2 ../SRA/SRR5043211_2.fastq.gz -l ../6_10/barcode06.fastq -o ../unicyc/SX439/ -t 38
unicycler-runner.py -1 ../SRA/SRR5125747_1.fastq.gz -2 ../SRA/SRR5125747_2.fastq.gz -l ../6_10/barcode07.fastq -o ../unicyc/SX441/ -t 38
unicycler-runner.py -1 ../SRA/SRR5221896_1.fastq.gz -2 ../SRA/SRR5221896_2.fastq.gz -l ../6_10/barcode08.fastq -o ../unicyc/SX443/ -t 38
unicycler-runner.py -1 ../SRA/SRR8841067_1.fastq.gz -2 ../SRA/SRR8841067_2.fastq.gz -l ../6_10/barcode09.fastq -o ../unicyc/SX446/ -t 38
unicycler-runner.py -1 ../SRA/SRR8841130_1.fastq.gz -2 ../SRA/SRR8841130_2.fastq.gz -l ../6_10/barcode10.fastq -o ../unicyc/SX447/ -t 38
```
Unicycler does jobs including assembly (long reads), polishing (SNP error correction using short reads) and rotate the genome to origin of replication site. It is very nice a single tool can do all necessary jobs in genome assembly process. We have to do all these jobs successively if we use "canu", eg polishing step is performed by "pylon" which I have explained below.

2. Assembly using "canu".
```
canu -p SX440 -d canu/SX440/  -nanopore-raw 1_5/barcode01.fastq -genomeSize=5m
canu -p SX442 -d canu/SX442/  -nanopore-raw 1_5/barcode02.fastq -genomeSize=5m
canu -p SX444 -d canu/SX444/  -nanopore-raw 1_5/barcode03.fastq -genomeSize=5m
canu -p SX445 -d canu/SX445/  -nanopore-raw 1_5/barcode04.fastq -genomeSize=5m
canu -p SX448 -d canu/SX448/  -nanopore-raw 1_5/barcode05.fastq -genomeSize=5m
canu -p SX439 -d canu/SX439/  -nanopore-raw 6_10/barcode06.fastq -genomeSize=5m
canu -p SX441 -d canu/SX441/  -nanopore-raw 6_10/barcode07.fastq -genomeSize=5m
canu -p SX443 -d canu/SX443/  -nanopore-raw 6_10/barcode08.fastq -genomeSize=5m
canu -p SX446 -d canu/SX446/  -nanopore-raw 6_10/barcode09.fastq -genomeSize=5m
canu -p SX447 -d canu/SX447/  -nanopore-raw 6_10/barcode10.fastq -genomeSize=5m
```

In general, contigs generated using long reads have many SNPs due to high error rate from Nanopore reads. To reduce the error contigs were polished using "Pilon" by give short reads as a reference. Short reads were mapped to contigs using BWA, then mapped reads were used as reference for polish. Idea is the repeat the polished process until no changes were observed in the \*.changes file (Pilon summary output).
```
module load python_3
module load samtools
module load pilon
module load quast
module load circlator

bwa index SX439.contigs.fasta
bwa mem -t 38 SX439.contigs.fasta ../../SRA/SRR5043211_1.fastq.gz ../../SRA/SRR5043211_2.fastq.gz | samtools sort > aln.bam
samtools index aln.bam
java -jar /software/7/apps/pilon/1.23/pilon-1.23.jar --genome SX439.contigs.fasta --frags aln.bam --output pil1SX439 --fix bases --changes --verbose

bwa index pil1SX439.fasta
bwa mem -t 38 pil1SX439.fasta ../../SRA/SRR5043211_1.fastq.gz ../../SRA/SRR5043211_2.fastq.gz | samtools sort > aln1.bam
samtools index aln1.bam
java -jar /software/7/apps/pilon/1.23/pilon-1.23.jar --genome pil1SX439.fasta --frags aln1.bam --output pil2SX439 --fix bases --changes --verbose

bwa index pil2SX439.fasta
bwa mem -t 38 pil2SX439.fasta ../../SRA/SRR5043211_1.fastq.gz ../../SRA/SRR5043211_2.fastq.gz | samtools sort > aln2.bam
samtools index aln2.bam
java -jar /software/7/apps/pilon/1.23/pilon-1.23.jar --genome pil2SX439.fasta --frags aln2.bam --output pil3SX439 --fix bases --changes --verbose
wc *.changes

circlator all --assembler canu --merge_min_id 85 --merge_breaklen 1000 pil3SX439.fasta SX439.trimmedReads.fasta.gz CIR/ --threads 32
cd CIR/

bwa index pil3cirpil3SX439.fasta
bwa mem -t 38 pil3cirpil3SX439.fasta ../../../FSEP/SX439_R1.fq.gz ../../../FSEP/SX439_R2.fq.gz | samtools sort > aln3.bam
samtools index aln3.bam
java -jar /software/7/apps/pilon/1.23/pilon-1.23.jar --genome pil3cirpil3SX439.fasta --frags aln3.bam --output pil4cirpil3SX439 --fix bases --changes --verbose

bwa index pil4cirpil3SX439.fasta
bwa mem -t 38 pil4cirpil3SX439.fasta ../../../FSEP/SX439_R1.fq.gz ../../../FSEP/SX439_R2.fq.gz | samtools sort > aln4.bam
samtools index aln4.bam
java -jar /software/7/apps/pilon/1.23/pilon-1.23.jar --genome pil4cirpil3SX439.fasta --frags aln4.bam --output pil5cirpil3SX439 --fix bases --changes --verbose

bwa index pil5cirpil3SX439.fasta
bwa mem -t 38 pil5cirpil3SX439.fasta ../../../FSEP/SX439_R1.fq.gz ../../../FSEP/SX439_R2.fq.gz | samtools sort > aln5.bam
samtools index aln5.bam
java -jar /software/7/apps/pilon/1.23/pilon-1.23.jar --genome pil5cirpil3SX439.fasta --frags aln5.bam --output pil6cirpil3SX439 --fix bases --changes --verbose
wc *.changes

```

Finally, contigs from both Canu and Unicycler were compared for the assembly quality. MiSeq short reads were mapped to contigs from both tools using BWA. Then the quality of the assemblies were checked. It seems like Unicycler assemblies have better quality compared to Canu. So, I am going to continue downstream process using contigs from Unicycler results.
