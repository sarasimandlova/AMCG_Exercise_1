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

## Visualizing alignments

 For visualizing alignment i used command bellow: 
 
 `samtools tview --reference sequence.fasta -p NC_045512.2:23000 aligned.bam`
 
 ## Variant calling 
 
 For variant calling i used command bellow:

`bcftools mpileup -f sequence.fasta aligned.bam | bcftools call --ploidy 1 -mv -Ob -o varcall.bcf`

Using this command:

`bcftools view variants.bcf | cut -f 1-5 | grep -v "^#"`

I got this output:

```
NC_045512.2     241     .       C       T

NC_045512.2     913     .       C       T

NC_045512.2     3037    .       C       T

NC_045512.2     3267    .       C       T

NC_045512.2     5388    .       C       A

NC_045512.2     5986    .       C       T

NC_045512.2     6402    .       C       T

NC_045512.2     6954    .       T       C

NC_045512.2     9419    .       A       G

NC_045512.2     11287   .       GTCTGGTTTT      G

NC_045512.2     11291   .       G       A

NC_045512.2     11296   .       T       G

NC_045512.2     14408   .       C       T

NC_045512.2     14676   .       C       T

NC_045512.2     15279   .       C       T

NC_045512.2     16176   .       T       C

NC_045512.2     17697   .       A       C

NC_045512.2     21137   .       A       G

NC_045512.2     21764   .       ATACATGT        AT

NC_045512.2     21990   .       TTTATTA TTTA

NC_045512.2     22997   .       C       T

NC_045512.2     23063   .       A       T

NC_045512.2     23271   .       C       A

NC_045512.2     23403   .       A       G

NC_045512.2     23604   .       C       A

NC_045512.2     23709   .       C       T

NC_045512.2     24506   .       T       G

NC_045512.2     24914   .       G       C

NC_045512.2     25603   .       C       T

NC_045512.2     26690   .       G       T

NC_045512.2     27972   .       C       T

NC_045512.2     28048   .       G       T

NC_045512.2     28111   .       A       G

NC_045512.2     28280   .       G       C

NC_045512.2     28281   .       A       T

NC_045512.2     28282   .       T       A

NC_045512.2     28881   .       G       A

NC_045512.2     28882   .       G       A

NC_045512.2     28883   .       G       C

NC_045512.2     28977   .       C       T
```
