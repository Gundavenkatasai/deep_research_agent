Engineering Oracle

Multi-Agent RAG Research & Benchmark Engine built with LangGraph, OpenRouter free-tier models, and Next.js 15.

Overview

Engineering Oracle is a multi-agent system that performs automated research, analysis, and benchmarking across technical topics.

It orchestrates multiple specialized agents to:

Discover relevant sources
Extract and clean data
Analyze performance and code patterns
Evaluate relevance
Generate structured reports

The system uses a supervisor loop to improve output quality until a confidence threshold is met.

Architecture
Query → [Discovery] → [Harvest] → [Clean] → [Reasoning] → [Evaluation] → [Synthesis]
              ↑                                                    |
              └──────────── Supervisor (score < 0.8) ──────────────┘
Agent Pipeline
1. Discovery
Performs web search using DuckDuckGo
Falls back to Tavily if fewer than 3 high-quality results
2. Harvest
Parallel scraping of web pages
GitHub repository cloning
PDF downloading
3. Clean
PDF parsing using PyMuPDF4LLM
Document chunking for embeddings
README extraction for repositories
4. Reasoning
Uses MiMo V2 Flash
Analyzes:
FLOPs
Latency
Code patterns
Architectural trade-offs
5. Evaluation
Embedding-based similarity scoring using ChromaDB
Threshold: 0.8
Re-routes pipeline if score is below threshold
6. Synthesis
Uses Llama 3.3 70B
Generates structured Markdown reports
Tech Stack
Orchestration
LangGraph (Supervisor + Evaluator pattern)
Search
DuckDuckGo
Tavily API
Extraction
Scrapy + Playwright
GitPython
PDF Parsing
PyMuPDF4LLM
LLMs (via OpenRouter)
Llama 3.3 70B
MiMo V2 Flash
Gemini 2.0 Flash
Embeddings
sentence-transformers/all-MiniLM-L6-v2
ChromaDB
Backend
FastAPI
Server-Sent Events (SSE) for streaming
Frontend
Next.js 15
Tailwind CSS
Shadcn/UI
Vercel AI SDK
Features
Multi-agent RAG pipeline
Supervisor-based iterative refinement
Real-time streaming responses
Automated research + benchmarking
GitHub + PDF + web ingestion
Embedding-based evaluation loop
Quick Start
1. Environment Setup
cp .env.example .env

Add the following keys:

OPENROUTER_API_KEY=your_key
TAVILY_API_KEY=your_key
2. Run with Docker (Recommended)
docker-compose up --build
3. Manual Setup
Backend
cd backend
pip install -e .
uvicorn app.main:app --reload
Frontend
cd frontend
npm install
npm run dev
4. Access the App
http://localhost:3000
Project Structure
.
├── backend/
│   ├── app/
│   ├── agents/
│   ├── services/
│   └── main.py
├── frontend/
│   ├── app/
│   ├── components/
│   └── lib/
├── docker-compose.yml
├── .env.example
└── README.md
Evaluation Logic
Uses cosine similarity via embeddings
Threshold: 0.8
If below threshold:
Supervisor re-triggers pipeline
Improves data quality before synthesis
Use Cases
Research automation
Model benchmarking
Codebase analysis
Technical report generation
AI-assisted literature review
License

MIT

If you want this to actually get shortlisted, one blunt fix:

Problem: This reads like a system design doc, not a product.
Why it hurts: Recruiters scan for impact, not architecture depth.
Fix:
Add this right after Overview:

## Key Results

- Reduced research time by X% (benchmark it)
- Processes X sources per query
- Average response latency: X seconds
- Achieves >0.8 relevance score in X% of runs
