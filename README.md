# PHI Detector: An Agentic Flow for PHI Detection Using LangGraph

**PHI Detector** is an agentic, multi-step workflow for detecting and assessing Personal Health Information (PHI) in documents, images and spreadsheets. It is built on top of **LangGraph**, leveraging the orchestration and state management capabilities of LangGraph to implement a modular, extensible agent system, with **LangChain** providing LLM integration and tool support.

## Project Overview

This project exemplifies a **graph-based agentic flow** for document analysis:

- **Agentic Workflow**: Each stage of the PHI detection process is encapsulated as a node (agent) in a directed graph, allowing for flexible, conditional, and multi-format processing.
- **LangGraph Orchestration**: The workflow is orchestrated using LangGraph, to define states, nodes, edges, handling routing, branching, and state persistence throughout the process.
- **LangChain Integration**: Nodes that require LLM reasoning (e.g., PHI identification and risk assessment) utilize LangChain’s LLM wrappers and prompt management for structured outputs.
- **Multi-Format Support**: The flow can process PNG (OCR), PDF (text extraction), and CSV (tabular parsing) files, routing each input dynamically to the appropriate parser node.
- **Exclude PHI Types with Plugins**: Pass a plugin of the PHI types that need to be excluded depending on the communication involved
- **Custom Input**: Add your custom files to the project directory and pass the path as input to check PHI on your own document! 

---

## Agentic Flow Architecture

The PHI Detector is structured as a **stateful agentic graph**:

![graph](https://github.com/user-attachments/assets/2245fca3-8d4d-4fd3-80a3-0dfd7f01d9ca)


| Node (Agent)        | Role                                                                 |
|---------------------|----------------------------------------------------------------------|
| Input Router        | Directs the file to the correct parser node based on file extension  |
| OCR Parser          | Extracts text from images using Tesseract OCR                        |
| PDF Parser          | Extracts text from PDF documents                                     |
| CSV Parser          | Parses and flattens CSV files into text                              |
| PHI Identifier      | LLM agent (via LangChain) that detects PHI entities                 |
| PHI Rationale       | LLM agent (via LangChain) that classifies PHI type and explains risk|


---
## How to run?

### Requirements

- Python 3.8+
- OpenAI API key (for LLM calls)
- LangSmith API key (for tracing/debugging)
- Tesseract OCR (for image processing)

### Installation
    pip install -r requirements.txt

### Running the graph
Simply run all cells


### Supported File Types

- `.png` (image, OCR)
- `.pdf` (PDF text extraction)
- `.csv` (tabular data parsing)

---

## Output

The workflow returns a structured list of PHI instances, each including:
- `type`: PHI category (e.g., Name, Date)
- `value`: The detected value
- `start`, `end`: Character positions in the text
- `PHI type`: Standardized PHI type
- `PHI risk rationale`: LLM-generated rationale for PHI risk
