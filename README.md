# historical-figures-rag

Starter structure for a collaborative HistoryChat RAG application.

## Planned stack

- LangChain
- FAISS
- OpenAI embeddings
- OpenAI / Grok as LLM providers
- Streamlit interface

## Project structure

- `app/streamlit/` - Streamlit UI entrypoint and pages
- `assets/avatars/` - generated or curated character images
- `config/` - shared configuration and character profiles
- `data/` - source documents, processed text, chat history
- `docs/` - architecture and team notes
- `logs/` - local logs for retrieval and app runs
- `prompts/` - system and character prompts
- `scripts/` - helper scripts for ingest/build tasks
- `src/` - application logic
- `tests/` - unit and integration tests
- `vector_store/faiss/` - local FAISS indexes