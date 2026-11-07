# LangGraph basics

> LangGraph builds an app as a graph: a typed shared State flows through Nodes (functions), ToolNodes run tools, and a StateGraph compiles it all into a Runnable.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 69–70)

## Key ideas
- **Type annotations**: give a structure fixed options and types, so errors and complexity don't spread further down the graph.
- **State**: the shared data structure that holds the current information, or context, of the whole application. Every node reads it and writes back to it.
- **Node**: an individual function or operation that performs one specific task within the graph.
- **ToolNode**: a special kind of node whose only job is to run a tool.
- **StateGraph**: the LangGraph class used to build and compile the graph structure.
- **Runnable**: the standard executable component. A compiled graph is one, so it's invoked like any other chain.
- Put together: you define the State type, add Nodes and ToolNodes to a StateGraph, connect them, and compile to get a Runnable.

## Example
```python
from typing import TypedDict

class State(TypedDict):          # type annotations = fixed shape for the shared state
    question: str
    context: list[str]
    answer: str
```
```
           ┌──────────── State {question, context, answer} ────────────┐
START ──► [retrieve node] ──► [ToolNode: search tool] ──► [generate node] ──► END
             writes context        writes context             writes answer

StateGraph(State) → add nodes → connect → compile() → Runnable → .invoke({"question": ...})
```

## Pitfalls
- Leaving the State untyped. Nodes then disagree on keys, and the errors show up far from where they started.
- Running tool calls inside an ordinary node instead of a ToolNode muddies each node's single job.
- Forgetting to compile. The StateGraph is only a builder until it becomes a Runnable.

## Related
- [LangChain ecosystem](langchain-ecosystem.md)
- [Prompt templates and output parsers](prompt-templates-and-output-parsers.md)
- [Prompt engineering](../llms/prompting/prompt-engineering.md)
