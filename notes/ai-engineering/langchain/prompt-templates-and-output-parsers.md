# Prompt templates and output parsers

> Chat prompt templates inject the user's variables into a reusable message structure, and output parsers turn the model's text back into clean strings, dicts or validated Pydantic objects.

studied: 2026-11-07 · status: done · source: llms_rag.pdf (pp. 66–68)

## Key ideas
- **ChatPromptTemplate**: injects string variables from the user into the prompt sent to the model. Define it once and reuse it with different values.
- Message types:
  - `SystemMessage`: sets the behaviour and persona (defines who the AI is).
  - `HumanMessage`: the user's input.
  - `AIMessage`: model responses, including previous ones.
  - `ToolMessage`: results from tools or function calls.
- **Output parsers** convert the model's formatted text output into structured data (e.g. JSON):
  - `StrOutputParser`: the simplest. Pulls clean text out of an AIMessage.
  - `JsonOutputParser`: parses the output into a Python dict.
  - `PydanticOutputParser` (recommended): define a schema → it generates format instructions → you get back a validated object. Gives type safety, IDE support and error handling.
- `with_structured_output(Model)`: binds the schema directly to the LLM and returns the Pydantic object.

## Example
```python
from pydantic import BaseModel, Field

class Person(BaseModel):
    name: str = Field(description="The person's name")
    age: int = Field(description="The person's age")
    occupation: str = Field(description="The person's occupation")

parser = PydanticOutputParser(pydantic_object=Person)
prompt = ChatPromptTemplate.from_template(
    "Return a JSON with 'name', 'age', and 'occupation' for: {description}\n{format_instructions}"
).partial(format_instructions=parser.get_format_instructions())

chain = prompt | llm | parser
chain.invoke({"description": "A 30-year-old artist named Maria"})
# Person(name='Maria', age=30, occupation='artist')

class MovieReview(BaseModel):
    title: str
    review: str
    rating: int                       # out of 10

llm.with_structured_output(MovieReview).invoke("Review: Inception is a mind-bending thriller. 9/10")
```

## Pitfalls
- Forgetting `format_instructions` with `PydanticOutputParser`. The model never learns the schema.
- Using `JsonOutputParser` when you need guaranteed types. Only Pydantic validates them.
- Putting user text into the system message instead of the human message.

## Related
- [LangChain ecosystem](langchain-ecosystem.md)
- [Prompt engineering](../llms/prompting/prompt-engineering.md)
- [Routing and query construction](../rag/advanced/routing-and-query-construction.md)
