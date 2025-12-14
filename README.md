# BIOL59500 Introduction to Bioinformatics

Tiffany Lin lin2208@purdue.edu

This repository contains materials for **Purdue University BIOL 59500 – Introduction to Bioinformatics**, including **extra credit programming projects**.

## Programming Projects

### Installation / Requirements

Tested on **macOS** with **Python 3.12.4**.

Install Biopython (Cock et al., 2009):
```bash
python3 -m pip install --upgrade pip
python3 -m pip install biopython
python3 -c "import Bio; print(Bio.__version__)"
```

### [PP1: DNA–Protein Alignment (40-55 pts)](https://github.itap.purdue.edu/lin2208/biol595_Bioinformatics/tree/main/pp1)
**Program Project 1** implements a DNA–protein alignment pipeline using translated reading frames and local alignment (Smith–Waterman).  
The project demonstrates frame detection, biologically meaningful scoring with BLOSUM62, and paired-line alignment output of amino acids and DNA codons. 

**Contents:**
```
pp1/
├── cds_data.md      # Data Acquisition information write-up and explanation
├── pp1.ipynb        # Python code for translation, alignment, and frame validation
└── data/
    ├── real_cds.fa
    ├── real_protein.fa
    ├── GCF_000005845.2_ASM584v2_cds_from_genomic.fna
    ├── GCF_000005845.2_ASM584v2_protein.faa
    └── BLOSUM62.txt
```
### [PP3: Sequence Randomization (20-40 pts)](https://github.itap.purdue.edu/lin2208/biol595_Bioinformatics/tree/main/pp3)

**Contents:**
```

```
## References
Cock PA, Antao T, Chang JT, Chapman BA, Cox CJ, Dalke A, Friedberg I, Hamelryck T, Kauff F, Wilczynski B and de Hoon MJL (2009) Biopython: freely available Python tools for computational molecular biology and bioinformatics. Bioinformatics, 25, 1422-1423
