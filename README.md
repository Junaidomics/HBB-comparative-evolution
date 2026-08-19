# Comparative Evolution of the HBB Gene Across Primates

 
**Project type:** Comparative bioinformatics / molecular evolution

## Project overview

This project investigates the evolutionary conservation of the **HBB (beta-globin) gene across selected primates** using comparative sequence analysis.

The analysis is built around a biological question rather than a software tool:

> **How conserved is the HBB gene across selected primates, and what do patterns of nucleotide and amino-acid conservation suggest about evolutionary constraint on this functionally important hemoglobin gene?**

The notebook contains the supplied FASTA sequences as separate embedded sequence blocks. This makes the core analysis reproducible without requiring a reader to download a separate collection of FASTA files.

---

## Biological background

The **HBB gene** encodes the beta subunit of hemoglobin, an essential component of red blood cells involved in oxygen transport.

Because HBB performs an important biological function, substantial conservation across primate species is expected. Comparing HBB sequences therefore provides a straightforward way to investigate how much sequence variation occurs at the nucleotide and protein levels.

The project asks whether the observed sequence patterns are consistent with evolutionary constraint.

> **Important:** sequence conservation is consistent with evolutionary constraint, but this project does not by itself prove a specific selection mechanism.

---

## Biological question

**How conserved is HBB across selected primates, and what do nucleotide and amino-acid differences tell us about the evolutionary constraint acting on this gene?**

### Working hypothesis

The HBB coding sequence and its encoded protein should be highly conserved across primates because HBB performs an essential biological function.

---

## Dataset

The project uses five supplied HBB sequence records:

| Species | Role in project |
|---|---|
| Human | Reference sequence |
| Chimpanzee | Quality-control inspection; kept separate because the supplied record is partial/genomic |
| Gorilla | Included in curated CDS comparison |
| Orangutan | Included in curated CDS comparison |
| Rhesus macaque | Included in curated CDS comparison |

The four curated comparison sequences each contain **444 nucleotides (444 nt)**.

### Why is chimpanzee treated separately?

The supplied chimpanzee record is a partial/genomic record rather than a clean complete CDS record comparable to the four curated sequences.

Rather than forcing an incomplete record into the quantitative CDS analysis, it is retained for inspection and documented separately.

This is an intentional quality-control decision:

> **Biologically comparable sequences should be compared directly; records with different sequence context should not be forced into the same analysis without confirming their annotated boundaries.**

---

## Analysis workflow

```text
Embedded FASTA sequences
          ↓
Sequence QC
          ↓
CDS extraction
          ↓
CDS comparability checks
          ↓
Nucleotide identity
          ↓
Position-wise conservation
          ↓
Protein translation
          ↓
Protein identity
          ↓
Synonymous / non-synonymous differences
          ↓
Biological interpretation
```

### Main analyses

1. FASTA sequence reading and quality control
2. HBB CDS extraction
3. CDS length and reading-frame checks
4. Nucleotide identity relative to human HBB
5. Position-wise nucleotide conservation
6. Protein translation and protein identity
7. Synonymous versus non-synonymous coding differences
8. Biological interpretation and limitations

---

## Main results

The curated four-species CDS comparison produced the following nucleotide identity values relative to human HBB:

| Species | Nucleotide identity to human |
|---|---:|
| Human | 100.00% |
| Gorilla | 99.55% |
| Orangutan | 98.42% |
| Rhesus macaque | 95.72% |

At the protein level:

| Species | Protein identity to human |
|---|---:|
| Human | 100.00% |
| Gorilla | 99.32% |
| Orangutan | 98.64% |
| Rhesus macaque | 94.56% |

Across the **444-nucleotide curated CDS comparison**:

- **423/444 positions** were completely conserved
- **14/444 positions** showed 75% conservation
- **7/444 positions** showed 50% conservation
- **24 coding differences** were identified in the human-versus-primate comparison
- **13** were synonymous
- **11** were non-synonymous

These values are calculated by the notebook from the embedded sequence data.

---

## What does the conservation graph show?

The main conservation plot represents the nucleotide conservation of HBB at each position of the 444-nucleotide curated CDS.

### X-axis

**Nucleotide position** within the HBB CDS.

### Y-axis

**Conservation**, ranging from 0.50 to 1.00 in the observed dataset.

At each position, conservation is calculated as the frequency of the most common nucleotide among the four curated species.

Therefore:

- **1.00** = all four species have the same nucleotide
- **0.75** = three of four species share the same nucleotide
- **0.50** = two of four species share the same nucleotide

### Biological interpretation of the graph

Positions close to **1.00** are highly conserved across the sampled primates.

A drop in the graph indicates nucleotide variation at that position.

The graph therefore answers an important part of the biological question:

> **Is HBB variation widespread across the coding sequence, or are most positions conserved with variation concentrated at a smaller number of sites?**

The nucleotide conservation plot should be interpreted together with the protein-level results because a nucleotide substitution can be **synonymous**, meaning that it does not change the encoded amino acid.

### Methodological note

The graph is a direct, gap-free position-wise comparison of the four curated, equal-length CDS records.

It is **not a formal multiple-sequence-alignment result** and does not replace an alignment method for datasets containing gaps, insertions, deletions, or uncertain homology.

---

## Biological interpretation

The high nucleotide and protein similarity observed among the curated primate HBB sequences is **consistent with evolutionary constraint** on this functionally important gene.

The data also show that nucleotide differences do not always translate into amino-acid differences. This is reflected in the synonymous and non-synonymous classification.

The results broadly support the expectation that HBB remains highly conserved across the sampled primates.

### What this project does not prove

This analysis does not by itself demonstrate:

- positive selection
- purifying selection through a formal statistical test
- adaptation
- disease causation
- pathogenicity of an individual variant
- functional effects of individual substitutions
- a complete species phylogeny

Those claims would require additional datasets and/or formal evolutionary or functional analyses.

---

## Reproducibility

### Requirements

- Python 3
- Biopython
- pandas
- NumPy
- Matplotlib
- Jupyter Notebook, JupyterLab, or VS Code

### Running the notebook

Open:

```text
HBB_Comparative_Evolution_GitHub_CLEAN.ipynb
```

Select a Python 3 kernel and run the notebook **from top to bottom** using **Run All**.

The notebook intentionally reuses variables created in earlier cells. Running a later cell without running the required earlier cells can produce errors such as:

```text
NameError: name 'records' is not defined
```

### External tools

**MAFFT is not required for this version.**

The four curated CDS records are equal in length and pass the notebook's comparability checks, allowing the position-wise nucleotide analysis to be performed directly.

---

## Repository structure

```text
HBB-comparative-evolution/
│
├── README.md
│
└── HBB_Comparative_Evolution_GitHub_CLEAN.ipynb
```

The core sequence records are embedded individually inside the notebook, so separate FASTA files are not required to reproduce the main analysis.

---

## Quality-control philosophy

A central principle of this project is to avoid treating every sequence record as automatically comparable.

Before direct comparison, the notebook checks:

- sequence identity/accession information
- sequence length
- ambiguous nucleotides
- HBB start motif
- CDS length
- reading-frame compatibility
- terminal stop codon
- unexpected internal stop codons
- translated protein length

This makes the project more than a simple percentage-identity exercise: the sequence data are checked before biological conclusions are drawn.

---

## Limitations and future development

This is a focused comparative-sequence project rather than a complete molecular-evolution study.

A future expanded version could:

1. Confirm the exact annotated chimpanzee HBB CDS and integrate it into the comparison.
2. Add more primate species.
3. Perform a formal multiple-sequence alignment.
4. Construct an HBB gene tree.
5. Calculate dN/dS using an appropriate evolutionary model.
6. Compare conserved positions with known HBB functional or structural regions.

These additions would allow the project to move from a focused comparative analysis toward a broader molecular-evolution study.

---

## Skills demonstrated

- FASTA sequence handling
- Biopython
- sequence quality control
- CDS extraction
- nucleotide sequence comparison
- conservation analysis
- protein translation
- protein sequence comparison
- synonymous/non-synonymous classification
- data visualization with Matplotlib
- pandas-based analysis
- reproducible Jupyter workflows
- biological interpretation of sequence data
- scientific documentation

---

## Author

**Muhammad Junaid**  
**BS Biotechnology**

This project demonstrates a practical bioinformatics workflow from a biological question through sequence quality control, quantitative comparison, visualization, and cautious biological interpretation.
