# Scripts used in this study

These are the exact scripts that produced the results of the manuscript, collected from the
analysis server: for the pipeline steps, the copies stored in each run directory at run time;
for the stand-alone tools, the versions installed when the analyses were run (searches and
assignment 25 April to 17 May 2026; orthology 22–23 June 2026). The files are byte-identical to
those copies; checksums are given below. Paths and thread counts inside the scripts are those of
the original server.

## Steps

| Step | Script | How it was run |
|---|---|---|
| Preliminary search (subfamily discovery) | `search/sear` | `sear <query> <genome>` with one Tal query |
| Random sample of 30,000 loci | `discovery/sample` | `sample 30000 <loci>` (GNU `shuf`, no seed); the samples are in `<species>/subfam/` |
| Batch consensuses | `discovery/SubFam` | `SubFam <sample>` (600 batches of 50, one consensus per batch) |
| Search with all subfamily consensuses, merging, extraction | `search/step1_search_extract.sh` | calls `sear -b -k <consensus> <genome> 0.8 65 50` for each consensus, then BEDtools merge and getfasta |
| Assignment of all loci (asSINEment) | `assignment/asSINEment.sh` | ten SSEARCH36 voting cycles; unanimous loci above 0.45 × TopN bit score are firm, the rest are assigned by best vote |
| Copy numbers per subfamily | `assignment/step3_postprocess.sh` | writes `summary.by_subfam.tsv` (firm + soft = copy numbers of Figure 2) |
| Similarity of copies to their consensus | `assignment/step4_plots.sh`, `assignment/plot_subfamily.py` | up to 10,000 unanimously assigned copies per subfamily; SSEARCH36 percent identity (Figure 2, Figure S2). The two *S. aquaticus* runs used the versions in `assignment/saq_runs/` |
| Orthologous presence/absence | `orthology/SINE_orth_loc.bash`, `orthology/ComPair.sh` | `SINE_orth_loc.bash toc.bnk teu.bnk TAL.q` and `SINE_orth_loc.bash gpy.bnk dmo.bnk TAL.q` |
| Tribes | VSEARCH | `vsearch --cluster_fast --id 0.99 --strand plus`, clusters of at least five copies |

`sear` corresponds to commit f315c11 of https://github.com/Toki-bio/sear2k, and `SINE_orth_loc.bash`
to commit 05d0dab of https://github.com/Toki-bio/SINE_orth_loc (the copy here calls `ComPair.sh`
by its absolute path; `ComPair.sh` is commit 376a86e). Both commits carry the tag
`tal-manuscript-2026`.

Third-party software: SSEARCH36 36.3.8h, BEDTools 2.29.2, SeqKit 2.6.1, MAFFT 7.490,
EMBOSS 6.6.0 (cons), BWA 0.7.17-r1188, samtools 1.16.1, VSEARCH.

## Checksums

Git blob hash (`git hash-object`) and SHA-256.

| File | git blob | SHA-256 |
|---|---|---|
| `assignment/asSINEment.sh` | `d406ae0cfe1d2d723d2f593c6fdad69387678a30` | `30095c8162b873cf415ba594322a701d8b3cdba28111296ec3b9c46954467ba0` |
| `assignment/plot_subfamily.py` | `aa78b93fa251f2b77bfc56299efc333ae3652697` | `c4568f017b64dc77ed9be5de0d3c4eea6bc9b34dc26e5e2bdd16d48c9464ad09` |
| `assignment/saq_runs/plot_subfamily.py` | `c15298ba37067fc0477474dd92674b65acedcbba` | `9a37cdfce225eb97e84b927b72b054ad73b2ba97b024dd8b43659578fafa1a6d` |
| `assignment/saq_runs/step4_plots.sh` | `d0c4b70c9161197e3456b3b855486e0f38560103` | `8212cbd13a1df22fdcf4b9fe9f86bec98cbed4d81e6ae742af214e06db185469` |
| `assignment/step3_postprocess.sh` | `b96b1d96b5e020c8a656e414025e88feab11d0db` | `182692c3717f759c9f7b4a10d124c12b3d300f46e771b23da1feb3beea82832c` |
| `assignment/step4_plots.sh` | `64dde5630f0b51ea8f1c547e6ac1bf3deac8c9cb` | `f0d5775091eeb067077a31f813ef152bbbdc409a0c7137a2310bd827c8c3ece9` |
| `discovery/SubFam` | `d5eca0cee72a3f7b88daa2c91197466a18535f42` | `bdeed4d6ad8126b8ef5c0f85a2d5585694ed3918011c4129318b1d9c09499648` |
| `discovery/sample` | `5a8295348a65a0ad8637ae7706066e19bb0026cf` | `921284303ff1ab9a63bcdd1d50480345a8894266bba9ea15320b69a3fa5af5a7` |
| `orthology/ComPair.sh` | `2e1cd3edb549c583dc674c74d8f2ece0f3191af6` | `f2ac0bcffae6dc4632a51f90a2c6bb95c0110d7e7ddf6d4cb23f8e60785642af` |
| `orthology/SINE_orth_loc.bash` | `6adb75dfcf69c3a6f15eba05266247e79d82cf84` | `342b8e93d40f1b54307ca582f4b19a1aeb7d549249cf67280590f2e74985b178` |
| `search/sear` | `9bc6d7377278faceb172a2fc0d81ddd28ae88a8d` | `ad6d9e14bf5e96314ffdd36ccfa94ea7a1356d6e2c54792370f10d3e31abdf84` |
| `search/step1_search_extract.sh` | `ec45efdae851ccf776d46e1db994fabdc32efca5` | `cc399f50725f5c0ff494c1637d26fa1c6b5be1182935720805dd1b3a49e0c990` |
