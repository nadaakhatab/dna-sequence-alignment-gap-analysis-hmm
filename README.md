# msa-to-profile-hmm

> DNA sequence alignment and Profile HMM construction using MAFFT and Python — a Computational Biology assignment.

---

**Pipeline:** Raw sequences → FASTA file → MAFFT alignment → Gap fraction analysis → Profile HMM state paths

---

## Requirements

All dependencies are installed automatically inside the notebook.

| Tool | Purpose |
|------|---------|
| MAFFT 7.490 | Multiple sequence alignment |
| Biopython | Parsing FASTA / alignment files |
| Pandas | Displaying results as tables |
| NumPy | Numerical support |   
---

## Input Sequences

| ID | Sequence | Length |
|----|----------|--------|
| Seq1 | ACAATG | 6 |
| Seq2 | TCAACTATC | 9 |
| Seq3 | ACACAGC | 7 |
| Seq4 | AGAATC | 6 |
| Seq5 | ACCGATC | 7 |
| Seq6 | GATCAC | 6 |

---

## Results

### Part A — Multiple Sequence Alignment (MAFFT)

MAFFT (`--auto` mode) produced the following 11-column alignment:

```
          1  2  3  4  5  6  7  8  9  10 11
Seq1      -  -  -  A  C  A  A  T  G  -  -
Seq2      T  C  A  A  C  T  A  T  C  -  -
Seq3      A  C  -  A  C  A  G  C  -  -  -
Seq4      -  -  -  A  G  A  A  T  C  -  -
Seq5      A  -  -  C  C  G  A  T  C  -  -
Seq6      -  -  -  -  -  G  A  T  C  A  C
```

### Part A — Gap Fraction Analysis

Gap threshold: **0.35** → ≤ 0.35 = Match (M) | > 0.35 = Insert (I)

| Column | Residues | Gap Count | Gap Fraction | Classification |
|--------|----------|-----------|--------------|----------------|
| 1 | -, T, A, -, A, - | 3 | 0.50 | **I** |
| 2 | -, C, C, -, -, - | 4 | 0.67 | **I** |
| 3 | -, A, -, -, -, - | 5 | 0.83 | **I** |
| 4 | A, A, A, A, C, - | 1 | 0.17 | **M** |
| 5 | C, C, C, G, C, - | 1 | 0.17 | **M** |
| 6 | A, T, A, A, G, G | 0 | 0.00 | **M** |
| 7 | A, A, G, A, A, A | 0 | 0.00 | **M** |
| 8 | T, T, C, T, T, T | 0 | 0.00 | **M** |
| 9 | G, C, -, C, C, C | 1 | 0.17 | **M** |
| 10 | -, -, -, -, -, A | 5 | 0.83 | **I** |
| 11 | -, -, -, -, -, C | 5 | 0.83 | **I** |

**Seed (Match) columns:** 4, 5, 6, 7, 8, 9  
**Non-seed (Insert) columns:** 1, 2, 3, 10, 11

### Part B — Profile HMM State Paths

State assignment rules:
- Residue at M column → **M** (Match)
- Gap at M column → **D** (Delete)
- Residue at I column → **I** (Insert)
- Gap at I column → silent (omitted)

| Sequence | State Path |
|----------|-----------|
| Seq1 | `S → M → M → M → M → M → M → E` |
| Seq2 | `S → I → I → I → M → M → M → M → M → M → E` |
| Seq3 | `S → I → I → M → M → M → M → M → D → E` |
| Seq4 | `S → M → M → M → M → M → M → E` |
| Seq5 | `S → I → M → M → M → M → M → M → E` |
| Seq6 | `S → D → D → M → M → M → M → I → I → E` |

---

## Notebook Structure

```
Part 0 — Setup
  ├── Install MAFFT
  └── Import libraries (Biopython, Pandas, NumPy)

Part A — Multiple Sequence Alignment
  ├── A1: Write input.fasta
  ├── A2: Run MAFFT → aligned.fasta
  ├── A3: Parse & display alignment matrix
  └── A4: Gap fraction analysis + M/I classification

Part B — Profile HMM Construction
  ├── B1: Identify seed (M) columns
  └── B2: Build state paths for all sequences

Finale — 
  └── Concepts summary + Download code
```

---

## Files

```
msa-to-profile-hmm/
├── CompBio_MSA_to_ProfileHMM.ipynb   # Main notebook
└── README.md

---
## Downloaded files
```

gap_analysis.csv
msa_matrix.csv
state_paths.csv
```
