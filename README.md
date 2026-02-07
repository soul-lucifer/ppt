# AI Presentation Generator (Free Models)

## Overview
- Frontend: Next.js 14 on Vercel
- Backend: FastAPI + Hugging Face FLAN-T5-small + python-pptx (deploy on Railway/Render/Cloud Run)

## Quick Start

### Backend (local)
cd backend
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --host 0.0.0.0 --port 8000 --reload

Test: http://localhost:8000/health

### Frontend (local)
cd frontend
npm install
npm run dev
Frontend will expect BACKEND_URL (default http://localhost:8000)

## Deploy

### Backend
- Railway: create new service from repo, set env `PORT=8000`.
- Render: Web Service, Start command: `uvicorn main:app --host 0.0.0.0 --port $PORT`
- Cloud Run: build Dockerfile and deploy.

Set env:
- HF_HOME (optional, for cache)
- MODEL_NAME (default google/flan-t5-small)
- PORT (Railway/Render)

### Frontend (Vercel)
- Import `frontend` folder as project.
- Env vars:
  - NEXT_PUBLIC_BACKEND_URL=https://<your-backend-host>
- Build command: `npm run build`
- Output: `.next`

## API (backend)
- POST /api/generate { topic, num_slides (5-20), style }
  returns { job_id, status }
- GET /api/status/{job_id}
- GET /api/download/{job_id} -> PPTX file

## Notes
- Uses free HF model flan-t5-small (fast, no key).
- Not production-hardened; add auth/rate limits for production.