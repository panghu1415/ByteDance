# AI Testcase Agent Architecture

## Current Runtime

This project now runs as a Streamlit frontend plus a FastAPI backend.

```powershell
# Terminal 1: backend
python -m uvicorn fastapi_backend:app --host 127.0.0.1 --port 8000

# Terminal 2: frontend
python -m streamlit run ai_testcase_agent_app_v7_fast_langgraph.py --server.port 8502
```

## Layers

```text
ai_testcase_agent_app_v7_fast_langgraph.py
  Thin Streamlit entrypoint.

src/testcase_agent_app/ui/
  Streamlit frontend pages and interaction state.

src/testcase_agent_app/api/
  FastAPI backend routes for document parsing, generation, evaluation, revision, and Agent workflow execution.

src/testcase_agent_app/services/
  Business capabilities:
  - document_service.py: Feishu document reading
  - rag_service.py: local RAG indexing and retrieval
  - generation_service.py: quick and detailed testcase generation
  - evaluation_service.py: rule metrics, human baseline F1, LLM Judge, hallucination check
  - revision_service.py: LLM-based testcase revision and dedup
  - export_service.py: CSV / Markdown / Excel export

src/testcase_agent_app/workflows/
  Agent orchestration. LangGraph workflow is wrapped here so UI code does not directly own orchestration.

src/testcase_agent_app/schemas/
  Shared dataclasses for runtime config and agent inputs.

src/testcase_agent_app/config.py
  App-level defaults.
```

## Why This Shape

The UI layer is responsible for display and user interaction. Model calls, Feishu parsing, generation, evaluation, revision, and LangGraph orchestration are exposed through FastAPI routes and implemented behind service/workflow boundaries.
