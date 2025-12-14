# BIOL59500 Introduction to Bioinformatics

Tiffany Lin lin2208@purdue.edu

This repository contains materials for **BIOL 59500 – Introduction to Bioinformatics**, including **extra credit programming projects**.

## Programming Projects

### [PP1: DNA–Protein Alignment](https://github.itap.purdue.edu/lin2208/biol595_Bioinformatics/tree/main/pp1)
**Program Project 1** implements a DNA–protein alignment pipeline using translated reading frames and local alignment (Smith–Waterman).  
The project demonstrates frame detection, biologically meaningful scoring with BLOSUM62, and paired-line alignment output of amino acids and DNA codons. 

**Contents:**
> pp1/
├── report.md        # Project write-up and explanation
├── pp1.ipynb        # Python code for translation, alignment, and frame validation
└── data/
    ├── real_cds.fa
    ├── real_protein.fa
    ├── GCF_000005845.2_ASM584v2_cds_from_genomic.fna
    ├── GCF_000005845.2_ASM584v2_protein.faa
    └── BLOSUM62.txt

