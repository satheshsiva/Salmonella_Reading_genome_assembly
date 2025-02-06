Title:  "Genome assembly for 10 Salmonella Reading strains"
Author: "Sathesh K. Sivasankaran"
Date:   "Nov 27, 2019"
---
# Genome assembly of 10 Salmonella Reading strains

## Methods

### Plasmid finder.
All assembles genomes have more than one contig. It tells that there is high chance of observing extra-chromosomal DNAs (plasmids) in these strains. To identify the origin of these plasmids we have run Abricate.
```
module load abricate
abricate --db plasmidfinder SX430.fasta > abricate/SX439.txt

```  

### Prokka annotation.
Unicycler contigs were annotated using prokka bacterial genome annotation tool. I have made a virtual environment within conda to install Prokka.
```
# Command to make conda local environment.
conda create --name pan_genome
conda activate pan_genome

conda config --add channels r
conda config --add channels defaults
conda config --add channels conda-forge
conda config --add channels bioconda

# Install prokka
conda install -c conda-forge -c bioconda -c defaults prokka

# Run prokka
prokka --compliant --outdir SX439 --prefix SX439 --cpus 32 SX439.fasta
prokka --compliant --outdir SX440 --prefix SX440 --cpus 32 SX440.fasta
prokka --compliant --outdir SX441 --prefix SX441 --cpus 32 SX441.fasta
prokka --compliant --outdir SX442 --prefix SX442 --cpus 32 SX442.fasta
prokka --compliant --outdir SX443 --prefix SX443 --cpus 32 SX443.fasta
prokka --compliant --outdir SX444 --prefix SX444 --cpus 32 SX444.fasta
prokka --compliant --outdir SX445 --prefix SX445 --cpus 32 SX445.fasta
prokka --compliant --outdir SX446 --prefix SX446 --cpus 32 SX446.fasta
prokka --compliant --outdir SX447 --prefix SX447 --cpus 32 SX447.fasta
prokka --compliant --outdir SX448 --prefix SX448 --cpus 32 SX448.fasta
```

### Pangenome analysis.
Annotated genomes (\*.gff) were copied into new folder location for pan_genome analysis to identify gene level differences between strains.
```
conda activate pan_genome

# Install Roary
conda install roary

# Run roary
roary -p 32 -f Roar_Results -e -r -v *gff
```

### SNP analysis.
Finally, the SNP level differences between strain were analyzed using Snippy. Here, SX440 genome (SX440.gbk) used as a reference.
```
conda activate pan_genome

#Install Snippy
conda install -c conda-forge -c bioconda -c defaults snippy

#Run Snippy
snippy --cpus 32 --outdir SX439 --ref SX440.gbk --R1 SX439_merg_R1.fastq.gz --R2 SX439_merg_R2.fastq.gz
snippy --cpus 32 --outdir SX441 --ref SX440.gbk --R1 SX441_merg_R1.fastq.gz --R2 SX441_merg_R2.fastq.gz
snippy --cpus 32 --outdir SX442 --ref SX440.gbk --R1 SX442_merg_R1.fastq.gz --R2 SX442_merg_R2.fastq.gz
snippy --cpus 32 --outdir SX443 --ref SX440.gbk --R1 SX443_merg_R1.fastq.gz --R2 SX443_merg_R2.fastq.gz
snippy --cpus 32 --outdir SX444 --ref SX440.gbk --R1 SX444_merg_R1.fastq.gz --R2 SX444_merg_R2.fastq.gz
snippy --cpus 32 --outdir SX445 --ref SX440.gbk --R1 SX445_merg_R1.fastq.gz --R2 SX445_merg_R2.fastq.gz
snippy --cpus 32 --outdir SX446 --ref SX440.gbk --R1 SX446_merg_R1.fastq.gz --R2 SX446_merg_R2.fastq.gz
snippy --cpus 32 --outdir SX447 --ref SX440.gbk --R1 SX447_merg_R1.fastq.gz --R2 SX447_merg_R2.fastq.gz
snippy --cpus 32 --outdir SX448 --ref SX440.gbk --R1 SX448_merg_R1.fastq.gz --R2 SX448_merg_R2.fastq.gz
```
