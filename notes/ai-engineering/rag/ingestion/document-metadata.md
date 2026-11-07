# Document metadata

> The Document object owns its metadata: it's a container for the clean text plus stable identifiers and attributes, captured once at ingestion when the information is still unambiguous.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 29–30, 32)

## Key ideas
- **Who owns the metadata?** The Document object. After ingestion the information becomes unambiguous, so it belongs with the text.
- A Document is a container for the clean input text and that text's metadata.
- Core fields:
  - `text`: the clean text.
  - `source_path`: a stable identifier for where the file came from.
  - `format`: pdf, docx, txt, md or html.
  - `doc_id`: a stable unique identifier for the document.
  - `ingested_at`: a UTC timestamp.
  - `page_count`: None for formats without pages (txt, md).
  - `section`: a heading or section name, if one can be extracted.
  - `content_hash`: for exact-match dedup.
- Other useful attributes: character count, file size and extraction method.
- **The loader's job (`loader.py`)**: find the files in the target directory, load and clean them, and return a list of Documents with their metadata.

## Example
```python
from dataclasses import dataclass, field
from datetime import datetime, timezone

@dataclass
class Document:
    text: str
    source_path: str
    format: str                       # "pdf", "docx", "txt", "md", "html"
    doc_id: str                       # stable unique id
    ingested_at: datetime = field(default_factory=lambda: datetime.now(timezone.utc))
    page_count: int | None = None     # None for formats without pages
    section: str | None = None
    content_hash: str | None = None   # for exact dedup
```

## Pitfalls
- Using a doc ID that changes between runs. Citations and dedup both depend on it staying stable.
- Faking a page count for formats that don't have pages. Use None.
- Adding metadata later in the pipeline, after the text has been merged and the source is no longer clear.

## Related
- [Format-specific extraction](format-specific-extraction.md)
- [Deduplication](deduplication.md)
- [Retriever design](../retrieval/retriever-design.md)
- [LangChain ecosystem](../../langchain/langchain-ecosystem.md)
