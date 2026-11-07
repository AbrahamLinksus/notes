# Vector database types

> A vector database stores data as vectors (direction and magnitude) in a multi-dimensional space. The main types differ in where the vectors live: memory, disk, a cluster, or a graph.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 62–63)

## Key ideas
- **Main use case**: analysis tasks that group items, classify items and find relationships between items.
- A vector database stores data as mathematical objects defined by magnitude and direction.
- **Vector**: an array of numerical values describing features, placed in a multi-dimensional space.
- Types:
  1. **In-memory**: vectors live in RAM, so reads and writes are fast. E.g. Redis AI, TorchServe.
  2. **Disk-based**: vectors live on large disks, which suits large datasets. Uses indexing and compression techniques. E.g. Annoy.
  3. **Distributed**: vector data is spread across multiple nodes or servers. Gives horizontal scalability and fault tolerance, and suits high-throughput data. E.g. FAISS (Facebook AI Similarity Search).
  4. **Graph-based**: models the data as a graph to capture relationships. E.g. Amazon Neptune, Neo4j, TigerGraph.

## Example
```
our RAG build         → in-memory NumPy store (fine for a small corpus)
corpus outgrows RAM   → disk-based, with an index and compression
high traffic + HA     → distributed across nodes
relationships matter  → graph-based
```

| Type | Strength | Example |
|---|---|---|
| In-memory | fastest reads/writes | Redis AI |
| Disk-based | large data | Annoy |
| Distributed | scale + fault tolerance | FAISS |
| Graph-based | relationships | Neo4j |

## Pitfalls
- Picking in-memory for a corpus that won't fit in RAM.
- Assuming one type fits every workload. The choice depends on data size, throughput and whether relationships matter.

## Related
- [In-memory vector store](in-memory-vector-store.md)
- [HNSW and IVF](hnsw-and-ivf.md)
