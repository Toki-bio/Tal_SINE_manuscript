# Tal SINE — manuscript supporting data

Per-species SINEderella run reports and intermediate outputs for the six talpid
genomes (Talpini, Desmanini, Scalopini, Condylurini) analyzed in the manuscript
on the Tal SINE family.

Live pages: https://toki-bio.github.io/Tal_SINE_manuscript/

## Contents

Each species directory (`toc`, `teu`, `gpy`, `dmo`, `saq`, `ccr`) contains:

- `report.html` — subfamily consensus alignments, SINE tribes (99% copy
  clusters), subfamily composition (copy counts, similarity to consensus),
  and per-copy divergence-from-consensus distributions, plus an optional
  "Pipeline QC" section (raw hit counts, assignment funnel stats including
  unassigned loci, bitscore thresholds, quality flags) kept for
  reproducibility but not used to generate manuscript figures.
- `alignments/` — subfamily and tribe MSA FASTA files, viewable via linked
  [MSA Viewer](https://toki-bio.github.io/MSA-viewer/) links in each report.
- `tribes/` — tribe alignments and `tribes_summary.tsv`.
- `subfam/` — SubFam chunk-consensus alignment files.

This repository does not include analyses not described in the manuscript
(e.g., PCA mutation-landscape plots, per-subfamily diagnostic galleries) or
species outside its scope.

## Custom software

The pipeline tools used are maintained as separate repositories:

- [sear2k](https://github.com/Toki-bio/sear2k) — SINE copy detection
- [SubFam](https://github.com/Toki-bio/SubFam) — subfamily consensus building
- [FaSort10 / asSINEment](https://github.com/Toki-bio/FaSort10) — subfamily assignment voting
- [SINE_orth_loc](https://github.com/Toki-bio/SINE_orth_loc) — orthologous locus assessment

## Genome assemblies

Analyzed genome assemblies are publicly available from NCBI GenBank/RefSeq;
accession numbers are listed in the manuscript's Methods section (2.1.1).
