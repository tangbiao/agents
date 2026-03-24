# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is an educational notebook repository covering AI agent development, aligned with the Hugging Face Agents Course. It contains Jupyter notebooks and a Python script demonstrating various agentic frameworks and patterns.

## Running Notebooks

Notebooks use `%pip install` cells to install their own dependencies — run those cells first before executing other cells.

To launch Jupyter:
```bash
jupyter notebook
# or
jupyter lab
```

To run a specific notebook non-interactively:
```bash
jupyter nbconvert --to notebook --execute <notebook>.ipynb
```

## Running the Vision Web Browser Script

```bash
python vision_web_browser.py --model-type <type>
```

## CI

The CI workflow (`.github/workflows/main.yml`) is currently a placeholder and runs no real tests.

## Architecture

### Notebook Themes

| Notebook | Framework | Focus |
|---|---|---|
| `tool_calling_agents.ipynb` | smolagents | CodeAgent vs ToolCallingAgent, MCP |
| `code_agents.ipynb` | smolagents | Code-executing agents, custom tools, Hub sharing |
| `multi-agents.ipynb` | smolagents | Manager/sub-agent hierarchy, multi-modal QA |
| `retrieval-agents.ipynb` | smolagents | Agentic RAG, BM25 knowledge base |
| `vision_agents.ipynb` | smolagents | Image input, visual identity verification |
| `langgraph_agent.ipynb` | LangGraph | StateGraph, tool binding, vision |
| `mail_sorting.ipynb` | LangGraph | Email routing, Langfuse tracing |
| `function-call-ft.ipynb` | HF/trl | Fine-tuning Gemma-2 with LoRA for function calling |
| `work_with_huggingface.ipynb` | HF Hub | Inference clients, tokenizers, smolagents backends |

### Key Frameworks

- **smolagents**: `CodeAgent` executes Python code; `ToolCallingAgent` makes structured tool calls. Tools defined via `@tool` decorator or by subclassing `Tool`. Supports pluggable model backends: `HfApiModel`, `OpenAIServerModel`, `TransformersModel`.
- **LangGraph**: State machines using `TypedDict` state, `StateGraph`, nodes/edges, conditional routing, and `bind_tools()`.
- **trl / PEFT**: Fine-tuning with `SFTTrainer` + LoRA adapters. The fine-tuned model (`biaotang/gemma-2-2B-it-thinking-function_calling-V0`) adds `<think>`, `<tool_call>`, `<tool_response>` special tokens.

### Model Backends Used

Notebooks demonstrate interchangeable backends: OpenAI-compatible endpoints (including Gemini and Vertex AI's OpenAI-compat APIs), Hugging Face Inference API, local llama.cpp (port 8080), and Ollama (`gemma3`).

### Sensitive Files

`.env` and `gemini.md` are git-ignored — API keys and credentials live there.
