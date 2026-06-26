# Galaxy workflow — BLAST → MSA → Phylogenetic tree

**Project:** The Bioinformatic Detective — sequence B (**TEM-1 β-lactamase**, UniProt P62593)
**Goal:** a reproducible Galaxy pipeline that takes the homolog multi-FASTA and produces BLAST hits, a multiple sequence alignment, and a phylogenetic tree.

Use the public server **usegalaxy.org** (or usegalaxy.eu). Create a new History, then a new Workflow (Workflow → Create) and add the steps below. Exact tool versions vary between servers — pick the latest available of each named tool.

---

## Inputs

| Input | What to upload |
|---|---|
| `query.fasta` | the single unknown sequence (student_seqB.fasta) |
| `homologs.fasta` | query + 4 homologs (multi-FASTA produced for this project) |

`Get Data → Upload File` for both; set datatype to **fasta**.

---

## Step 1 — Similarity search (BLAST)

**Tool:** *NCBI BLAST+ blastp*

- Query: `query.fasta`
- Search against: a protein database — either a built-in nr/SwissProt DB on the server, or make your own with *NCBI BLAST+ makeblastdb* from `homologs.fasta`.
- Scoring: BLOSUM62, default gaps.
- **Output format:** *Tabular (extended, 25 columns)* so you capture `pident`, `evalue`, `qcovs`, `staxids`.

→ Output: `blast_hits.tabular` (record % identity, E-value, query coverage for the report).

> Teaching point: hits will span several Gram-negative genera at ~100 % identity → mobile, highly conserved resistance gene.

---

## Step 2 — Multiple sequence alignment (MSA)

**Tool:** *MUSCLE* (or *MAFFT*)

- Input: `homologs.fasta`
- Output format: **FASTA alignment** (also keep ClustalW/HTML for visual inspection).

→ Output: `alignment.fasta`

> Inspect conserved columns: the S-x-x-K (Ser70/Lys73), SDN (Ser130–Asp131–Asn132) and K-[S/T]-G (Lys234…Gly236) catalytic motifs should be invariant.

---

## Step 3 — Phylogenetic tree

**Tool:** *FastTree* (fast) or *IQ-TREE* (model selection + bootstrap, slower but more rigorous)

- Input: `alignment.fasta`
- Mode: protein (WAG/LG model).
- (IQ-TREE) enable ultrafast bootstrap (e.g. 1000 replicates) for support values.

→ Output: `tree.nwk` (Newick).

**Visualise:** *Newick Display* tool, or download the Newick and open in iTOL / FigTree. Root on the Gram-positive outgroup (BlaZ/PC1, *S. aureus*).

---

## Step 4 — Save & share the workflow

1. Run the chain once end-to-end so every step has a green dataset.
2. **History → Extract Workflow** to auto-build the `.ga` workflow from the run (this is the "use agent to create a workflow" part of the brief).
3. Workflow → **Download** (`.ga` file) — commit it to the GitHub repo alongside `Sequence_B_report.docx`, `homologs.fasta`, `alignment.fasta`, and `tree.nwk`.
4. Optionally **Share** the workflow with the teacher(s) via the Galaxy share link.

---

## Pipeline diagram

```
homologs.fasta ─┬─► [makeblastdb] ─► [blastp] ─► blast_hits.tabular
                │
                └─► [MUSCLE / MAFFT] ─► alignment.fasta ─► [FastTree / IQ-TREE] ─► tree.nwk ─► [Newick Display]
```

## GitHub submission checklist

- [ ] `Sequence_B_report.docx` — full written analysis
- [ ] `homologs.fasta` — multi-FASTA (query + homologs)
- [ ] `alignment.fasta` — MSA
- [ ] `tree.nwk` — phylogenetic tree
- [ ] `*.ga` — exported Galaxy workflow
- [ ] commit + share repo with teacher(s)
