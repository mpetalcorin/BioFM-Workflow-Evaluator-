# Model Card: BioFM Workflow Evaluator

## Model and system name

BioFM Workflow Evaluator by aAidea

## Version

Version 0.1.0

## Date

2026-04-29

## Developed by

A-aidea Ltd / aAidea

Scientific and technical lead:
Mark I.R. Petalcorin

Website:
https://a-aidea.com

Repository:
https://github.com/mpetalcorin/Biofm-Workflow-Evaluator-

## Intended use

BioFM Workflow Evaluator is intended as a full-stack scientific software demonstrator for evaluating biological model outputs, single-cell or omics-style workflows, quality-control metrics, biological plausibility, and production-readiness. It is designed to show how a biology software developer can turn biological foundation-model-like outputs into an interpretable, testable, and user-facing workflow.

The application may be used for portfolio demonstration, software engineering demonstration, educational purposes, computational biology prototyping, internal research discussions, and early-stage workflow design for drug discovery or perturbation biology.

## Out-of-scope use

The application is not intended for clinical diagnosis, patient stratification, treatment recommendation, regulatory decision-making, validated drug-discovery prioritisation, or use as a medical device. It should not be used as the sole basis for experimental decisions, clinical interpretation, or commercial drug-development claims.

## System type

The system is a hybrid software demonstrator composed of:

1. A React/Vite frontend for interactive scientific visualisation and user control.
2. A FastAPI backend for file upload, AnnData conversion, Scanpy-style preprocessing, quality-control reporting, embedding inspection, biological reasoning, and release-readiness scoring.
3. A simple transparent marker-based reasoning layer used to infer whether uploaded data contain gene features associated with broad biological states.

The current version is not a trained deep learning model. It is a workflow evaluator and reasoning demonstrator that can be extended with biological foundation models such as scGPT, Geneformer, scVI, or related single-cell representation-learning systems.

## Input data

Supported input file types:

h5ad
parquet
csv

Expected data content:

The backend expects expression-like or feature-matrix-like biological data. For CSV and parquet files, numeric columns are treated as features and non-numeric columns are treated as observations or metadata. For h5ad files, AnnData structure is read directly.

Example feature names used by the demonstrator include:

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

## Output data

The backend returns:

filename
file_type
qc_report
embedding_report
biological_reasoning
release_readiness_score
warnings

The frontend displays:

backend status
technical quality score
biological meaning score
release-readiness score
review-risk score
2D UMAP-like visualisation
3D molecular/state visualisation
radar chart
bar chart
workflow progression plot
quality-gate checklist
backend interpretation summary
exportable JSON report

## Biological reasoning logic

The current reasoning layer uses transparent marker-overlap scoring. It compares uploaded feature names against predefined marker sets for broad biological programmes:

Proliferative programme:
MKI67, TOP2A, PCNA, MCM2

Hypoxic or metabolic stress programme:
HIF1A, CA9, SLC2A1, LDHA

DNA damage or replication-stress programme:
CDKN1A, GADD45A, RAD51, CHEK1

Inflammatory programme:
IL6, CXCL8, NFKBIA, TNFAIP3

The marker-overlap score is combined with quality-control and embedding information to produce biological plausibility, pathway coherence, evidence support, and release-readiness scores.

## Quality-control logic

The backend computes:

number of cells or observations
number of genes or features
mean counts per cell or observation
mean genes per cell or observation
percentage of missing metadata
matrix sparsity

These metrics are used to inform the release-readiness score and warnings.

## Performance considerations

The app is designed for lightweight demonstration datasets and small-to-medium uploaded biological files. It is not currently optimised for very large single-cell atlases or GPU-scale foundation model inference. For larger datasets, future versions should include asynchronous processing, cloud object storage, background jobs, memory-aware sparse matrix handling, streaming upload, and queued model inference.

## Evaluation

The current version includes basic pytest tests for the backend health endpoint and biological reasoning logic. The system has been designed for transparency and software demonstration rather than benchmarked biological prediction performance.

Suggested future evaluation includes:

benchmarking on annotated single-cell datasets
comparison with known cell-type labels
comparison with known perturbation-response datasets
batch-effect sensitivity testing
missing-data robustness testing
runtime and memory profiling
reproducibility testing across environments
expert biological review of predictions

## Known limitations

The current version does not perform real scGPT, Geneformer, or scVI inference.

The frontend 2D UMAP-like view is illustrative unless connected to real backend embeddings.

The 3D molecular/state visualisation is a conceptual visual, not a true molecular structure viewer.

The marker-overlap approach is simplistic and does not capture gene expression magnitude, pathway activity, causal biology, temporal dynamics, cell-type context, or perturbation-specific mechanisms.

The release-readiness score is heuristic and should not be interpreted as a validated scientific confidence score.

The backend currently performs synchronous analysis, which is not ideal for very large datasets.

## Bias and risk considerations

The system may overstate biological meaning if uploaded feature names overlap with marker sets but expression levels or experimental context do not support the interpretation. It may understate biological meaning if relevant markers are missing, renamed, species-specific, or represented by alternative identifiers. It may be sensitive to inconsistent gene naming, incomplete metadata, batch effects, and small sample size.

Users should review outputs as hypotheses rather than conclusions.

## Ethical and safety considerations

This software is for research, education, and software demonstration. It is not a clinical tool. It should not be used to make patient-level decisions or validated therapeutic claims. Any drug-discovery or biological interpretation should be followed by rigorous computational validation, wet-lab validation, expert review, and appropriate regulatory oversight.

## Recommended use

Use the application to demonstrate:

production biology software design
FastAPI and React integration
AnnData and Scanpy-style workflows
file upload and backend analysis
transparent biological reasoning
single-cell workflow interpretation
quality-control and release-readiness logic
scientific dashboard design


## Citation and acknowledgement

If reused in a portfolio, website, or scientific software demonstration, acknowledge:

BioFM Workflow Evaluator by aAidea, developed by Mark I.R. Petalcorin.

**Petalcorin, M.I.R.** (2026). BioFM Workflow Evaluator: A Full-Stack Biology Software Framework for Interpretable Bio Foundation Model Outputs, Single-Cell Workflow Quality Control, and Production-Ready Translational Decision Support. https://github.com/mpetalcorin/BioFM-Workflow-Evaluator- 

## Contact

Website:
https://a-aidea.com

GitHub:
https://github.com/mpetalcorin
