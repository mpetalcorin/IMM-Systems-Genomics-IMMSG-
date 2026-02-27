# Datasheet: IMM Systems Genomics (IMMSG) Datasets
Documentation for the expression and metadata inputs used to score **IMM functional modules** and infer coupling, leak, and network structure.

## Dataset overview
This project uses:
1. An **expression matrix** (genes x samples)
2. A **metadata table** describing sample labels, group membership, and optional covariates.

The pipeline is compatible with:
- TPM/CPM expression matrices
- count-like matrices (recommended to transform or normalize before use)

## Data sources
- User-provided datasets (bulk RNA-seq or comparable expression technologies)
- Optional demo simulation generated within the notebook for validation of the workflow.

## Expected file formats
### Expression matrix
- File: `expr.csv` or `expr.tsv`
- Rows: gene symbols (HGNC); mtDNA symbols like `MT-ND1`, `MT-CO1` supported
- Columns: sample IDs
- Values: non-negative expression units

### Metadata
- File: `meta.csv` or `meta.tsv`
- Index (or first column): sample IDs matching the expression columns
- Required column (default workflow): `group` with exactly two groups (e.g., Control/Case)
- Optional columns: batch, tissue, age, sex, treatment, timepoint, etc.

## Data preprocessing
- Gene symbols are harmonized by trimming whitespace and converting to uppercase.
- Expression is transformed using `log1p(x)` in the notebooks.
- Samples are intersected between expression and metadata to ensure alignment.

## Label definitions
- `group`: the primary two-class phenotype used in differential tests (default pipeline).
If you have >2 groups or continuous labels, the workflow should be extended to linear models.

## Potential biases and confounders
Common confounders include:
- Batch effects and library preparation differences
- Tissue heterogeneity and cell-type composition
- Unequal group sizes
- Unmeasured covariates (age, medication, disease stage)

Recommendations:
- Include batch/covariates in extended models.
- Perform sensitivity analyses stratifying by confounders.

## Missing data
- If a moduleÕs genes are absent from the dataset, that module score becomes missing for all samples.
- Missing sample metadata can exclude samples from differential tests.

## Privacy and governance (if human data)
- Remove direct identifiers.
- Follow institutional ethics and consent requirements.
- Use secure storage for controlled data.

## Outputs generated from the dataset
Tables in `outputs_immsg/tables/`:
- Module activity scores (`module_scores_auc.csv`)
- Composite scores (`composite_scores.csv`)
- Differential results (`diff_module_activity.csv`, `diff_expression_IMM_genes.csv`)
- Latent factor loadings (`pca_loadings.csv`, `pca_variance.csv`, `nmf_loadings.csv`)
- Network edges (`module_partial_corr_edges.csv`)
- Summary JSON (`summary.json`)

## Suggested citation and attribution
**Petalcorin, M.I.R.** (2026). Systems Genomics of the Inner Mitochondrial Membrane Identifies a Coupled OXPHOS–Cristae Program Opposed by Leak and Stress Signatures. GitHub: https://github.com/mpetalcorin/IMM-Systems-Genomics-IMMSG-
