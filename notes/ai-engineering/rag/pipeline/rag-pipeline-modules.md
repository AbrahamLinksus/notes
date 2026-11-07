# RAG pipeline modules

> A from-scratch RAG pipeline is eight modules, each with one responsibility, orchestrated into two public flows: `index()` and `query()`.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 58, 61)

## Key ideas
- Each module's single responsibility:
  - `loader.py`: turns raw files into clean, deduplicated `Document` objects with metadata.
  - `chunker.py`: splits a Document's text into `Chunk` objects using a configurable strategy.
  - `embedder.py`: attaches an embedding vector to each Chunk.
  - `vector_store.py`: stores normalised vectors and metadata, and answers top-k similarity queries.
  - `retriever.py`: turns a raw query string into ranked, thresholded `SearchResult` objects.
  - `context_assembly.py`: formats the SearchResult list into one prompt-ready context string.
  - `generator.py`: builds a grounded prompt, calls the LLM, and resolves citations.
  - `pipeline.py`: orchestrates everything into `index()` and `query()`.
- All the knobs live in one `Config`, so a change in one place flows through the whole pipeline.

## Example
```python
class Config:
    EMBEDDING_MODEL = "BAAI/bge-small-en-v1.5"
    EMBEDDING_DIM = 384
    CHUNK_SIZE = 1000
    CHUNK_OVERLAP = 200
    CHUNK_STRATEGY = "recursive"
    RETRIEVAL_K = 5
    SCORE_THRESHOLD = 0.3
    MMR_LAMBDA = 0.6
    MMR_CANDIDATE_POOL = 20
    LLM_TEMPERATURE = 0.1
    LLM_MODEL = "gpt-4o-mini"

class RAGPipeline:
    def __init__(self, llm, config=Config()):
        self.config, self.llm = config, llm
        self.store = VectorStore(dim=config.EMBEDDING_DIM)

    def index(self, folder_path: str) -> None:       # ingest → chunk → embed → store
        all_chunks = []
        for doc in build_documents(folder_path):
            all_chunks.extend(chunk_document(doc, strategy=self.config.CHUNK_STRATEGY,
                              chunk_size=self.config.CHUNK_SIZE, overlap=self.config.CHUNK_OVERLAP))
        self.store.add(embed_chunks(all_chunks))
```
`query()`: retrieve → assemble context → generate answer with citations.

## Pitfalls
- Letting modules leak into each other's jobs (e.g. the store embedding queries). That's where coupling bugs come from.
- Changing `EMBEDDING_MODEL` without changing `EMBEDDING_DIM` and re-indexing.

## Related
- [Format-specific extraction](../ingestion/format-specific-extraction.md)
- [Chunking strategies](../chunking/chunking-strategies.md)
- [Retriever design](../retrieval/retriever-design.md)
- [Context assembly](context-assembly.md)
- [Grounding and failure modes](grounding-and-failure-modes.md)
