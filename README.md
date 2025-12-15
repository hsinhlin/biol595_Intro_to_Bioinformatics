# BIOL59500 Introduction to Bioinformatics

Tiffany Lin lin2208@purdue.edu

This repository contains materials for **Purdue University BIOL 59500 – Introduction to Bioinformatics**, including **extra credit programming projects**.

Last Update: Dec 15th, 2025

## Programming Projects

### Installation / Requirements

Tested on **macOS** with **Python 3.12.4**.

**Requirements**
- Python 3.8 or newer
- Biopython

Install Biopython (Cock et al., 2009):
```bash
python3 -m pip install --upgrade pip
python3 -m pip install biopython
python3 -c "import Bio; print(Bio.__version__)"
```
---
### [PP1: DNA–Protein Alignment (40-55 pts)](https://github.itap.purdue.edu/lin2208/biol595_Bioinformatics/tree/main/pp1)
**Program Project 1** implements a DNA–protein alignment pipeline using translated reading frames and local alignment (Smith–Waterman).  
The project demonstrates frame detection, biologically meaningful scoring with BLOSUM62, and paired-line alignment output of amino acids and DNA codons. 

**How to run**
- Open `pp1/pp1.ipynb` and run all cells from top to bottom.
- The notebook performs DNA–protein alignment using translated reading frames.
- `cds_data.md` documents how the CDS and protein sequences were obtained and prepared.
- Input FASTA test files are provided in `pp1/data/`.

**Contents:**
```
pp1/
├── cds_data.md      # Data Acquisition information write-up and explanation
├── pp1.ipynb        <- report + code 
└── data/
    ├── real_cds.fa
    ├── real_protein.fa
    ├── GCF_000005845.2_ASM584v2_cds_from_genomic.fna
    ├── GCF_000005845.2_ASM584v2_protein.faa
    └── BLOSUM62.txt
```
---
### [PP3: Sequence Randomization (20-40 pts)](https://github.itap.purdue.edu/lin2208/biol595_Bioinformatics/tree/main/pp3)
**Program Project 3** implements sequence randomization with and without exact k-mer preservation.  
A sampling shuffle is compared to an Euler/De Bruijn graph method that guarantees identical k-mer counts.

**How to run**
- Open `pp3/pp3.ipynb` and run all cells from top to bottom.
- The notebook will prompt for a k-mer size `k` (demo: `k = 5`).
- Input FASTA test files are provided in `pp3/data/`.

**Expected results (for k ≥ 2)**
- Sampling shuffle: `Exact k-mer match (sampling)? False`
- Euler/De Bruijn method: `Exact k-mer match (Euler)? True`

(Only the first 60 characters of each randomized sequence are printed for readability; k-mer comparisons use the full sequence.)

**Contents:**
```
pp3/
├── pp3.ipynb   ← report + code
└── data/
    ├── real_protein.fa
    └── real_cds.fa
```
## References
Cock PA, Antao T, Chang JT, Chapman BA, Cox CJ, Dalke A, Friedberg I, Hamelryck T, Kauff F, Wilczynski B and de Hoon MJL (2009) Biopython: freely available Python tools for computational molecular biology and bioinformatics. Bioinformatics, 25, 1422-1423

## AI Acknowledgements
When writing Project 1, I used ChatGPT to help guide me on how to locate and download publicly available sequence data from NCBI. I also use it to revise my paragraphs in both Project 1 and 3.
