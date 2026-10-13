# Tal SINE — manuscript supporting data

Per-species run reports and intermediate outputs for the six talpid genomes
(Talpini, Desmanini, Scalopini, Condylurini) analyzed in the manuscript on the Tal SINE family.

Live pages: https://toki-bio.github.io/Tal_SINE_manuscript/

## Contents

Each species directory (`toc`, `teu`, `gpy`, `dmo`, `saq`, `ccr`) contains:

- `report.html` — subfamily consensus alignments, SINE tribes (99 % copy clusters) and
  subfamily composition (copy numbers), plus a "Pipeline QC" section (raw hit counts,
  assignment statistics, bit-score thresholds, quality flags) kept for reproducibility but not
  used for the manuscript figures.
- `alignments/` — subfamily consensus alignments and, per subfamily, the 100 best-scoring and
  100 random copies with flanks.
- `tribes/` — tribe alignments, `tribes_summary.tsv` (all clusters with at least five copies)
  and `tribes_metadata.txt`.
- `code/` — the scripts used (see below).
- `subfam/` — SubFam chunk-consensus alignments, and `<species>_subfam_sample_30000.fasta.gz`:
  the random sample of 30,000 Tal loci on which the subfamilies were discovered (600 SubFam
  batches of 50). The sample was drawn once per species, with GNU `shuf` and no fixed seed,
  from the loci found in a preliminary search with a single Tal query. All loci in each genome
  were then assigned to the resulting subfamilies, so the copy numbers were counted directly,
  not extrapolated from the sample.

### Copy numbers

Every locus is assigned to a subfamily: unanimously in all ten voting cycles and above the
bit-score threshold ("firm"), or otherwise to the subfamily with the best vote ("soft"). The
copy numbers in the manuscript (Figure 2) are the "Total copies" column of each report
(firm + soft). The report column "Bit-score ratio" is a pipeline statistic; the similarity
values in Figure 2 are percent identities.

### Subfamily names

Files keep the run names of the consensus sequences; the reports show both names.

| species | a | b / b1 | b2 | b3 | c | d | e | f | g |
|---|---|---|---|---|---|---|---|---|---|
| *T. occidentalis*, *T. europaea* (`toc`, `teu`) | t3 | b1 = t6 | t5 | | t4 | t2 | t1 | | |
| *G. pyrenaicus*, *D. moschata* (`gpy`, `dmo`) | d1 | b = d5 | | | d3 | d2 | d4 | | |
| *S. aquaticus* (`saq`) | s2 | b1 = s3 | s7g | | s1 + s9 | s8 | s6 | s5 | s4 |
| *C. cristata* (`ccr`) | a_ccr | b1 = g1 | g7 | g6 | g2 | g3 | g4 | g5 | |

One consensus set was used for both *Talpa* species and one for both desmans; copy numbers were
obtained separately for each genome.

### Tribes (Table 2)

The report column "Table 2 tribe #" gives the number used in the manuscript. Alignment files keep
the cluster rank of `tribes_summary.tsv`. They are the same for *T. occidentalis*,
*G. pyrenaicus*, *D. moschata* and *C. cristata*; they differ in two species, where tandem,
satellite-like clusters and clusters without assigned copies were removed:

| species | Table 2 tribe | file |
|---|---|---|
| *T. europaea* | 01, 02, 03 | `teu_tribe01`, `02`, `03` |
| | 04, 05, 06 | `teu_tribe06`, `07`, `08` |
| | 07, 08, 09, 10 | `teu_tribe11`, `12`, `13`, `14` |
| *S. aquaticus* | 01, 02, 03 | `saq_tribe04`, `05`, `06` |
| | 04, 05 | `saq_tribe08`, `09` |

Figure S5 (*T. europaea* tribe 04) is `teu/tribes/teu_tribe06_79seqs.aln.fa`.

## Software — exact versions used

`code/` holds the exact scripts that produced the results (search, subfamily discovery,
assignment, copy numbers, similarity, orthology), byte-identical to the copies used in the runs,
with checksums and the commands used; see [`code/README.md`](code/README.md).

The stand-alone tools are also maintained as separate repositories; the versions used carry the
tag `tal-manuscript-2026`:

- [sear2k](https://github.com/Toki-bio/sear2k/tree/tal-manuscript-2026) — `sear`, SSEARCH36-based
  genome search (commit f315c11);
- [SINE_orth_loc](https://github.com/Toki-bio/SINE_orth_loc/tree/tal-manuscript-2026) —
  orthologous presence/absence of loci (commit 05d0dab; `ComPair.sh` 376a86e).

Third-party: SSEARCH36 36.3.8h, BEDTools 2.29.2, SeqKit 2.6.1, MAFFT 7.490, EMBOSS 6.6.0,
BWA 0.7.17, samtools 1.16.1, VSEARCH.

## Genome assemblies

Analyzed genome assemblies are publicly available from NCBI GenBank/RefSeq; accession numbers
are listed in the manuscript's Methods section (2.1).
