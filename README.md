## Design and Implementation of a Multidocument Retrieval Agent Using LlamaIndex

### AIM:
To design and implement a multidocument retrieval agent using LlamaIndex to extract and synthesize information from multiple research articles, and to evaluate its performance by testing it with diverse queries, analyzing its ability to deliver concise, relevant, and accurate responses.

### PROBLEM STATEMENT:

Accessing and synthesizing information from multiple documents is crucial for research, but manual analysis is time-consuming. A multidocument retrieval agent can automate this process by:

1. Parsing and indexing multiple research articles.
2. Enabling users to ask queries in natural language.
3. Providing synthesized, concise, and accurate responses from the indexed documents.

The effectiveness of the system will be evaluated through diverse queries to test its accuracy and relevance.

### DESIGN STEPS:

#### STEP 1: Load and Parse Research Articles
Use LlamaIndex's document loaders to read and parse multiple research articles in PDF or text format.

#### STEP 2: Create a Unified Index
Combine and index content from all documents using LlamaIndex to enable cross-document retrieval.

#### STEP 3: Set Up a Query Engine
Configure a query engine to allow natural language questions and retrieve relevant content.

#### STEP 4: Implement the Retrieval Agent
Build a retrieval agent that extracts and synthesizes information from the index.

#### STEP 5: Evaluate the Agent
Test the agent with diverse queries to evaluate the quality of its responses.

### Developed By

**Name:** AMIRTHA VARSHINI M

**Register Number:** 212224230017

### PROGRAM:
```python
from helper import get_openai_api_key
OPENAI_API_KEY = get_openai_api_key()
```
```python
import nest_asyncio
nest_asyncio.apply()
```
```python
urls = [
    "https://openreview.net/pdf?id=jHDZEUgS4r",
    "https://openreview.net/pdf?id=CCSPm6V5EF",
    "https://openreview.net/pdf?id=krGpQzo8Mz",
    "https://openreview.net/pdf?id=kMuQBgPIdg",
    "https://openreview.net/pdf?id=xuY33XhEGR"
    
]

papers = [
    "MEDAGENTGYM.pdf",
    "WEBDEVJUDGE.pdf",
    "LATENT_SPEECH_TEXT_TRANSFORMER.pdf",
    "GENERATIVE_AUTO_BIDDING.pdf",
    "CLIMODE.pdf"
]
```
```python
from utils import get_doc_tools
from pathlib import Path

paper_to_tools_dict = {}
for paper in papers:
    print(f"Getting tools for paper: {paper}")
    vector_tool, summary_tool = get_doc_tools(paper, Path(paper).stem)
    paper_to_tools_dict[paper] = [vector_tool, summary_tool]
```
```python
initial_tools = [t for paper in papers for t in paper_to_tools_dict[paper]]
```
```python
from llama_index.llms.openai import OpenAI

llm = OpenAI(model="gpt-3.5-turbo")
```
```python
len(initial_tools)
```
```python
from llama_index.core.agent import FunctionCallingAgentWorker
from llama_index.core.agent import AgentRunner

agent_worker = FunctionCallingAgentWorker.from_tools(
    initial_tools, 
    llm=llm, 
    verbose=True
)
agent = AgentRunner(agent_worker)
```
```python
response = agent.query(
    "What is MedAgentGym?"
    "What is auto-bidding in online advertising?"
    "What problem does ClimODE solve?"
    "Why are speech-text models computationally expensive?"
    "Why was WEBDEVJUDGE introduced?"
    
)
```
```python
response = agent.query("Give me a summary of all the 5 documents")
print(str(response))
```

### OUTPUT:

<img width="1365" height="893" alt="image" src="https://github.com/user-attachments/assets/2c7d0929-0248-4ab2-9a0f-b1ee2b6fe32a" />

<img width="1234" height="869" alt="image" src="https://github.com/user-attachments/assets/f6e7c11d-3a72-43df-a0ed-dc15bc722bf9" />

<img width="1283" height="416" alt="image" src="https://github.com/user-attachments/assets/122b1e55-25c5-405d-817b-eedb20e9bf83" />
<img width="1312" height="76" alt="image" src="https://github.com/user-attachments/assets/6ff5acda-6e5c-4cce-ac6f-950cff10bd29" />

### RESULT:

Thus, a multidocument retrieval agent using LlamaIndex to extract and synthesize information from multiple research articles is designed and implemented successfully.
