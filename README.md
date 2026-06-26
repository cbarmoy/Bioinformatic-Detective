# The Bioinformatic Detective — Sequence B

**Bioinformatics Minor · 2025–2026**

Identification and characterisation of an unknown protein delivered as a neutral-header FASTA file (`sequence B`).

## Verdict

> **Sequence B = TEM-1 β-lactamase** · *Escherichia coli* · UniProt **P62593** · gene *bla*TEM-1 · EC 3.5.2.6

A 286-residue, ~31.5 kDa class A serine β-lactamase: the periplasmic enzyme that hydrolyses the β-lactam ring of penicillins and early cephalosporins, conferring antibiotic resistance. It is the most widespread plasmid-mediated β-lactamase in Gram-negative bacteria and the ancestral scaffold of many extended-spectrum (ESBL) and inhibitor-resistant variants.

## Repository contents

| File | Description |
|------|-------------|
| `Sequence_B_report.docx` | Full written analysis (BLAST, annotation, literature, MSA, tree, clinical significance) |
| `Sequence_B_presentation.pptx` | 8-slide presentation for the oral defence |
| `homologs.fasta` | Multi-FASTA: query + 4 class A β-lactamase homologs |
| `alignment.fasta` | Multiple sequence alignment of the homologs (MAFFT) |
| `tree.nwk` / `tree.png` | Phylogenetic tree, rooted on the BlaZ outgroup (Newick + figure) |
| `msa_motifs.png` | Conserved catalytic motifs across the alignment |
| `galaxy_workflow.ga` | Exported Galaxy workflow (BLAST → MAFFT → FastTree → Newick Display) |

## Methods

1. **Similarity search** — BLASTp of sequence B vs NCBI ClusteredNR → 100 % identity to TEM-1, E-value 0.0, full coverage; near-identical hits across many Gram-negative genera (mobile, conserved gene).
2. **Annotation** — gene and reviewed protein entry (UniProt P62593): length, MW, periplasmic localisation, class A fold, and catalytic residues (Ser70, Lys73, SDN loop, Glu166, K-[S/T]-G triad).
3. **Homolog collection** — TEM-1 (query), SHV-1, SHV-2, CTX-M-15, and BlaZ/PC1 (*S. aureus*, Gram-positive outgroup).
4. **MSA** — MAFFT alignment; 48 fully conserved columns concentrated in the catalytic core.
5. **Phylogeny** — FastTree (SH-like supports), rooted on the BlaZ outgroup → BlaZ | CTX-M-15 | TEM-1 | (SHV-1, SHV-2).
6. **Galaxy workflow** — reproducible pipeline chaining BLAST + MSA + tree.

## Key findings

- **Mobile, highly conserved resistance gene** — the same protein appears across *Acinetobacter, Klebsiella, Escherichia, Morganella, Providencia, Enterobacter*… via horizontal gene transfer.
- **Conserved catalytic core / variable surface** — the active-site signatures (S-x-x-K, SDN, K-[S/T]-G) are invariant across all five enzymes.
- **ESBL evolution by single mutations** — SHV-1 → SHV-2 differ by a single residue, illustrating how one substitution extends the resistance spectrum.

## Reproduce

Import `galaxy_workflow.ga` into [usegalaxy.org](https://usegalaxy.org) and supply `homologs.fasta` as input to re-run BLAST → MSA → tree.

## License

MIT © 2026 Côme Barmoy
