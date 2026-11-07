# RAG from scratch in LangChain

> The "RAG from scratch" map has six stages: query construction, query translation, routing, retrieval, indexing and generation. The basic build counts tokens with tiktoken, embeds with OpenAI (1536 dims), compares by cosine, and retrieves k nearby chunks.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 71–73)

## Key ideas
- The overview map:
  - **Query construction**: text-to-SQL (relational DBs), text-to-Cypher (graph DBs), self-query retriever (vector DBs).
  - **Query translation**: multi-query, RAG-Fusion, decomposition, step-back, HyDE.
  - **Routing**: logical and semantic.
  - **Retrieval**: ranking and refinement (re-rank, RankGPT, RAG-Fusion), CRAG, active retrieval.
  - **Indexing**: chunk optimisation (semantic splitter), multi-representation, specialised embeddings (fine-tuning, ColBERT), hierarchical indexing (RAPTOR).
  - **Generation**: active retrieval (Self-RAG, RRR).
- **Indexing** is the step where embedded chunks are organised into a structure that supports fast similarity search.
- **tiktoken** is OpenAI's BPE tokenizer (text → numeric tokens). Rule of thumb: about 4 characters per token.
- **OpenAIEmbeddings**: `embed_query` and `embed_documents` both return vectors of length **1536**.
- Cosine similarity is the recommended comparison for OpenAI embeddings (1 = identical).
- **Retrieval**: `k` is the number of nearby chunks to retrieve.

## Example
```python
import tiktoken
def num_tokens_from_string(string: str, encoding_name: str) -> int:
    return len(tiktoken.get_encoding(encoding_name).encode(string))
num_tokens_from_string("What kinds of pets do I like?", "cl100k_base")

from langchain_openai import OpenAIEmbeddings
embd = OpenAIEmbeddings()
q = embd.embed_query("What kinds of pets do I like?")
d = embd.embed_query("My favorite pet is a cat.")
len(q)   # 1536

import numpy as np
cos = np.dot(q, d) / (np.linalg.norm(q) * np.linalg.norm(d))

import bs4
from langchain_community.document_loaders import WebBaseLoader
loader = WebBaseLoader(web_paths=("https://.../agent/",),
    bs_kwargs=dict(parse_only=bs4.SoupStrainer(class_=("post-content", "post-title", "post-header"))))
docs = loader.load()
```

## Pitfalls
- Mixing embedding models between indexing and querying. A 1536-dim OpenAI vector can't be compared with a 384-dim bge vector.
- Loading web pages without `SoupStrainer` pulls in navigation and footer boilerplate.
- Picking k without checking the generator's token budget.

## Related
- [BPE tokenizer](../llms/fundamentals/bpe-tokenizer.md)
- [LangChain ecosystem](langchain-ecosystem.md)
- [Multi-query and RAG-Fusion](../rag/advanced/multi-query-and-rag-fusion.md)
- [RAPTOR and ColBERT](../rag/advanced/raptor-and-colbert.md)
- [Context assembly](../rag/pipeline/context-assembly.md)
