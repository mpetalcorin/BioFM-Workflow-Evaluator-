# BioFM Workflow Evaluator <img width="1603" height="1056" alt="Screenshot 2026-04-29 at 14 30 25" src="https://github.com/user-attachments/assets/eff2132d-f978-46f3-b79e-d183002e50a5" />
BioFM Workflow Evaluator is a full-stack scientific software demonstrator for evaluating Bio Foundation Model outputs, single-cell and perturbation-biology workflows, biological plausibility, quality-control status, and production-readiness. The application combines a React/Vite frontend with a FastAPI backend that supports AnnData-style data handling, Scanpy-style preprocessing, biological reasoning, backend health checks, file upload, demo dataset analysis, 2D and 3D visualisations, and exportable JSON reports.

The project was developed by aAidea as an example of how biology-facing software can translate complex model outputs into interpretable, testable, and user-facing workflows for drug discovery, biological data science, and computational biology product development.

## Live application

Frontend:
https://biofm-workflow-evaluator.vercel.app/

Backend API, after deployment:
https://biofm-workflow-api.onrender.com/

GitHub repository:
https://github.com/mpetalcorin/Biofm-Workflow-Evaluator-

## Purpose

Modern biological foundation models and single-cell analysis tools can generate embeddings, predicted cell states, perturbation responses, and numerical scores. However, these outputs are only useful in discovery settings if they can be assessed for technical reliability, biological plausibility, evidence strength, and production-readiness. BioFM Workflow Evaluator provides a practical software pattern for bridging that gap.

The application is designed to demonstrate how a biology software developer can combine production-grade software engineering with biological reasoning. It shows how model outputs may be contextualised using quality-control metrics, file-format awareness, pathway coherence, marker-gene logic, perturbation plausibility, backend validation, and exportable reporting.

## Main features

The frontend provides a dark scientific dashboard with active controls for running demo analyses, checking backend health, preprocessing uploaded datasets, performing release checks, pausing or resuming backend calls, resetting state, and exporting reports.

The backend provides FastAPI endpoints for health checks and dataset analysis. Uploaded files are handled through an AnnData-compatible workflow. CSV and parquet files are converted into AnnData objects, while h5ad files are read directly. The backend computes quality-control metrics, performs Scanpy-style preprocessing where possible, checks available embeddings, applies a marker-based biological reasoning layer, and returns a release-readiness score.

The application includes a 2D UMAP-like visualisation, a lightweight 3D molecular/state visualisation, radar charts, bar charts, line charts, radial release-readiness scoring, quality-gate checklists, backend interpretation panels, and JSON export.

## Technology stack

Frontend:
React
Vite
Tailwind CSS
Recharts
Framer Motion
Lucide React

Backend:
Python
FastAPI
Uvicorn
Pydantic
AnnData
Scanpy
NumPy
Pandas
SciPy
scikit-learn
PyArrow
h5py
pytest

Deployment targets:
Vercel for frontend
Render for backend
GitHub for source control and CI/CD

## Project structure

biofm-workflow-evaluator/
├── src/
│   ├── App.jsx
│   ├── index.css
│   └── main.jsx
├── backend/
│   ├── app/
│   │   ├── __init__.py
│   │   ├── main.py
│   │   ├── schemas.py
│   │   ├── anndata_pipeline.py
│   │   ├── embedding_pipeline.py
│   │   └── biological_reasoning.py
│   ├── tests/
│   │   ├── test_health.py
│   │   └── test_reasoning.py
│   ├── demo_data/
│   │   └── demo_expression.csv
│   ├── requirements.txt
│   ├── pytest.ini
│   └── Dockerfile
├── .github/
│   └── workflows/
│       └── ci.yml
├── package.json
├── vite.config.js
├── docker-compose.yml
├── README.md
├── modelcard.md
└── datasheet.md

## Local frontend setup

From the project root:

```bash
npm install
npm install lucide-react recharts framer-motion
npm install -D tailwindcss @tailwindcss/vite
npm run dev
```

The frontend usually runs at:

http://localhost:5173/

## Local backend setup

From the backend folder:

```bash
cd backend
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

The backend runs at:

http://localhost:8000

API documentation is available at:

http://localhost:8000/docs

## Environment variable

For local frontend-backend communication, create a `.env.local` file in the project root:

```bash
VITE_API_BASE_URL=http://localhost:8000
```

For production deployment on Vercel, set:

```bash
VITE_API_BASE_URL=https://biofm-workflow-api.onrender.com
```

or replace the value with the actual deployed backend URL.

## Backend endpoints

GET /api/health

Returns backend health status.

POST /api/analyse

Accepts an uploaded `.h5ad`, `.parquet`, or `.csv` file and returns quality-control metrics, embedding information, biological reasoning output, release-readiness score, and warnings.

## Example backend test

Run the backend, then from the project root:

```bash
curl http://localhost:8000/api/health
```

Expected response:

```json
{"status":"ok","service":"BioFM Workflow Evaluator API"}
```

Test uploaded demo data:

```bash
curl -X POST \
  -F "file=@backend/demo_data/demo_expression.csv" \
  http://localhost:8000/api/analyse
```

## Testing

From the backend folder:

```bash
pytest
```

The tests cover the health endpoint and the biological reasoning module.

## Deployment

Frontend deployment is intended for Vercel. Backend deployment is intended for Render.

Render backend settings:

Root Directory:
backend

Build Command:
pip install -r requirements.txt

Start Command:
uvicorn app.main:app --host 0.0.0.0 --port $PORT

Vercel frontend settings:

Build Command:
npm run build

Output Directory:
dist

Production environment variable:
VITE_API_BASE_URL=https://biofm-workflow-api.onrender.com

## Scientific interpretation

The current biological reasoning module is a transparent demonstrator rather than a validated diagnostic or clinical model. It uses marker-overlap logic and quality-control-derived scores to infer whether outputs appear biologically plausible. The software should be interpreted as a research and portfolio platform, not as a medical device or a clinical decision-support system.

## Limitations

The demo does not currently run real scGPT, Geneformer, or scVI inference. Placeholder hooks are included for future extension. The 2D and 3D visualisations in the frontend are demonstrative and should not be interpreted as real embeddings or molecular structures unless connected to validated backend outputs. The marker-based biological reasoning layer is intentionally simple and should be replaced or extended for real production research use.

## Future development

Planned extensions include real scVI latent embeddings, scGPT or Geneformer inference, UMAP coordinate export from backend to frontend, batch-effect diagnostics, marker-gene heatmaps based on uploaded data, pathway enrichment, perturbation-response ranking, user authentication, persistent analysis history, cloud object storage, Dockerized deployment, CI/CD hardening, and expanded model-card and datasheet reporting.

## Licence

MIT

## Author

Developed by aAidea.

Director and scientific lead:
Mark I. R. Petalcorin

Website:
https://a-aidea.com

GitHub:
https://github.com/mpetalcorin

