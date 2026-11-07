# Routing and query construction

> Routing decides which data source should handle a query, and query construction splits the question into a semantic search term plus metadata filters that narrow the pool before similarity search.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 82–83)

## Key ideas
- **Routing**: given a query, which data source should handle it?
  - **Logical routing**: give the LLM a description of the existing data sources and let it choose the right one.
  - **Semantic routing**: embed the question and route it based on its semantic meaning, i.e. by similarity to embedded prompts or routes.
- **Query construction**: turn a natural-language question into a structured query, *bifurcating* (splitting in two) it into:
  1. the **semantic search term**, and
  2. the **logical conditions** (metadata filters) that narrow the candidate pool *before* similarity search.
- How: bind a Pydantic model to the LLM so it extracts the metadata filters from the query you pass in.
- In plain words: pull the metadata out of the input query and use it to filter the candidate pool before searching.
- The same idea shows up as text-to-SQL, text-to-Cypher and a self-query retriever, depending on the target store.

## Example
```python
from pydantic import BaseModel

class Search(BaseModel):
    query: str               # semantic part
    year: int | None = None  # filter
    format: str | None = None

structured_llm = llm.with_structured_output(Search)
structured_llm.invoke("videos about LangChain agents from 2024")
# Search(query="LangChain agents", year=2024, format="video")
#   → filter(year=2024, format="video") → similarity_search("LangChain agents")
```

## Pitfalls
- Embedding the whole question, filters and all. "from 2024" barely moves a dense vector, so it has to be a filter.
- Logical routing depends on how well you describe each source to the LLM.
- Filtering first can shrink the pool below k. Handle that.

## Related
- [Retriever design](../retrieval/retriever-design.md)
- [Prompt templates and output parsers](../../langchain/prompt-templates-and-output-parsers.md)
- [Document metadata](../ingestion/document-metadata.md)
