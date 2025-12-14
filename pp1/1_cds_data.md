# Selection of Real CDS and Protein Sequences from NCBI RefSeq

## Introduction

The goal of this project is to align a DNA sequence to a protein sequence based on translation and forward reading-frame detection. To ensure that the alignment reflects true biological coding structure rather than random sequence artifacts, a biologically annotated coding sequence was used after we test the small artificial ~50 bp sequence.

### Why use a coding DNA sequence (CDS)?

**Using an arbitrary genomic DNA sequence would introduce large non-coding regions, frequent premature stop codons, and frame disruptions that are unrelated to the alignment method itself.** These features would confound interpretation of alignment scores and obscure true reading-frame signals.

Therefore, we specifically use a **coding DNA sequence (CDS)**. A CDS is a contiguous nucleotide region that encodes a functional protein and is annotated with a defined start codon, reading frame, and stop codon. Using a CDS ensures that:
- Exactly one forward reading frame corresponds to the true protein
- Alternative frames contain frequent stop codons or mismatches
- Differences in alignment scores across frames reflect real frame structure rather than noise

### Biological data source

To ensure biological validity and reproducibility, the CDS and its corresponding protein sequence were obtained from the **NCBI RefSeq database**, which provides curated and consistently annotated reference sequences.

The real-data test case I chose is from a CDS–protein pair from the bacterium *E. coli* K-12 substr. MG1655:
- Organism: *E. coli* K-12 substr. MG1655
- Domain: Bacteria
- Database: NCBI RefSeq genome assembly
- Assembly accession: GCF_000005845.2
- Gene: *thrL* (thr operon leader peptide)
- Protein accession: NP_414542.1

**CDS data were obtained from:** https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/

FYI: You can choose any other CDS sequence for testing. The same workflow can be applied to any RefSeq CDS–protein pair by selecting a different CDS entry and extracting the corresponding protein sequence using its RefSeq accession.

### Download data from bash terminal
```bash
# change to your own path
cd /Users/rusher/Desktop/biol595_extra_credit/pp1/data 
curl -L -O https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_cds_from_genomic.fna.gz
curl -L -O https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_protein.faa.gz

file GCF_000005845.2_ASM584v2_cds_from_genomic.fna.gz
file GCF_000005845.2_ASM584v2_protein.faa.gz

gunzip -f GCF_000005845.2_ASM584v2_cds_from_genomic.fna.gz
gunzip -f GCF_000005845.2_ASM584v2_protein.faa.gz
```

### Extract 1 CDS sequence and corresponding protein sequence
The RefSeq CDS FASTA file contains thousands of coding sequences from the genome assembly, corresponding to many different genes. Because this project focuses on validating translation-based alignment and reading-frame detection, **a single, well-annotated CDS–protein pair** was selected for analysis rather than using the entire dataset.

To ensure that the selected sequence was biologically interpretable and suitable for presentation in a report, the following criteria were applied:

1.	not partial (avoid truncated sequences)
2.	not hypothetical protein (avoid unclear annotation)
3.	reasonable length for your report (not too tiny, not insanely long)
4.	has a clear protein_id=NP_… in the header 

Write it into `real_cds.fa`


```bash
awk '
  BEGIN{RS=">"; ORS=""}
  NR>1 {
    split($0, a, "\n");
    header=a[1];
    if (header !~ /partial/ && header !~ /hypothetical protein/) {
      print ">"$0;
      exit
    }
  }
' GCF_000005845.2_ASM584v2_cds_from_genomic.fna > real_cds.fa
```
Check the CDS header
```bash
# print out check
head -n 1 real_cds.fa
```
From this header, the RefSeq protein accession number was parsed using a regular expression:
```bash
ACC=$(head -n 1 real_cds.fa | grep -oE 'WP_[0-9]+\.[0-9]+|NP_[0-9]+\.[0-9]+|YP_[0-9]+\.[0-9]+')
echo "$ACC"
```
This accession was then used to extract the **corresponding protein sequence** from the RefSeq protein FASTA file, ensuring that the DNA and protein sequences represent the same gene product, and we write it to `real_protein.fa`
```bash
awk -v acc="NP_414542.1" '
  BEGIN{p=0}
  /^>/ {
    if ($0 ~ acc) {p=1; print; next}
    else if (p==1) {exit}
  }
  p==1 {print}
' GCF_000005845.2_ASM584v2_protein.faa > real_protein.fa
```
Finally, the protein FASTA file was checked to confirm that exactly one protein sequence was extracted
```bash
head -n 2 real_protein.fa
grep -c "^>" real_protein.fa # should return 1
```
This guarantees that the CDS and protein sequences used in subsequent analyses are biologically matched, fully annotated, and suitable for evaluating translation-based DNA–protein alignment and reading-frame selection.
