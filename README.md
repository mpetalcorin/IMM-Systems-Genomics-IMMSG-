# IMM Systems Genomics (IMMSG) 
A reproducible systems-genomics pipeline that scores **inner mitochondrial membrane** modules per sample and maps **coupling vs leak/stress** states with differential analysis, PCA/NMF, partial-correlation networks, hypergraphs, and bootstrap robustness.

## What this repository is
This repository contains a fully reproducible **systems-genomics** workflow for analyzing the **inner mitochondrial membrane (IMM)** as a set of mechanistic layers (modules), rather than isolated genes. It converts expression matrices into per-sample **module activity** scores, then performs differential analysis, latent structure discovery, conditional-dependency network inference, hypergraph-style module–gene mapping, and robustness checks.

The workflow is built around curated IMM layers including:
- **ETC complexes I–IV** (including mtDNA-encoded subunits)
- **CoQ biosynthesis** and **cytochrome c**
- **ATP synthase** and regulators
- **SLC25 carrier logistics**
- **Ion handling** (MCU, NCLX, UCPs/LETM1)
- **Protein import/insertion** (TIM23, TIM22, OXA1L)
- **Cristae architecture** (MICOS, OPA1-linked factors)
- **Proteostasis and quality control** (AAA proteases, OMA1)
- **Cardiolipin biosynthesis/remodeling**
- **Assembly/organization factors** (expandable)

## Key outputs 
The pipeline produces:
- Per-sample **module activity matrix** (rank-based AUC scores)
- **Composite system metrics**: Coupling Integrity Score, Leak/Uncoupling Index
- **Differential module activity** (two-group)
- **Differential expression** on curated IMM genes (two-group)
- **PCA + NMF** for low-dimensional IMM state programs
- **Partial-correlation module network** (Graphical Lasso)
- **Hypergraph-style visualization** linking modules to genes
- **Bootstrap stability** of module differences

All core tables are written to:
`outputs_immsg/tables/`

Expected tables include:
- `module_scores_auc.csv`
- `composite_scores.csv`
- `diff_module_activity.csv`
- `diff_expression_IMM_genes.csv`
- `pca_loadings.csv`
- `pca_variance.csv`
- `nmf_loadings.csv`
- `module_partial_corr_edges.csv`
- `summary.json`

## Repository structure
```
├── notebooks/
│   ├── IMM_systems_genomics_IMMSG_notebook.ipynb
│   └── IMM_systems_genomics_IMMSG_notebook_intensive.ipynb
├── outputs_immsg/
│   ├── figures/                    
│   └── tables/                     
├── src/
│   └── immsg_core.py               
├── data/
│   ├── expr_example.csv            
│   └── meta_example.csv             
├── README.md
├── modelcard.md
└── datasheet.md
```
## Run
	•	notebooks/IMM_systems_genomics_IMMSG_notebook.ipynb (core pipeline)
	•	notebooks/IMM_systems_genomics_IMMSG_notebook_intensive.ipynb (intensive analysis: volcano, networks, hypergraph, bootstrap)

## Method summary (high level)
	1.	Rank-based module scoring per sample (AUC-style)
	2.	Composite coupling metrics: Coupling Integrity and Leak/Uncoupling
	3.	Differential testing: modules and curated IMM genes
	4.	Latent structure: PCA and NMF programs
	5.	Conditional dependency: Graphical Lasso partial correlations
	6.	Hypergraph mapping: module–gene bipartite graph with hulls
	7.	Bootstrap stability: robustness of module differences

## Interpreting results
	•	High Coupling Integrity Score suggests coordinated ETC + ATP synthase + architecture/logistics activity.
	•	High Leak/Uncoupling Index suggests elevated leak/stress signatures relative to ETC.
	•	Top differential modules identify which IMM layers most separate groups.
	•	PCA shows whether IMM state separates groups in low-dimensional space.
	•	Partial-correlation edges suggest direct module couplings, not just co-variation.
	•	Bootstrap stability identifies which findings are most reproducible.

## Limitations
	•	Expression-based inference does not directly measure protein abundance, assembly state, membrane potential, or flux.
	•	Network inference is statistical and does not establish causality.
	•	Default tests assume 2 groups; multi-group designs require extension.

## Extending the pipeline
Common extensions:
	•	Multi-group ANOVA or linear models with covariates (batch, tissue, age)
	•	Continuous-outcome regression (e.g., survival, metabolite levels)
	•	Integration with proteomics/lipidomics (cardiolipin composition, ETC complex abundance)
	•	Single-cell adaptation (cell-type stratified module activity)

## Citation
**Petalcorin, M.I.R.** (2026). Systems Genomics of the Inner Mitochondrial Membrane Identifies a Coupled OXPHOS–Cristae Program Opposed by Leak and Stress Signatures. GitHub: https://github.com/mpetalcorin/IMM-Systems-Genomics-IMMSG-

## License
MIT 
