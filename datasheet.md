# Datasheet: BioFM Workflow Evaluator Demo Dataset and Supported Inputs

## Dataset and system name

BioFM Workflow Evaluator demo dataset and supported input schema

## Version

Version 0.1.0

## Date

2026-04-29

## Maintainer

aAidea

Scientific and technical lead:
Mark I.R. Petalcorin

Website:
https://a-aidea.com

Repository:
https://github.com/mpetalcorin/Biofm-Workflow-Evaluator-

## Purpose of this datasheet

This datasheet describes the demo dataset, expected input formats, data assumptions, preprocessing logic, quality-control outputs, and limitations for BioFM Workflow Evaluator. The goal is to document how the application handles uploaded biological datasets and how users should interpret the outputs.

## Dataset purpose

The included demo dataset is a small synthetic expression-like table designed to test the full software workflow. It allows the frontend to send a browser-generated CSV file to the FastAPI backend and receive a structured analysis response.

The dataset is intended for software testing, demonstration, user-interface testing, API testing, and portfolio presentation. It is not intended for biological discovery, clinical interpretation, or statistical inference.

## Dataset location

The project may include a local demo file at:

backend/demo_data/demo_expression.csv

The frontend can also generate a demo CSV file in the browser when the user presses the Run demo button.

## Supported file types

The backend supports:

h5ad
parquet
csv

h5ad files are read directly as AnnData objects.

CSV and parquet files are converted into AnnData objects by treating numeric columns as features and non-numeric columns as observation metadata.

## Expected data structure

For CSV or parquet files:

Rows represent cells, samples, observations, or perturbation conditions.
Numeric columns represent expression-like or feature-like measurements.
Non-numeric columns represent metadata.

For h5ad files:

The file should contain a valid AnnData object with `.X`, `.obs`, `.var`, and optionally `.obsm`, `.layers`, or other AnnData attributes.

## Demo dataset fields

The demo CSV includes one metadata column:

sample_type

and several numeric gene-like columns:

MKI67
TOP2A
PCNA
MCM2
HIF1A
CA9
SLC2A1
LDHA
CDKN1A
GADD45A
RAD51
CHEK1
IL6
CXCL8
NFKBIA
TNFAIP3

## Biological programmes represented in the demo

The demo marker sets represent broad biological programmes:

Proliferation:
MKI67, TOP2A, PCNA, MCM2

Hypoxia or metabolic stress:
HIF1A, CA9, SLC2A1, LDHA

DNA damage or replication stress:
CDKN1A, GADD45A, RAD51, CHEK1

Inflammation:
IL6, CXCL8, NFKBIA, TNFAIP3

These marker sets are used only for transparent demonstration. They are not comprehensive signatures and should not be treated as validated classifiers.

## Data collection process

The demo dataset is synthetically generated and manually defined for software testing. It was not collected from human participants, animal experiments, clinical trials, patient samples, or wet-lab experiments.

## Data subject information

The demo dataset contains no personal data, no patient data, no protected health information, no human subject identifiers, and no clinical metadata.

## Preprocessing

For uploaded CSV and parquet files, the backend performs the following steps:

1. Read file into a pandas DataFrame.
2. Select numeric columns as expression-like features.
3. Treat non-numeric columns as observation metadata.
4. Convert the resulting table into an AnnData object.
5. Compute quality-control metrics.
6. Apply Scanpy-style preprocessing where possible.
7. Inspect available embeddings.
8. Apply marker-overlap biological reasoning.
9. Return a release-readiness score and warnings.

For h5ad files, the backend reads the AnnData object directly and applies quality-control and preprocessing logic.

## Quality-control metrics

The backend computes:

n_cells
n_genes
mean_counts_per_cell
mean_genes_per_cell
pct_missing_metadata
sparsity

These metrics help identify whether the uploaded dataset appears suitable for downstream interpretation.

## Backend output schema

The `/api/analyse` endpoint returns:

filename
file_type
qc_report
embedding_report
biological_reasoning
release_readiness_score
warnings

## Biological reasoning output

The biological reasoning object includes:

predicted_state
biological_plausibility_score
pathway_coherence_score
evidence_support_score
interpretation
recommended_next_steps

## Recommended next steps produced by the system

The backend may recommend:

Inspect marker genes and pathway enrichment.
Check batch effects and metadata consistency.
Compare predicted state against negative and positive controls.
Validate top predictions using orthogonal assays or public datasets.

## Intended users

Intended users include computational biologists, bioinformaticians, scientific software developers, data scientists, machine learning scientists, drug-discovery researchers, and portfolio reviewers evaluating biology software engineering capability.

## Non-intended users

The software is not intended for clinicians, patients, regulatory decision-makers, or users seeking validated clinical or diagnostic recommendations.

## Dataset limitations

The demo dataset is small and synthetic.

It does not represent real single-cell sequencing data.

It does not include real sequencing depth, dropout, doublet structure, batch effects, donor effects, cell-type annotation, or experimental replicates.

It does not validate biological claims.

It is designed to test software pathways, not biological hypotheses.

## Data quality limitations

Real uploaded datasets may contain missing values, inconsistent gene identifiers, duplicate feature names, sparse matrices, batch effects, metadata errors, mixed species gene names, or non-standard file structures. These issues may affect output interpretation.

## Ethical considerations

The demo dataset contains no human or sensitive data. If users upload real biological or clinical datasets, they are responsible for ensuring proper data governance, consent, anonymisation, security, and compliance with applicable institutional, legal, and ethical requirements.

## Privacy considerations

The local version runs on the user's machine. In a deployed version, uploaded files are sent to the backend server. Users should not upload sensitive, patient-level, proprietary, or regulated data unless the deployment environment has appropriate privacy and security safeguards.

## Recommended safeguards for production

For production use, implement:

authentication
authorisation
file-size limits
virus and content scanning
secure temporary file handling
encrypted transport
audit logging
private object storage
data-retention controls
user access logs
role-based access control
explicit privacy policy
secure deletion of uploaded data

## Maintenance

The dataset schema and backend reasoning logic should be updated when new model types, embedding methods, biological signatures, or file formats are added.

## Future dataset extensions

Future versions may include:

real public single-cell example datasets
small h5ad examples
perturbation-response datasets
batch-effect examples
cell-type annotation examples
pathway-enrichment examples
model-output examples from scVI, Geneformer, or scGPT
benchmark datasets with known labels

## Contact

Website:
https://a-aidea.com

GitHub:
https://github.com/mpetalcorin

## Citation
**Petalcorin, M.I.R. (2026). BioFM Workflow Evaluator: A Full-Stack Biology Software Framework for Interpretable Bio Foundation Model Outputs, Single-Cell Workflow Quality Control, and Production-Ready Translational Decision Support. https://github.com/mpetalcorin/BioFM-Workflow-Evaluator- 
