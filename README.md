# Mammalian T-Cell Coreceptor Sequence Analysis: CD4 and CD8A

## Overview

This project compares the protein-coding sequences of two T-cell coreceptors,
CD4 and CD8A, across seven mammalian species: human, chimpanzee, mouse, rat,
dog, cow, and pig.

The workflow curates sequences, aligns each protein family with MAFFT,
calculates gap-aware pairwise sequence identity, examines column-wise
conservation, and produces reproducible result tables and figures.

## Biological question

CD4 and CD8A are coreceptors involved in T-cell recognition and immune
signaling. This project asks:

- How similar are CD4 and CD8A sequences across mammals?
- Which regions of each protein are most conserved?
- Do CD4 and CD8A show different overall levels of sequence conservation?

## Key results

- Mean CD4 pairwise identity across mammals: **59.2%**
- Mean CD8A pairwise identity across mammals: **58.4%**
- CD4 and CD8A show similar overall levels of mammalian sequence conservation.
- Human and chimpanzee CD4 are 98.9% identical.
- Human and chimpanzee CD8A are 99.1% identical.
- The final CD4 alignment contains 7 sequences and is 478 columns long.
- The corrected cow CD4 sequence reduced alignment gaps from 83 to 23.
- CD8A sequences and alignment were not modified during the CD4 correction.

## Figures

### CD4 pairwise sequence identity

![CD4 pairwise identity heatmap](figures/CD4_pairwise_identity_heatmap.png)

### CD8A pairwise sequence identity

![CD8A pairwise identity heatmap](figures/CD8A_pairwise_identity_heatmap.png)

### Alignment conservation

![Coreceptor alignment conservation](figures/coreceptor_alignment_conservation.png)

## Data

For each coreceptor, the analysis uses one protein sequence from each of
seven species: human, chimpanzee, mouse, rat, dog, cow, and pig.

The cow CD4 sequence was replaced during quality control because the original
record produced an unusually gap-rich alignment. The active replacement is
`XP_024847184.1`, with a saved protein length of 455 amino acids.

## Methods

1. **Sequence retrieval:** CD4 and CD8A amino-acid sequences were retrieved
   from NCBI and saved as FASTA files.

2. **Sequence curation:** Each sequence was checked for accession, format,
   and amino-acid length. The original cow CD4 sequence was retained as a
   backup before replacement.

3. **Multiple sequence alignment:** CD4 and CD8A sequences were aligned
   independently using MAFFT with the `--auto` option.

4. **Pairwise identity:** Pairwise identity was calculated from each MAFFT
   alignment. Alignment-gap positions were excluded so that identity reflects
   comparable amino-acid positions only.

5. **Conservation analysis:** For every alignment column, conservation was
   calculated as the percentage of sequences sharing the most common
   non-gap residue.

6. **Visualization:** Identity matrices were plotted as heatmaps, and
   column-wise conservation was plotted for CD4 and CD8A.

## Project structure

```text
project_01_tcell_coreceptors/
├── README.md
├── data/
│   ├── raw/
│   │   ├── CD4/
│   │   └── CD8A/
│   ├── processed/
│   └── excluded_sequences/
├── results/
│   ├── CD4/
│   ├── CD8A/
│   └── final_results_inventory.csv
└── figures/
```

## Main outputs

| Output | Location |
|---|---|
| Combined CD4 sequences | `data/processed/CD4_sequences.fasta` |
| CD4 MAFFT alignment | `results/CD4/CD4_alignment.fasta` |
| CD4 identity matrix | `results/CD4/CD4_pairwise_identity.csv` |
| Combined CD8A sequences | `data/processed/CD8A_sequences.fasta` |
| CD8A MAFFT alignment | `results/CD8A/CD8A_alignment.fasta` |
| CD8A identity matrix | `results/CD8A/CD8A_pairwise_identity.csv` |
| Coreceptor comparison | `results/coreceptor_identity_summary.csv` |
| CD4 identity heatmap | `figures/CD4_pairwise_identity_heatmap.png` |
| CD8A identity heatmap | `figures/CD8A_pairwise_identity_heatmap.png` |
| Conservation plot | `figures/coreceptor_alignment_conservation.png` |
| Results inventory | `results/final_results_inventory.csv` |

## How to reproduce

This analysis was developed in Google Colab with Google Drive storage.

### Requirements

- Google account with Google Drive access
- Python 3
- Biopython
- pandas
- NumPy
- Matplotlib
- Seaborn
- MAFFT

Install the Python dependencies in Colab with:

```bash
pip install biopython pandas numpy matplotlib seaborn
```

Install MAFFT in Colab with:

```bash
apt-get update
apt-get install -y mafft
```

### Workflow

1. Mount Google Drive.
2. Place the raw FASTA files in `data/raw/CD4/` and `data/raw/CD8A/`.
3. Run the sequence-combination cells.
4. Run the MAFFT alignment cells.
5. Run the pairwise-identity cells.
6. Run the heatmap and conservation-analysis cells.
7. Run the final-results-inventory cell.

## Quality control and provenance

- The original cow CD4 sequence is retained in `data/excluded_sequences/`.
- The CD4 alignment from before the cow replacement is retained in
  `data/excluded_sequences/`.
- The replacement cow CD4 accession is `XP_024847184.1`.
- The replacement cow CD4 protein length is 455 amino acids.
- CD8A sequences and alignment were not changed during the CD4 correction.
- MAFFT standard error output is saved as `results/CD4/CD4_mafft.log`.

## Limitations

- This analysis compares primary amino-acid sequences, not protein structure
  or expression.
- Pairwise identity does not by itself demonstrate functional conservation.
- One sequence per species limits interpretation of within-species variation.
- Alignment gaps are excluded from identity calculations, so identity values
  should not be interpreted as whole-protein coverage.

## Future work

- Add more mammalian species to improve evolutionary sampling.
- Map conserved alignment columns onto known CD4 and CD8A domains.
- Compare nonsynonymous substitution rates across species.
- Use AlphaFold or experimentally determined structures to assess whether
  conserved residues cluster in functional regions.
