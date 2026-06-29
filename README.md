<div align="center">

# 🦜🔗 LangGraph — Agentic AI from Scratch

### A Hands-On Learning Repository for Building Stateful, Multi-Step AI Agents

[![Python](https://img.shields.io/badge/Python-3.12+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![LangGraph](https://img.shields.io/badge/LangGraph-1.2+-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)](https://langchain-ai.github.io/langgraph/)
[![LangChain](https://img.shields.io/badge/LangChain-1.3+-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)](https://www.langchain.com/)
[![Groq](https://img.shields.io/badge/Groq-Llama_3.3_70B-F55036?style=for-the-badge&logo=groq&logoColor=white)](https://groq.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

<br/>

> **Learn by building.** This repository walks you through the core concepts of LangGraph — the agent orchestration framework by LangChain — through progressive, well-documented Jupyter notebooks. Each section builds on the last, taking you from a bare-bones chatbot to a fully agentic, memory-enabled, streaming-capable AI system.

<br/>

[Getting Started](#-getting-started) · [What You'll Learn](#-what-youll-learn) · [Project Structure](#-project-structure) · [Tech Stack](#%EF%B8%8F-tech-stack) · [Contributing](#-contributing)

</div>

---

## 📚 What You'll Learn

This repository is structured as a **progressive tutorial**. Each section introduces a new LangGraph concept, complete with runnable code, inline explanations, and real output from the Groq-powered LLM.

| # | Topic | Key Concepts | Notebook |
|:-:|-------|--------------|:--------:|
| 1 | **Basic ChatBot** | `StateGraph`, `START`/`END` nodes, `add_messages` reducer, graph compilation | [📓](1-BasicChatBot/1-basicchatbot.ipynb) |
| 2 | **ChatBot with Tools** | Tavily web search, custom Python tools, `bind_tools()`, `ToolNode`, `tools_condition` | [📓](1-BasicChatBot/1-basicchatbot.ipynb) |
| 3 | **ReAct Agent** | Reason + Act loop, multi-tool orchestration in a single prompt, `create_react_agent` | [📓](1-BasicChatBot/1-basicchatbot.ipynb) |
| 4 | **Memory & Persistence** | `MemorySaver` checkpointer, `thread_id` config, cross-turn conversation recall | [📓](1-BasicChatBot/1-basicchatbot.ipynb) |
| 5 | **Streaming** | `stream()` with `updates`/`values` modes, `astream_events()` for async token-level streaming | [📓](1-BasicChatBot/1-basicchatbot.ipynb) |

---

## 🏗️ Architecture Overview

The following diagram illustrates the progression of graph architectures built in this repository:

```
┌──────────────────────────────────────────────────────────────────────┐
│                                                                      │
│   1. BASIC CHATBOT          2. TOOL-CALLING           3. ReAct AGENT │
│                                                                      │
│   ┌───────┐                 ┌───────┐                 ┌───────┐      │
│   │ START │                 │ START │                 │ START │      │
│   └───┬───┘                 └───┬───┘                 └───┬───┘      │
│       │                         │                         │          │
│       ▼                         ▼                         ▼          │
│   ┌────────┐               ┌─────────┐               ┌─────────┐    │
│   │Chatbot │               │ LLM +   │◄──────────┐   │ ReAct   │    │
│   │  Node  │               │ Tools   │           │   │  Agent  │◄─┐ │
│   └───┬────┘               └────┬────┘           │   └────┬────┘  │ │
│       │                      ┌──┴──┐             │     ┌──┴──┐    │ │
│       ▼                      │Route│             │     │Route│    │ │
│   ┌───────┐                  └┬───┬┘             │     └┬───┬┘    │ │
│   │  END  │                   │   │              │      │   │     │ │
│   └───────┘              ┌────┘   └────┐    ┌────┘ ┌───┘   └───┐ │ │
│                          ▼             ▼    │      ▼           ▼ │ │
│                      ┌───────┐   ┌────────┐ │  ┌────────┐  ┌───────┐│
│                      │  END  │   │  Tool  │─┘  │  Tool  │──│  END  ││
│                      └───────┘   │  Node  │    │  Node  │  └───────┘│
│                                  └────────┘    └────────┘           │
│                                                                      │
│   4. + MEMORY (MemorySaver)    5. + STREAMING (stream / astream)    │
│      Adds persistence via         Token-by-token output with        │
│      thread-based checkpoints     updates, values & events modes    │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

---

## ⚡ Getting Started

### Prerequisites

- **Python 3.12+**
- **[uv](https://docs.astral.sh/uv/)** (recommended) or `pip`
- API keys for **[Groq](https://console.groq.com/)** and **[Tavily](https://tavily.com/)**

### 1. Clone the Repository

```bash
git clone https://github.com/BharadwajNB/langgraph.git
cd langgraph
```

### 2. Set Up Environment

**Using uv (recommended):**
```bash
uv venv
uv sync
```

**Using pip:**
```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate

pip install -r requirements.txt
```

### 3. Configure API Keys

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key_here
TAVILY_API_KEY=your_tavily_api_key_here
```

> **🔑 Where to get your keys:**
>
> | Service | Sign Up | Free Tier |
> |---------|---------|-----------|
> | Groq | [console.groq.com](https://console.groq.com/) | ✅ Generous free tier |
> | Tavily | [tavily.com](https://tavily.com/) | ✅ 1,000 free searches/month |

### 4. Launch the Notebooks

```bash
jupyter notebook
```

Navigate to `1-BasicChatBot/1-basicchatbot.ipynb` and run the cells sequentially.

---

## 🗂️ Project Structure

```
langgraph/
├── 1-BasicChatBot/
│   └── 1-basicchatbot.ipynb   # 📓 Progressive tutorial notebook
│                                #    ├── Basic ChatBot (Graph API)
│                                #    ├── ChatBot with Tools (Tavily + Custom)
│                                #    ├── ReAct Agent (Multi-tool reasoning)
│                                #    ├── Memory & Persistence (MemorySaver)
│                                #    └── Streaming (sync + async)
├── main.py                     # Entry point scaffold
├── pyproject.toml              # Project metadata & dependencies
├── requirements.txt            # Pip-compatible dependency list
├── .env                        # API keys (⚠️ do NOT commit)
├── .gitignore                  # Ignores .env, __pycache__, .venv
└── README.md                   # You are here
```

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Orchestration** | [LangGraph](https://langchain-ai.github.io/langgraph/) `>=1.2.6` | Graph-based agent workflows with state management |
| **Framework** | [LangChain](https://www.langchain.com/) `>=1.3.11` | LLM abstraction, tool binding, prompt management |
| **LLM Provider** | [Groq](https://groq.com/) — Llama 3.3 70B Versatile | Ultra-fast inference via LPU™ hardware |
| **Web Search** | [Tavily](https://tavily.com/) | Real-time internet search optimized for AI agents |
| **Observability** | [LangSmith](https://smith.langchain.com/) `>=0.9.0` | Tracing, debugging, and evaluation |
| **Language** | Python 3.12+ | Type hints, `Annotated` types, async support |
| **Package Manager** | [uv](https://docs.astral.sh/uv/) | Fast, reliable Python package management |

---

## 🧠 Core Concepts Covered

### 1. State Management with `TypedDict` + Reducers

```python
from typing import Annotated
from langgraph.graph.message import add_messages

class State(TypedDict):
    messages: Annotated[list, add_messages]  # Append-only message history
```

The `add_messages` reducer ensures messages accumulate across graph steps instead of being overwritten — the foundation of conversational memory.

### 2. Graph Construction (Nodes + Edges)

```python
graph_builder = StateGraph(State)
graph_builder.add_node("chatbot", chatbot_fn)
graph_builder.add_edge(START, "chatbot")
graph_builder.add_edge("chatbot", END)
graph = graph_builder.compile()
```

### 3. Tool Integration (Tavily Search + Custom Functions)

```python
from langchain_tavily import TavilySearch

tool = TavilySearch(max_result=2)

def multiply(a: int, b: int) -> int:
    """Multiply a and b."""
    return a * b

llm_with_tools = llm.bind_tools([tool, multiply])
```

### 4. ReAct Agent Pattern

The **Reason + Act** loop enables the agent to:
- 🤔 **Reason** about which tool to call
- 🛠️ **Act** by executing the selected tool
- 👀 **Observe** the tool's output
- 🔁 **Repeat** until the task is complete

```python
# Handle multiple tools in a single prompt:
response = graph.invoke({
    "messages": "What is the latest news in AI and 45 multiplied by 109?"
})
```

### 5. Persistent Memory with Checkpointers

```python
from langgraph.checkpoint.memory import MemorySaver

memory = MemorySaver()
graph = graph_builder.compile(checkpointer=memory)

# Each thread maintains its own conversation history
config = {"configurable": {"thread_id": "1"}}
graph.invoke({"messages": "My name is Bharadwaj"}, config)
graph.invoke({"messages": "What is my name?"}, config)  # ✅ Remembers!
```

### 6. Streaming Responses

```python
# Synchronous streaming (updates mode)
for chunk in graph.stream(input, config, stream_mode="updates"):
    print(chunk)

# Async token-level streaming
async for event in graph.astream_events(input, config, version="v2"):
    if event["event"] == "on_chat_model_stream":
        print(event["data"]["chunk"].content, end="")
```

---

## 🗺️ Roadmap

- [ ] **Human-in-the-Loop** — Add interrupt nodes for user approval workflows
- [ ] **Multi-Agent Systems** — Supervisor + worker agent architectures
- [ ] **Custom State Channels** — Advanced state management patterns
- [ ] **LangGraph Cloud Deployment** — Production deployment walkthrough
- [ ] **RAG Agent** — Retrieval-augmented generation with vector stores
- [ ] **Evaluation & Testing** — Automated agent evaluation with LangSmith

---

## 🤝 Contributing

Contributions are welcome! Whether it's fixing a typo, adding a new notebook, or improving explanations:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/new-tutorial`)
3. **Commit** your changes (`git commit -m 'feat: add human-in-the-loop tutorial'`)
4. **Push** to the branch (`git push origin feature/new-tutorial`)
5. **Open** a Pull Request

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 🙏 Acknowledgements

- [LangChain](https://www.langchain.com/) — for building the LangGraph framework
- [Groq](https://groq.com/) — for blazing-fast LLM inference
- [Tavily](https://tavily.com/) — for AI-optimized web search
- [LangChain Academy](https://academy.langchain.com/) — for educational inspiration

---

<div align="center">

**⭐ If this repository helped you learn something new, consider giving it a star!**

Built with ❤️ by [Bharadwaj](https://github.com/BharadwajNB)

</div>
