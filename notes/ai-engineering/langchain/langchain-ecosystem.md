# LangChain ecosystem

> LangChain is a Python framework that adds functionality around LLMs. It's split into core, chains/agents, LangGraph, LangSmith and LangServe, and its `Document` is just page content plus a free-form metadata dict.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 64–65)

## Key ideas
- **LangChain**: a Python framework for giving LLMs extra functionality.
- **Hugging Face**: an open-source community that provides AI/ML models and tools.
- Core packages:
  1. `langchain-core`: core abstractions and LCEL.
  2. `langchain`: agents, chains and the high-level API.
  3. `langgraph`: stateful agent orchestration.
  4. `langsmith`: tracing and evaluation.
  5. `langserve`: deploy a chain as a REST API.
- **Indexing** in LangChain terms: take a document, **load, split and embed** it into a numerical representation.
- **Document model** (`langchain_core.documents`): `Document(page_content: str, metadata: dict = {})`.
  - The metadata is a **free dict** on purpose. It doesn't enforce a schema, so each loader can fill it in based on what the document is.

## Example
```python
from langchain_core.documents import Document

pdf_doc = Document(page_content="Leave policy...", metadata={"source": "hr.pdf", "page": 4})
web_doc = Document(page_content="Blog text...",   metadata={"source": "https://...", "title": "Agents"})
# same class, different metadata keys, decided by each loader
```
```
my from-scratch build            LangChain
loader.py → Document dataclass   document loaders → Document(page_content, metadata)
chunker.py                       text splitters
embedder.py / vector_store.py    embeddings + vector stores
```

## Pitfalls
- Expecting `metadata` to have the same keys across loaders. It doesn't, so check before filtering on a key.
- Mixing up LangChain's "indexing" (load → split → embed) with ANN indexing structures like HNSW.
- Putting orchestration logic into `langchain` chains when it needs state. That's LangGraph's job.

## Related
- [Prompt templates and output parsers](prompt-templates-and-output-parsers.md)
- [LangGraph basics](langgraph-basics.md)
- [RAG from scratch in LangChain](rag-from-scratch.md)
- [Document metadata](../rag/ingestion/document-metadata.md)
