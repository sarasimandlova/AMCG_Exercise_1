## Exercise 1: Sars-CoV-2 Lineage Determination

I downloaded the [FASTA file ]( https://www.ncbi.nlm.nih.gov/nuccore/NC_045512.2?report=fasta ).

I installed the bwa package:

`sudo apt install bwa`

I indexed the reference as follows: 

`bwa index sequence.fasta`

I then downloaded the reference genome using the `wget` command:

`wget https://gear.embl.de/data/.slides/Plate42B2.R2.fastq.gz`


## Align to the reference

`bwa mem sequence.fasta Plate42B2.R1.fastq.gz Plate42B2.R2.fastq.gz | samtools sort -o aligned.bam -`

I indexed the bam file using this command:

`samtools index aligned.bam`
