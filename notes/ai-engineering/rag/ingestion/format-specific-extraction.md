# Format-specific extraction

> Ingestion turns every file on disk into one consistent representation (clean text + metadata), and each file format needs its own extraction path because each one stores content differently.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 25–27)

## Key ideas
- **Goal of ingestion**: take the files on disk and normalise them into one internal representation, clean text plus metadata. It soaks up all the format-specific mess so nothing downstream has to deal with it.
- Each format needs its own extraction path because the underlying storage model is different:
  - **.txt / .md**: no extraction needed. The bytes on disk decode straight to a string.
  - **PDF**: stores a *layout description*, meaning instructions for where to draw each glyph at given coordinates on a page, with no inherent order. The extraction library has to reconstruct the text, and different libraries can give meaningfully different text from the same file.
  - **.docx**: stores content as structured XML. Paragraphs, runs and tables are explicit elements of the document tree, so paragraphs and tables get separate handling.
- **Capture metadata at ingestion time.** After this stage the content gets merged or converted, and the source information is lost. If you'll ever need citations, the source metadata has to be carried forward from here.

## Example
```python
from pypdf import PdfReader

def extract_pdf(path: str) -> tuple[str, dict]:
    reader = PdfReader(path)
    pages = [page.extract_text() or "" for page in reader.pages]  # "" for image-only pages
    text = "\n\n".join(pages)
    meta = {"source": path, "format": "pdf", "num_pages": len(reader.pages)}
    return text, meta

def extract_txt(path: str) -> tuple[str, dict]:
    with open(path, "r", encoding="utf-8-sig") as f:   # utf-8-sig strips a BOM
        return f.read(), {"source": path, "format": path.split(".")[-1]}
```

## Pitfalls
- Trusting PDF text order. It's rebuilt from coordinates, so check the output.
- Image-only PDF pages return no text at all, which leaves empty strings, not errors.
- Flattening a .docx into paragraphs only and silently dropping its tables.
- Throwing away the source path or page count here makes citations impossible later.

## Related
- [Text cleaning](text-cleaning.md)
- [Document metadata](document-metadata.md)
- [Deduplication](deduplication.md)
- [RAG pipeline modules](../pipeline/rag-pipeline-modules.md)
