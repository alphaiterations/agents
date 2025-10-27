## react-agent.ipynb — Overview

This repository contains a Jupyter notebook `react-agent.ipynb` that implements a REACT-style agent for medical question answering using a combination of local datasets, a vector store, simple tools, web search, and an LLM.

Read the full article on Medium here: [Build ReAct Agent from Scratch using LangGraph](https://medium.com/@alphaiterations/agentic-ai-build-react-agent-using-langgraph-facac8ae6031)








What the notebook does
- Loads two CSV datasets: `medical_q_n_a.csv` (medical Q&A) and `Hospitals.csv` (US hospitals).
- Prepares the medical Q&A text for embedding and stores it in a Chromadb collection.
- Uses sentence-transformers / FAISS embeddings (via Chroma) to retrieve relevant medical context.
- Provides tool functions for: retrieving Q&A context, performing web searches (Google Serper wrapper), geocoding an address, and searching for nearest hospitals by haversine distance.
- Builds an agent/workflow graph using `langgraph` that calls an LLM and then stateless tools until the agent finds an ANSWER.

Key libraries used (from the notebook)
- pandas, numpy
- faiss-cpu, sentence-transformers
- chromadb
- openai (OpenAI Python client)
- langchain_community (Google Serper wrapper)
- langgraph
- scikit-learn, seaborn
- python-dotenv
- requests

Environment variables
- `OPEN_AI_KEY` — OpenAI API key used in the notebook (noting the notebook reads `OPEN_AI_KEY`).
- `SERPER_API_KEY` — API key for Serper (Google search wrapper).
- `GEOCODE_API_KEY` — (optional) Geocoding API key if you use a paid provider.

Quick setup
1. Create and activate a Python environment (recommended Python 3.10+).
2. Install dependencies from `requirements.txt`:

```bash
python -m pip install -r requirements.txt
```

3. Copy your API keys into a `.env` file in the repo root (or export as env vars):

```
OPEN_AI_KEY=sk-...
SERPER_API_KEY=...
GEOCODE_API_KEY=...
```

4. Open and run `react-agent.ipynb` in JupyterLab / Jupyter Notebook. Use a Python kernel matching your environment.

Notes about models and "Claude Sonnet 4"
- The notebook uses the OpenAI client. Enabling or switching to Anthropic's Claude (e.g., "Claude Sonnet 4") is an external provider action and typically requires configuring the client SDK or the orchestration layer that calls the model. This repository does not automatically enable external models for clients.
- If you want to use Claude Sonnet 4 in place of the OpenAI calls, you will need to:
  1. Install and configure the appropriate client SDK (Anthropic/Anthropic's Python package or a third-party wrapper).
  2. Replace the `get_llm_response` function to call the Claude Sonnet 4 model endpoint and provide your Anthropic API key (or provider configuration) via environment variables.

Example: replace internals of `get_llm_response` with your chosen provider's client call and update env var names.

Security & privacy
- The notebook demonstrates calls to external services and stores data locally in `chroma_db/` — do not commit secrets or API keys.

Next steps / suggestions
- Run the notebook top-to-bottom to verify behavior in your environment.
- If you prefer strict dependency pinning for reproducibility, we can: 1) generate a frozen `requirements.txt` using `pip freeze`, or 2) pin versions for `langgraph`/other newly added packages after testing.

---
Generated on 2025-10-27 — summary created from `react-agent.ipynb`.
