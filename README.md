# Agentic AI Learning Plan — Master Summary
**Created:** May 2026 | **For:** Gaurav Verma | **Goal:** Fundamentals → Advanced Agentic AI → Saleable Products

---

## Table of Contents
1. [Your Profile & Schedule](#your-profile--schedule)
2. [What Was Built — All Files](#what-was-built--all-files)
3. [The 3-Month Plan Overview](#the-3-month-plan-overview)
4. [Week 0 — Environment Setup](#week-0--environment-setup)
5. [Month 1 — Foundations (Weeks 1–4)](#month-1--foundations-weeks-14)
6. [Month 2 — Builder (Weeks 5–8)](#month-2--builder-weeks-58)
7. [Month 3 — Creator (Weeks 9–12)](#month-3--creator-weeks-912)
8. [All Resources Master Index](#all-resources-master-index)
9. [API Costs & Budget](#api-costs--budget)
10. [All Ready-to-Paste Claude Prompts](#all-ready-to-paste-claude-prompts)
11. [Key Code Snippets](#key-code-snippets)
12. [Milestone Tracker](#milestone-tracker)

---

## Your Profile & Schedule

| Field | Detail |
|-------|--------|
| **Study window (weekdays)** | 9–11 AM (2 hrs/day) |
| **Study window (weekends)** | 5 hrs/day (around kids) |
| **Total weekly hours** | ~15 hrs/week |
| **Total over 3 months** | ~180 hrs |
| **Python level** | Intermediate — API calls with requests + json, slight notebooks experience |
| **Tools** | VS Code, Mac Mini, local development |
| **Budget** | $50/month comfortable |
| **Product goal** | SaaS tools sold to strangers + personal productivity tools |

---

## What Was Built — All Files

All files are saved in your project workspace: `~/Documents/Claude/Projects/AI and agentic AI/`

| File | Description |
|------|-------------|
| `Agentic_AI_3Month_Plan.pptx` | 10-slide PowerPoint roadmap — week-by-week overview, timeline, products to ship |
| `Agentic_AI_Study_Plan.docx` | Full 12-week study guide with resource links, coached weekend projects, Claude prompts |
| `Agentic_AI_Cost_Guide.docx` | Complete cost breakdown — every tool, API, subscription; free vs paid; monthly spend |
| `Agentic_AI_Week0_Setup.docx` | Step-by-step environment setup guide for your Mac Mini before Week 1 starts |
| `Weekly Guides/Week01_Guide.docx` | Week 1 prep guide — pre-reading, packages, daily plan, project steps, prompts |
| `Weekly Guides/Week02_Guide.docx` | Week 2 prep guide |
| `Weekly Guides/Week03_Guide.docx` | Week 3 prep guide |
| `Weekly Guides/Week04_Guide.docx` | Week 4 prep guide — Month 1 capstone |
| `Weekly Guides/Week05_Guide.docx` | Week 5 prep guide |
| `Weekly Guides/Week06_Guide.docx` | Week 6 prep guide |
| `Weekly Guides/Week07_Guide.docx` | Week 7 prep guide |
| `Weekly Guides/Week08_Guide.docx` | Week 8 prep guide — Month 2 capstone |
| `Weekly Guides/Week09_Guide.docx` | Week 9 prep guide |
| `Weekly Guides/Week10_Guide.docx` | Week 10 prep guide |
| `Weekly Guides/Week11_Guide.docx` | Week 11 prep guide |
| `Weekly Guides/Week12_Guide.docx` | Week 12 prep guide — Launch week |

---

## The 3-Month Plan Overview

```
Month 1 — FOUNDATIONS  (Weeks 1–4)
  Week 1: AI & LLM Foundations
  Week 2: Prompt Engineering Mastery
  Week 3: Python for AI + Tool Use
  Week 4: SHIP — Smart Summariser v1

Month 2 — BUILDER  (Weeks 5–8)
  Week 5: Agentic AI Architecture (ReAct)
  Week 6: Tools, Memory & Context
  Week 7: Claude SDK Deep Dive + MCP
  Week 8: SHIP — Research Agent v1

Month 3 — CREATOR  (Weeks 9–12)
  Week 9:  Multi-Agent Systems (LangGraph)
  Week 10: Production Engineering
  Week 11: Product Design & Packaging
  Week 12: LAUNCH — Your AI Product
```

---

## Week 0 — Environment Setup

Complete before Day 1. Estimated time: 2–3 hours.

### Folder structure
```bash
mkdir -p ~/agentic-ai/week01
mkdir -p ~/agentic-ai/week02
mkdir -p ~/agentic-ai/projects/smart-summariser
mkdir -p ~/agentic-ai/projects/research-agent
mkdir -p ~/agentic-ai/projects/multi-agent
cd ~/agentic-ai
```

### Virtual environment
```bash
cd ~/agentic-ai
python3 -m venv .venv
source .venv/bin/activate          # run this every session
pip install --upgrade pip
```

### VS Code extensions to install
- Python (Microsoft)
- Pylance (Microsoft)
- DotENV

### API accounts to create

| Service | URL | Purpose | Cost |
|---------|-----|---------|------|
| Anthropic (Claude) | https://console.anthropic.com | Primary LLM for all projects | Pay-as-you-go |
| DeepSeek | https://platform.deepseek.com | Cheap bulk tasks (~10x cheaper than Claude) | Pay-as-you-go |
| OpenAI | https://platform.openai.com | Follow any tutorial without code changes | Free $5 credits |
| Serper.dev | https://serper.dev | Web search API for agents | Free 2,500/month |
| LangSmith | https://smith.langchain.com | Agent tracing + debugging | Free tier |

> **Important:** Set a $20/month spend limit on Anthropic BEFORE using the API.  
> Go to: console.anthropic.com/settings/limits → Hard Limit → $20

### .env file setup
```bash
# ~/agentic-ai/.env
ANTHROPIC_API_KEY=your_anthropic_key_here
DEEPSEEK_API_KEY=your_deepseek_key_here
OPENAI_API_KEY=your_openai_key_here
SERPER_API_KEY=your_serper_key_here
LANGCHAIN_API_KEY=your_langsmith_key_here
LANGCHAIN_TRACING_V2=true
```

### .gitignore (CRITICAL — prevents key leaks)
```bash
# ~/agentic-ai/.gitignore
.env
.venv/
__pycache__/
*.pyc
.DS_Store
```

### Hello World test — verify all APIs work
```python
# ~/agentic-ai/week01/test_apis.py
import os
from dotenv import load_dotenv
load_dotenv(dotenv_path=os.path.expanduser('~/agentic-ai/.env'))

# Test Anthropic Claude
import anthropic
client = anthropic.Anthropic(api_key=os.getenv('ANTHROPIC_API_KEY'))
msg = client.messages.create(
    model='claude-haiku-4-5-20251001',
    max_tokens=50,
    messages=[{'role': 'user', 'content': 'Say hello in 5 words.'}]
)
print('Claude:', msg.content[0].text)

# Test DeepSeek
from openai import OpenAI
ds_client = OpenAI(
    api_key=os.getenv('DEEPSEEK_API_KEY'),
    base_url='https://api.deepseek.com'
)
resp = ds_client.chat.completions.create(
    model='deepseek-chat',
    messages=[{'role': 'user', 'content': 'Say hello in 5 words.'}],
    max_tokens=50
)
print('DeepSeek:', resp.choices[0].message.content)

print('All tests passed!')
```

### Week 0 checklist
- [ ] Python 3.10+ installed and verified
- [ ] VS Code with Python + Pylance + DotENV extensions
- [ ] Project folder structure created (`~/agentic-ai/...`)
- [ ] Virtual environment created and activated
- [ ] Anthropic account created at console.anthropic.com
- [ ] Anthropic billing enabled with **$20 spend limit set**
- [ ] Anthropic API key saved to `.env`
- [ ] DeepSeek account + credits ($5 min) + key saved to `.env`
- [ ] OpenAI account + key saved to `.env`
- [ ] Serper.dev account + key saved to `.env`
- [ ] `.gitignore` created (includes `.env` and `.venv/`)
- [ ] `test_apis.py` ran successfully — all APIs responded
- [ ] Week 1 packages installed
- [ ] Git configured + GitHub repo created (private)

---

## Month 1 — Foundations (Weeks 1–4)

### Week 1 — AI & LLM Foundations

**Theme:** Before touching code, understand what you are actually working with. LLMs are prediction machines.

**Install:**
```bash
source ~/agentic-ai/.venv/bin/activate
pip install anthropic python-dotenv requests streamlit
```

**Daily Plan:**
| Day | Task |
|-----|------|
| Mon | Watch 3Blue1Brown neural network videos 1+2. Notes on: weights, layers, activation. Research: tokens, context window, temperature, embeddings. |
| Tue | Read Anthropic Intro + Models Overview. Compare Claude.ai vs GPT-4o vs Gemini on the same prompt. |
| Wed | Follow Anthropic quickstart exactly. Make your first API call. Print the raw response object. |
| Thu | Write `classify_text()` function. Try Haiku, Sonnet, Opus. Print token counts. |
| Fri | Set up GitHub repo `agentic-ai-projects`. Push week1/ folder. Write README. |

**Key resources:**
- [3Blue1Brown Neural Networks](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi) — Videos 1, 2, 3
- [Anthropic: Intro to Claude](https://docs.anthropic.com/en/docs/intro-to-claude) — What is Claude + Key capabilities
- [Anthropic: Models Overview](https://docs.anthropic.com/en/docs/about-claude/models/overview) — Haiku vs Sonnet vs Opus
- [Anthropic: Quickstart](https://docs.anthropic.com/en/docs/quickstart) — First API call in Python
- [Anthropic Python SDK](https://github.com/anthropics/anthropic-sdk-python#readme) — Installation + basic usage
- [Stephen Wolfram: What is ChatGPT?](https://writings.stephenwolfram.com/2023/02/what-is-chatgpt-doing-and-why-does-it-work/) — Sections 1–4

**Weekend Project 1: Text Classifier App**  
Build a Streamlit web app that classifies text into 5 categories using the Claude API.
```python
# Core function pattern
import anthropic
import os
from dotenv import load_dotenv

load_dotenv()
client = anthropic.Anthropic(api_key=os.getenv('ANTHROPIC_API_KEY'))

def classify_text(text: str) -> str:
    msg = client.messages.create(
        model='claude-haiku-4-5-20251001',
        max_tokens=50,
        system="Classify the following text into exactly one category: Technology, Health & Wellness, Finance, Sports, or Entertainment. Return ONLY the category name.",
        messages=[{'role': 'user', 'content': text}]
    )
    return msg.content[0].text.strip()
```
Deploy free at: https://share.streamlit.io

**Deliverable:** Text classifier live at a public Streamlit URL. Screenshot saved.

---

### Week 2 — Prompt Engineering Mastery

**Theme:** Prompting is the highest-leverage skill in AI. A better prompt costs nothing and can 10x output quality.

**Install:** No new packages — Week 1 covers everything.

**Daily Plan:**
| Day | Task |
|-----|------|
| Mon | Read Anthropic Prompt Engineering guide — all sections. |
| Tue | Chain-of-thought: write zero-shot vs CoT for 3 tasks. Measure quality difference. |
| Wed | Build a `PromptLibrary` class — 5 reusable templates as Python strings. |
| Thu | System prompt testing: same message, 5 different system prompts. Document changes. |
| Fri | Prompt chaining: extract → analyse → summarise (3-step chain). |

**Key resources:**
- [Anthropic: Prompt Engineering Overview](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview) — **Read ALL sections**
- [Anthropic: Chain of Thought](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/chain-of-thought)
- [Anthropic: Use XML Tags](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/use-xml-tags)
- [Anthropic: Give Claude a Role](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/give-claude-a-role)
- [Anthropic Prompt Library](https://docs.anthropic.com/en/resources/prompt-library/library) — 20+ real examples
- [DeepLearning.AI: Prompt Engineering for Developers (free)](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/) — Lessons 2, 3, 4
- [LearnPrompting: Basics](https://learnprompting.org/docs/basics/introduction) — Basics + Intermediate

**6 Techniques to Master:**
1. Zero-shot vs Few-shot
2. Chain-of-thought
3. Role prompting
4. XML structure
5. System vs user prompt
6. Output formatting

**Weekend Project 2: Smart Email Summariser**  
Streamlit app with 3 summary styles (Executive Brief, Bullet Points, Action Items) using `st.tabs`.

**Deliverable:** Email Summariser live with 3 prompt styles + prompt comparison view.

---

### Week 3 — Python for AI + Tool Use

**Theme:** Give Claude the ability to take actions — call APIs, read files, use the web. This is the bridge from chatbot to agent.

**Install:**
```bash
pip install requests streamlit
# Also: sign up at serper.dev and add SERPER_API_KEY to .env
```

**Daily Plan:**
| Day | Task |
|-----|------|
| Mon | Python JSON mastery: parse API responses, extract nested values, handle missing keys. |
| Tue | Call the Serper API from Python — search → parse → format results. |
| Wed | Read Anthropic Tool Use docs. Define a tool schema. Parse `tool_use` response. |
| Thu | Build calculator tool: add/subtract/multiply/divide. Let Claude decide when to call it. |
| Fri | Connect web search + calculator as two tools. Observe Claude's routing decisions. |

**Key resources:**
- [Anthropic: Tool Use Overview](https://docs.anthropic.com/en/docs/build-with-claude/tool-use/overview) — Read completely
- [Anthropic: Implement Tool Use](https://docs.anthropic.com/en/docs/build-with-claude/tool-use/implement-tool-use)
- [Anthropic: Tool Use Best Practices](https://docs.anthropic.com/en/docs/build-with-claude/tool-use/best-practices-for-tool-definitions)
- [Anthropic Cookbook: Tool Use](https://github.com/anthropics/anthropic-cookbook/tree/main/tool_use) — Run `calculator_tool.ipynb`
- [Serper.dev API Reference](https://serper.dev/api-reference)
- [RealPython: Working with JSON](https://realpython.com/python-json/)

**Tool use pattern — core code:**
```python
# Define a tool
tools = [{
    "name": "search_web",
    "description": "Search the web for current information on any topic.",
    "input_schema": {
        "type": "object",
        "properties": {
            "query": {"type": "string", "description": "The search query"}
        },
        "required": ["query"]
    }
}]

# Call Claude with tools
response = client.messages.create(
    model='claude-haiku-4-5-20251001',
    max_tokens=1024,
    tools=tools,
    messages=[{'role': 'user', 'content': 'What is the latest news about AI?'}]
)

# Check if Claude wants to use a tool
if response.stop_reason == 'tool_use':
    for block in response.content:
        if block.type == 'tool_use':
            tool_name = block.name
            tool_input = block.input
            # ... call your actual function here
```

**Weekend Project 3: News Aggregator Agent**  
Agent that searches the web and produces a structured daily brief on any topic.

**Deliverable:** News Aggregator live — searches web, produces structured brief with sources.

---

### Week 4 — Ship: Smart Summariser v1 (Month 1 Capstone)

**Theme:** Polish, deploy, and launch your Month 1 product. Ship it.

**Install:**
```bash
pip install pymupdf requests streamlit python-dotenv
```

**Daily Plan:**
| Day | Task |
|-----|------|
| Mon | Build full Smart Summariser: accepts URL, PDF, and pasted text. |
| Tue | UI polish: sidebar, summary length slider, download button, usage counter. |
| Wed | Error handling: invalid URL, huge PDF, empty input, API timeout. |
| Thu | Deploy to Render.com — connect GitHub, set env vars, smoke test. |
| Fri | Share with 3 people. Collect feedback. Write Month 1 retrospective. |

**Key resources:**
- [PyMuPDF: Text Extraction Tutorial](https://pymupdf.readthedocs.io/en/latest/tutorial.html)
- [Python Requests Quickstart](https://requests.readthedocs.io/en/latest/user/quickstart/)
- [Streamlit Advanced Features](https://docs.streamlit.io/develop/api-reference/widgets)
- [Render.com: Deploy Streamlit](https://render.com/docs/deploy-streamlit)
- [python-dotenv Usage](https://pypi.org/project/python-dotenv/#usage)

**Input handler pattern:**
```python
import fitz  # PyMuPDF
import requests
from bs4 import BeautifulSoup

def extract_from_url(url: str) -> str:
    resp = requests.get(url, timeout=10)
    soup = BeautifulSoup(resp.text, 'html.parser')
    text = ' '.join(p.get_text() for p in soup.find_all('p'))
    return text[:12000]  # ~3000 words

def extract_from_pdf(file_bytes: bytes) -> str:
    doc = fitz.open(stream=file_bytes, filetype='pdf')
    text = ''.join(page.get_text() for page in doc)
    return text[:12000]
```

**Deliverable:** Smart Summariser at a public URL. Shown to 3+ people. LinkedIn post published. **MONTH 1 COMPLETE.**

---

## Month 2 — Builder (Weeks 5–8)

### Week 5 — Agentic AI Architecture

**Theme:** Understand the ReAct loop — Reason, Act, Observe, Repeat.

**Install:**
```bash
pip install langchain langchain-anthropic langchain-community langsmith langgraph
```

**Daily Plan:**
| Day | Task |
|-----|------|
| Mon | Read ReAct paper (abstract + sections 1–3). Draw Thought→Action→Observation loop on paper. |
| Tue | Install LangChain. Run the quickstart. Understand chains, runnables, LCEL pipe syntax (`|`). |
| Wed | Run a LangChain agent with 2 tools. Use LangSmith to trace it. |
| Thu | Compare LangChain agent vs raw Claude Tool Use — same task, both approaches. |
| Fri | Read supervisor/worker pattern. Sketch a 3-agent research system on paper. |

**Key resources:**
- [ReAct Paper (original)](https://arxiv.org/abs/2210.03629) — Abstract + sections 1, 2, 3
- [LangChain: Agents Concept](https://python.langchain.com/docs/concepts/agents/)
- [LangChain: Build an Agent Tutorial](https://python.langchain.com/docs/tutorials/agents/)
- [LangSmith: Tracing Quickstart](https://docs.smith.langchain.com/how_to_guides/tracing/trace_with_langchain)
- [Anthropic: Orchestrating Agents](https://docs.anthropic.com/en/docs/build-with-claude/tool-use/orchestrating-agents)
- [AI Jason: ReAct Agent from Scratch (YouTube)](https://www.youtube.com/watch?v=Nq9wMjEcLGo)

**ReAct loop — pure Python implementation (no LangChain):**
```python
def run_react_agent(user_question: str, tools: list, max_iterations: int = 10) -> str:
    messages = [{'role': 'user', 'content': user_question}]
    
    for i in range(max_iterations):
        response = client.messages.create(
            model='claude-sonnet-4-6',
            max_tokens=1024,
            tools=tools,
            messages=messages
        )
        
        # Add Claude's response to messages
        messages.append({'role': 'assistant', 'content': response.content})
        
        # If Claude is done, return the answer
        if response.stop_reason == 'end_turn':
            return response.content[0].text
        
        # Process tool calls
        tool_results = []
        for block in response.content:
            if block.type == 'tool_use':
                print(f"Step {i+1}: Calling tool '{block.name}' with args: {block.input}")
                result = call_tool(block.name, block.input)  # your dispatch function
                tool_results.append({
                    'type': 'tool_result',
                    'tool_use_id': block.id,
                    'content': str(result)
                })
        
        # Add tool results back into messages
        messages.append({'role': 'user', 'content': tool_results})
    
    return "Max iterations reached"
```

**Weekend Project 5: ReAct Agent from Scratch**  
Build the full ReAct loop using ONLY the Anthropic SDK — no LangChain. The most important project in the plan.

**Deliverable:** ReAct agent with 2 tools (search + calculator) working on 5 test questions. No frameworks.

---

### Week 6 — Tools, Memory & Context

**Theme:** An agent without memory is amnesiac. Give your agent a brain.

**Install:**
```bash
pip install chromadb
```

**Key resources:**
- [Pinecone: What Are Vector Embeddings](https://www.pinecone.io/learn/vector-embeddings/) — best explanation online
- [ChromaDB: Getting Started](https://docs.trychroma.com/docs/overview/getting-started)
- [ChromaDB: Querying Collections](https://docs.trychroma.com/docs/querying-collections/query-and-get)
- [LangChain: Memory Concept](https://python.langchain.com/docs/concepts/memory/)
- [LangChain + ChromaDB Integration](https://python.langchain.com/docs/integrations/vectorstores/chroma/)
- [DeepLearning.AI: Agentic RAG](https://www.deeplearning.ai/short-courses/building-agentic-rag-with-llamaindex/) — All 5 lessons

**Persistent memory pattern:**
```python
import chromadb
from datetime import datetime

# Create persistent client — data survives across Python sessions
chroma_client = chromadb.PersistentClient(path='./memory')
collection = chroma_client.get_or_create_collection('agent_memory')

def save_memory(question: str, facts: str, answer: str):
    collection.add(
        documents=[f"Q: {question}\nFacts: {facts}\nAnswer: {answer}"],
        metadatas=[{'timestamp': datetime.now().isoformat(), 'question': question}],
        ids=[f"mem_{datetime.now().timestamp()}"]
    )

def retrieve_memories(query: str, n: int = 3) -> str:
    results = collection.query(query_texts=[query], n_results=n)
    if not results['documents'][0]:
        return "No relevant memories found."
    return "\n\n".join(results['documents'][0])
```

**Weekend Project 6: Agent with Persistent Memory**  
Upgrade your Week 5 agent to remember what it researched across Python sessions.

**Deliverable:** Agent with persistent ChromaDB memory — remembers across Python sessions.

---

### Week 7 — Claude SDK Deep Dive + MCP

**Theme:** MCP (Model Context Protocol) is how Claude connects to the real world at scale.

**Install:**
```bash
pip install fastmcp
# MCP Inspector (requires Node.js):
# npx @modelcontextprotocol/inspector --version
```

**Key resources:**
- [MCP: Introduction & Architecture](https://modelcontextprotocol.io/introduction)
- [MCP: Build a Server (Python)](https://modelcontextprotocol.io/quickstart/server)
- [MCP: Connect to Claude Desktop](https://modelcontextprotocol.io/quickstart/user)
- [MCP Inspector](https://modelcontextprotocol.io/docs/tools/inspector)
- [FastMCP GitHub](https://github.com/jlowin/fastmcp) — simpler than the official SDK
- [Anthropic: Streaming Responses](https://docs.anthropic.com/en/docs/build-with-claude/streaming)
- [Anthropic: Prompt Caching](https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching) — 90% cost reduction

**Minimal MCP server (FastMCP):**
```python
# server.py
from fastmcp import FastMCP
import os, requests

mcp = FastMCP("My Tools Server")

@mcp.tool()
def search_web(query: str) -> str:
    """Search the web for current information on any topic.
    
    Args:
        query: The search query string
    
    Returns:
        A formatted string of search results with titles, URLs, and snippets
    """
    resp = requests.post(
        'https://google.serper.dev/search',
        headers={'X-API-KEY': os.getenv('SERPER_API_KEY')},
        json={'q': query, 'num': 5}
    )
    results = resp.json().get('organic', [])
    return '\n\n'.join(
        f"Title: {r['title']}\nURL: {r['link']}\nSnippet: {r['snippet']}"
        for r in results
    )

@mcp.tool()
def calculate(expression: str) -> str:
    """Safely evaluate a mathematical expression.
    
    Args:
        expression: A mathematical expression like '2 + 2' or '(100 * 1.5) / 3'
    """
    try:
        result = eval(expression, {"__builtins__": {}}, {})
        return str(result)
    except Exception as e:
        return f"Error: {e}"

if __name__ == '__main__':
    mcp.run()
```

**Run + test:**
```bash
# Test with MCP Inspector
npx @modelcontextprotocol/inspector python server.py

# Connect to Claude Desktop — add to claude_desktop_config.json:
{
  "mcpServers": {
    "my-tools": {
      "command": "python",
      "args": ["/absolute/path/to/server.py"],
      "env": {"SERPER_API_KEY": "your_key"}
    }
  }
}
```

**Weekend Project 7: Your First MCP Server**  
MCP server with 2 tools, tested with Inspector, connected to Claude.

**Deliverable:** MCP server running. Tested with Inspector. Connected to Claude Desktop/Cowork. README on GitHub.

---

### Week 8 — Ship: Research Agent v1 (Month 2 Capstone)

**Install:**
```bash
pip install beautifulsoup4 tenacity
```

**Key resources:**
- [BeautifulSoup: Quick Start](https://beautiful-soup-4.readthedocs.io/en/latest/#quick-start)
- [Streamlit: st.write_stream](https://docs.streamlit.io/develop/api-reference/write-magic/st.write_stream)
- [Railway: Deploy Python App](https://docs.railway.app/guides/python)
- [Tenacity: Retry Logic](https://tenacity.readthedocs.io/en/latest/)

**Retry decorator pattern:**
```python
from tenacity import retry, wait_exponential, stop_after_attempt
from anthropic import RateLimitError, APIConnectionError

@retry(
    wait=wait_exponential(multiplier=1, min=1, max=10),
    stop=stop_after_attempt(3),
    retry=retry_if_exception_type((RateLimitError, APIConnectionError))
)
def call_claude(messages, tools=None):
    return client.messages.create(
        model='claude-sonnet-4-6',
        max_tokens=2048,
        messages=messages,
        tools=tools or []
    )
```

**Streaming output in Streamlit:**
```python
import streamlit as st

with st.spinner("Researching..."):
    with client.messages.stream(
        model='claude-sonnet-4-6',
        max_tokens=2048,
        messages=messages
    ) as stream:
        st.write_stream(stream.text_stream)
```

**Deliverable:** Research Agent live — answers better than 30-minute Google search. Post published. **MONTH 2 COMPLETE.**

---

## Month 3 — Creator (Weeks 9–12)

### Week 9 — Multi-Agent Systems

**Theme:** One agent is a tool. Multiple specialised agents working together is a product.

**Install:**
```bash
# langgraph already installed Week 5 — verify:
pip show langgraph
pip install langchain-anthropic  # if needed
```

**Key resources:**
- [LangGraph: Why LangGraph](https://langchain-ai.github.io/langgraph/concepts/why_langgraph/)
- [LangGraph: Introduction Tutorial](https://langchain-ai.github.io/langgraph/tutorials/introduction/) — **Complete Parts 1–5**
- [LangGraph: Multi-Agent Networks](https://langchain-ai.github.io/langgraph/concepts/multi_agent/) — Supervisor + Hierarchical patterns
- [LangGraph: Human in the Loop](https://langchain-ai.github.io/langgraph/concepts/human_in_the_loop/)
- [Anthropic: Building Effective Agents](https://www.anthropic.com/research/building-effective-agents)
- [DeepLearning.AI: AI Agents in LangGraph](https://www.deeplearning.ai/short-courses/ai-agents-in-langgraph/) — All lessons
- [Sam Witteveen: LangGraph Tutorial (YouTube)](https://www.youtube.com/watch?v=sFbmEZBSKrQ)

**3-Agent LangGraph pipeline:**
```python
from typing import TypedDict, List
from langgraph.graph import StateGraph, END

class PipelineState(TypedDict):
    topic: str
    raw_research: List[dict]
    quality_score: int
    refined_facts: List[str]
    final_article: str
    iteration_count: int

def researcher_node(state: PipelineState) -> PipelineState:
    # Search 3 times with different queries
    results = []
    for query in generate_queries(state['topic']):
        results.extend(search_web(query))
    return {**state, 'raw_research': results, 'iteration_count': state.get('iteration_count', 0) + 1}

def analyst_node(state: PipelineState) -> PipelineState:
    # Score quality and refine facts
    score, facts = analyse_research(state['raw_research'])
    return {**state, 'quality_score': score, 'refined_facts': facts}

def writer_node(state: PipelineState) -> PipelineState:
    article = write_article(state['refined_facts'], state['topic'])
    return {**state, 'final_article': article}

def route_after_analysis(state: PipelineState) -> str:
    if state['quality_score'] < 6 and state['iteration_count'] < 3:
        return 'researcher'  # loop back
    return 'writer'

# Build the graph
graph = StateGraph(PipelineState)
graph.add_node('researcher', researcher_node)
graph.add_node('analyst', analyst_node)
graph.add_node('writer', writer_node)

graph.set_entry_point('researcher')
graph.add_edge('researcher', 'analyst')
graph.add_conditional_edges('analyst', route_after_analysis, {
    'researcher': 'researcher',
    'writer': 'writer'
})
graph.add_edge('writer', END)

pipeline = graph.compile()
result = pipeline.invoke({'topic': 'Your topic here', 'iteration_count': 0})
```

**Deliverable:** 3-agent LangGraph pipeline producing articles. Quality loop working. Tested on 5 topics.

---

### Week 10 — Production Engineering

**Install:**
```bash
pip install tenacity pytest pytest-mock
```

**Key resources:**
- [Anthropic: Prompt Caching](https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching)
- [Tenacity: Retry Decorator](https://tenacity.readthedocs.io/en/latest/#tenacity.retry)
- [LangSmith: Trace Your Agents](https://docs.smith.langchain.com/how_to_guides/tracing/trace_with_langchain)
- [Anthropic: Token Counting](https://docs.anthropic.com/en/docs/build-with-claude/token-counting)
- [pytest: Getting Started](https://docs.pytest.org/en/stable/getting-started.html)

**Prompt caching (90% cost reduction on repeated system prompts):**
```python
response = client.messages.create(
    model='claude-sonnet-4-6',
    max_tokens=1024,
    system=[{
        "type": "text",
        "text": "Your long system prompt here...",
        "cache_control": {"type": "ephemeral"}  # <-- this is all you need
    }],
    messages=messages
)
```

**Cost logging:**
```python
def log_cost(response, model='claude-sonnet-4-6'):
    # Sonnet pricing: $3/M input, $15/M output
    input_cost  = response.usage.input_tokens  / 1_000_000 * 3
    output_cost = response.usage.output_tokens / 1_000_000 * 15
    total = input_cost + output_cost
    print(f"Cost: ${total:.4f} | In: {response.usage.input_tokens} | Out: {response.usage.output_tokens}")
    assert total < 0.10, f"Run exceeded $0.10 budget: ${total:.4f}"
    return total
```

**Deliverable:** Production agent — retries on, caching on, LangSmith tracing, 5 tests passing, cost logged.

---

### Week 11 — Product Design & Packaging

**Install:**
```bash
pip install fastapi uvicorn stripe python-multipart
```

**Key resources:**
- [Stripe: Checkout Quickstart](https://docs.stripe.com/checkout/quickstart)
- [FastAPI: Getting Started](https://fastapi.tiangolo.com/tutorial/first-steps/)
- [FastAPI: API Key Security](https://fastapi.tiangolo.com/tutorial/security/http-basic-auth/)
- [Vercel: Deploy a Site](https://vercel.com/docs/frameworks/nextjs) — or use a template
- [Stripe Test Cards](https://docs.stripe.com/testing#cards) — use `4242 4242 4242 4242`
- [Beehiiv: Create a Publication](https://support.beehiiv.com/hc/en-us/articles/10141498937623)

**FastAPI endpoint + API key auth:**
```python
# api.py
from fastapi import FastAPI, HTTPException, Header
from pydantic import BaseModel
import os

app = FastAPI()

class ResearchRequest(BaseModel):
    question: str

@app.post("/research")
async def research(req: ResearchRequest, x_api_key: str = Header(None)):
    if x_api_key != os.getenv('API_SECRET_KEY'):
        raise HTTPException(status_code=403, detail="Invalid API key")
    answer, sources = run_research_agent(req.question)
    return {"answer": answer, "sources": sources}

@app.get("/checkout")
async def checkout():
    import stripe
    stripe.api_key = os.getenv('STRIPE_SECRET_KEY')
    session = stripe.checkout.Session.create(
        payment_method_types=['card'],
        line_items=[{'price': os.getenv('STRIPE_PRICE_ID'), 'quantity': 1}],
        mode='subscription',
        success_url='https://yourdomain.com/success',
        cancel_url='https://yourdomain.com/',
    )
    return {"checkout_url": session.url}
```

```bash
# Run locally
uvicorn api:app --reload
```

**Deliverable:** Landing page live. Stripe test checkout working. FastAPI deployed. Loom demo recorded.

---

### Week 12 — LAUNCH: Your AI Product

**Key resources:**
- [Product Hunt: Maker Handbook](https://www.producthunt.com/stories/how-to-launch-on-product-hunt)
- [There's An AI For That: Submit](https://theresanaiforthat.com/get-listed/)
- [Futurepedia: Submit Tool](https://www.futurepedia.io/submit-tool)
- [Google Search Console](https://search.google.com/search-console/about)
- [Indie Hackers: Post a Launch](https://www.indiehackers.com/post/launch)

**Launch day checklist:**
- [ ] Final QA — test every user flow as a first-time visitor
- [ ] Meta title (60 chars) + description (150 chars) on landing page
- [ ] Submit to theresanaiforthat.com
- [ ] Submit to futurepedia.io
- [ ] Submit to toolify.ai
- [ ] Product Hunt submitted (schedule for 12:01 AM PST)
- [ ] LinkedIn post published
- [ ] Posted in 3 AI Discord channels
- [ ] Indie Hackers launch post
- [ ] 3-month retrospective published

**Deliverable:** LIVE PRODUCT. Landing page. Pricing. Product Hunt submitted. LinkedIn post. **MONTH 3 COMPLETE.**

---

## All Resources Master Index

### Anthropic / Claude Official Docs
| Resource | URL | When to Use |
|----------|-----|-------------|
| Intro to Claude | https://docs.anthropic.com/en/docs/intro-to-claude | Week 1 |
| Models Overview | https://docs.anthropic.com/en/docs/about-claude/models/overview | Week 1 |
| Quickstart | https://docs.anthropic.com/en/docs/quickstart | Week 1 |
| Prompt Engineering Overview | https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview | Week 2 |
| Chain of Thought | https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/chain-of-thought | Week 2 |
| XML Tags in Prompts | https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/use-xml-tags | Week 2 |
| Give Claude a Role | https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/give-claude-a-role | Week 2 |
| Long Context Tips | https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/long-context-tips | Week 2 |
| Tool Use Overview | https://docs.anthropic.com/en/docs/build-with-claude/tool-use/overview | Week 3 |
| Implement Tool Use | https://docs.anthropic.com/en/docs/build-with-claude/tool-use/implement-tool-use | Week 3 |
| Tool Use Best Practices | https://docs.anthropic.com/en/docs/build-with-claude/tool-use/best-practices-for-tool-definitions | Week 3 |
| Orchestrating Agents | https://docs.anthropic.com/en/docs/build-with-claude/tool-use/orchestrating-agents | Week 5 |
| Streaming | https://docs.anthropic.com/en/docs/build-with-claude/streaming | Week 7 |
| Prompt Caching | https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching | Week 7 + 10 |
| Token Counting | https://docs.anthropic.com/en/docs/build-with-claude/token-counting | Week 10 |
| Rate Limits | https://docs.anthropic.com/en/docs/build-with-claude/rate-limits | Week 10 |
| Building Effective Agents | https://www.anthropic.com/research/building-effective-agents | Week 9 |
| Anthropic Cookbook | https://github.com/anthropics/anthropic-cookbook | All months |
| Prompt Library | https://docs.anthropic.com/en/resources/prompt-library/library | Week 2 |

### LangChain + LangGraph
| Resource | URL | When to Use |
|----------|-----|-------------|
| LangChain Quickstart | https://python.langchain.com/docs/tutorials/llm_chain/ | Week 5 |
| Agents Concept | https://python.langchain.com/docs/concepts/agents/ | Week 5 |
| Build an Agent Tutorial | https://python.langchain.com/docs/tutorials/agents/ | Week 5 |
| Memory Concept | https://python.langchain.com/docs/concepts/memory/ | Week 6 |
| ChromaDB Integration | https://python.langchain.com/docs/integrations/vectorstores/chroma/ | Week 6 |
| LangGraph Introduction | https://langchain-ai.github.io/langgraph/tutorials/introduction/ | Week 9 |
| Why LangGraph | https://langchain-ai.github.io/langgraph/concepts/why_langgraph/ | Week 9 |
| Multi-Agent Patterns | https://langchain-ai.github.io/langgraph/concepts/multi_agent/ | Week 9 |
| Human in the Loop | https://langchain-ai.github.io/langgraph/concepts/human_in_the_loop/ | Week 9 |
| LangSmith Tracing | https://docs.smith.langchain.com/how_to_guides/tracing/trace_with_langchain | Week 5 + 10 |

### MCP (Model Context Protocol)
| Resource | URL | When to Use |
|----------|-----|-------------|
| MCP Introduction | https://modelcontextprotocol.io/introduction | Week 7 |
| MCP Architecture | https://modelcontextprotocol.io/docs/concepts/architecture | Week 7 |
| Build a Server (Python) | https://modelcontextprotocol.io/quickstart/server | Week 7 |
| Connect to Claude Desktop | https://modelcontextprotocol.io/quickstart/user | Week 7 |
| MCP Inspector | https://modelcontextprotocol.io/docs/tools/inspector | Week 7 |
| FastMCP GitHub | https://github.com/jlowin/fastmcp | Week 7 |

### Vector Stores & Embeddings
| Resource | URL | When to Use |
|----------|-----|-------------|
| Pinecone: Vector Embeddings | https://www.pinecone.io/learn/vector-embeddings/ | Week 6 |
| ChromaDB Getting Started | https://docs.trychroma.com/docs/overview/getting-started | Week 6 |
| ChromaDB Querying | https://docs.trychroma.com/docs/querying-collections/query-and-get | Week 6 |

### Free Courses (Specific Modules)
| Course | URL | What to Watch |
|--------|-----|---------------|
| DeepLearning.AI: Prompt Engineering | https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/ | Lessons 2, 3, 4 |
| DeepLearning.AI: LangChain | https://www.deeplearning.ai/short-courses/langchain-for-llm-application-development/ | Lessons 3, 4, 5 |
| DeepLearning.AI: Agentic RAG | https://www.deeplearning.ai/short-courses/building-agentic-rag-with-llamaindex/ | All 5 lessons |
| DeepLearning.AI: AI Agents in LangGraph | https://www.deeplearning.ai/short-courses/ai-agents-in-langgraph/ | All lessons |
| fast.ai Lesson 1 | https://course.fast.ai/Lessons/lesson1.html | Week 1 background |
| LearnPrompting | https://learnprompting.org/docs/basics/introduction | Week 2 |

### YouTube (Specific Videos)
| Video | URL | When to Watch |
|-------|-----|---------------|
| 3Blue1Brown: Neural Networks | https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi | Week 1 — videos 1, 2, 3 |
| Andrej Karpathy: Let's Build GPT | https://www.youtube.com/watch?v=kCc8FmEb1nY | Week 1 — best LLM deep dive |
| AI Jason: ReAct Agent from Scratch | https://www.youtube.com/watch?v=Nq9wMjEcLGo | Before Weekend Project 5 |
| Sam Witteveen: LangGraph Tutorial | https://www.youtube.com/watch?v=sFbmEZBSKrQ | Before Weekend Project 9 |

### Tools, APIs & Deployment
| Tool | URL | Purpose |
|------|-----|---------|
| Anthropic Console | https://console.anthropic.com | API keys + usage monitoring |
| Serper.dev | https://serper.dev | Web search API — 2,500 free/month |
| Streamlit Docs | https://docs.streamlit.io/develop/api-reference | UI components |
| Streamlit Cloud | https://share.streamlit.io | Free deployment from GitHub |
| Render.com | https://render.com/docs/deploy-streamlit | Streamlit deployment |
| Railway.app | https://railway.app | FastAPI deployment — 500 free hours/month |
| Tenacity | https://tenacity.readthedocs.io | Retry decorator for all API calls |
| LangSmith | https://smith.langchain.com | Agent tracing + observability |
| Langfuse | https://langfuse.com/docs | Open-source LangSmith alternative |
| Stripe Checkout | https://docs.stripe.com/checkout/quickstart | Payment integration |
| FastAPI Tutorial | https://fastapi.tiangolo.com/tutorial/first-steps/ | API backend |
| PyMuPDF | https://pymupdf.readthedocs.io/en/latest/tutorial.html | PDF text extraction |
| BeautifulSoup | https://beautiful-soup-4.readthedocs.io/en/latest/#quick-start | HTML parsing |

### Community & Launch Platforms
| Platform | URL | Purpose |
|----------|-----|---------|
| Anthropic Discord | https://discord.gg/anthropic | Claude developer community |
| LangChain Discord | https://discord.gg/langchain | LangGraph help |
| Indie Hackers | https://www.indiehackers.com/group/artificial-intelligence | AI founders community |
| Product Hunt | https://www.producthunt.com | Launch platform |
| There's An AI For That | https://theresanaiforthat.com/get-listed/ | AI directory submission |
| Futurepedia | https://www.futurepedia.io/submit-tool | AI directory submission |
| AI News Newsletter | https://buttondown.com/ainews | Best weekly AI digest |
| Beehiiv | https://beehiiv.com | Email waitlist — free tier |

---

## API Costs & Budget

### Claude API Pricing (as of May 2026)
| Model | Input (per 1M tokens) | Output (per 1M tokens) | Best for |
|-------|-----------------------|------------------------|----------|
| Claude Haiku 4.5 | $0.80 | $4.00 | Learning, testing, cheap bulk tasks |
| Claude Sonnet 4.6 | $3.00 | $15.00 | Production projects |
| Claude Opus 4.6 | $15.00 | $75.00 | Complex reasoning only |

> **Prompt caching** reduces input costs by up to **90%** for repeated system prompts — always use it in production.

### DeepSeek Pricing
| Model | Input | Output | Best for |
|-------|-------|--------|---------|
| DeepSeek-V3 | ~$0.07/M | ~$1.10/M | Bulk tasks, experimentation |
| DeepSeek-R1 | ~$0.55/M | ~$2.19/M | Reasoning tasks |

### 3-Month Realistic Budget
| Month | Min | Realistic | Upper Bound | What you're doing |
|-------|-----|-----------|-------------|-------------------|
| Month 1 | $0 | $5 | $15 | Learning, small API calls |
| Month 2 | $5 | $15 | $25 | Agents, vector store |
| Month 3 | $15 | $30 | $45 | Production multi-agent |
| **Total** | **$17** | **$37** | **$70** | Full 3-month plan |

### Free tiers to use
- **Streamlit Cloud** — free app hosting
- **Serper.dev** — 2,500 free searches/month
- **Railway** — 500 free hours/month
- **LangSmith** — free tier for tracing
- **ChromaDB** — fully free (local)
- **GitHub** — free repo hosting
- **Render.com** — free tier for web services
- **Vercel** — free for static sites
- **Beehiiv** — free unlimited subscribers

---

## All Ready-to-Paste Claude Prompts

### Understanding Concepts

**Tokens (Week 1):**
```
I'm just starting to learn about LLMs. Can you explain what a 'token' is in plain English — not a technical definition, but a real analogy that helps me understand why Claude counts tokens instead of words. Then tell me: how many tokens is a typical sentence?
```

**Context Windows (Week 1):**
```
Explain context windows to me like I'm building my first app. What is the practical implication of a 200k token context window? Give me 3 real scenarios where you would hit the limit and what happens when you do.
```

**Chain-of-Thought (Week 2):**
```
Teach me chain-of-thought prompting by showing me a before/after example. Take this task: 'A user wants to buy a laptop under $800 for video editing. What should they buy?' Show me: (1) a zero-shot prompt that gets a mediocre answer, (2) a chain-of-thought prompt that gets a much better answer, (3) explain exactly why CoT works better for this specific task.
```

**Tool Use Architecture (Week 3):**
```
Explain the Anthropic Tool Use flow to me step by step, as if I'm implementing it for the first time. Specifically: (1) What exactly do I put in the 'tools' parameter of the API call? (2) How does Claude signal it wants to call a tool — what does that response look like? (3) How do I pass the tool result back? (4) How do I know when the agent is done? Show me a minimal code skeleton with comments.
```

**ReAct Loop (Week 5):**
```
I just read the ReAct paper. Explain the ReAct loop (Reason + Act) to me using a concrete example. Scenario: I ask an agent 'What is the current population of Tokyo?' Walk me through every step: (1) what Claude's Thought is, (2) what Action it takes, (3) what the Observation is, (4) how it decides to stop. Show me pseudocode of the loop, not full Python yet.
```

**Vector Stores (Week 6):**
```
Explain vector stores and semantic search to me using a concrete analogy. I understand that words become numbers (embeddings). But explain: (1) Why are similar meanings close together in vector space? Give me a geometric intuition. (2) What is the difference between ChromaDB, Pinecone, and Weaviate — when would I choose each? (3) How does ChromaDB decide which documents are 'similar' to my query?
```

**MCP Architecture (Week 7):**
```
Explain Model Context Protocol (MCP) to me as a developer building my first server. Specifically: (1) What is the relationship between an MCP server and Claude — is it like a plugin, an API, or something else? (2) When I add a @mcp.tool() decorator to a function, what exactly happens when Claude 'calls' that tool? (3) What is the difference between MCP tools, resources, and prompts?
```

### Coding Help

**Serper search function (Week 3):**
```
Write me a Python function called search_web(query: str, num_results: int = 5) -> list[dict] that calls the Serper.dev search API. Requirements: loads SERPER_API_KEY from environment, makes a POST request to https://google.serper.dev/search, returns a list of dicts each with 'title', 'url', and 'snippet' keys, handles API errors gracefully with a try/except.
```

**ReAct agent implementation (Week 5):**
```
I want to implement a ReAct agent from scratch using only the Anthropic Python SDK — no LangChain. Explain the exact structure of the Python code I need. Specifically: (1) How do I set up the messages list before the first call? (2) When Claude returns a tool_use block, what does that JSON look like exactly? (3) How do I append the tool result back into messages? (4) What is the loop termination condition? Show me a skeleton with comments.
```

**ChromaDB memory system (Week 6):**
```
Help me add persistent memory to my ReAct agent using ChromaDB. I want two functions: (1) save_memory(question: str, facts: str, answer: str) — stores to a ChromaDB PersistentClient at './memory', with metadata including a timestamp. (2) retrieve_memories(query: str, n: int = 3) -> list[str] — queries ChromaDB by similarity and returns the top n memories formatted as a readable string. Show complete code for both functions.
```

**LangGraph conditional routing (Week 9):**
```
I'm building a LangGraph pipeline. After my Analyst node runs, I need conditional routing: if state['quality_score'] < 6 and state['iteration_count'] < 3, route back to the Researcher node. Otherwise route to the Writer node. Show me: (1) the conditional function signature, (2) how to add it to the StateGraph with add_conditional_edges(), (3) how to increment iteration_count in the Researcher node to prevent infinite loops.
```

**Retry logic with tenacity (Week 10):**
```
I have multiple places in my code that call the Anthropic API. Show me how to add proper retry logic using the tenacity library. I want: (1) Retry up to 3 times, (2) Wait 1s, then 2s, then 4s between retries (exponential backoff), (3) Only retry on RateLimitError and APIConnectionError — not on AuthenticationError, (4) Log each retry attempt with the error message. Show me: the decorator, where to import it, and how to apply it to a function.
```

**pytest tests for LangGraph (Week 10):**
```
Help me write pytest tests for my LangGraph pipeline. I have a node called analyst_node(state: PipelineState) that calls the Claude API and returns a quality_score between 1-10. I want to test it without making real API calls. Show me: (1) how to mock the Claude API response using unittest.mock, (2) a test that checks quality_score is always between 1 and 10, (3) a test that checks the node handles an empty raw_research list gracefully.
```

**FastAPI + Stripe backend (Week 11):**
```
I'm building a FastAPI backend for my AI product. I need: (1) A POST /research endpoint that takes {question: str} in the request body, checks for an X-API-Key header against an env variable, calls my research_agent() function, and returns {answer: str, sources: list[str]}. (2) A GET /checkout endpoint that creates a Stripe Checkout Session for a $19/month subscription and returns the checkout URL. Show me the complete api.py file.
```

### Debugging

**App crashes (any week):**
```
My [Streamlit/FastAPI] app using the Anthropic Python SDK is crashing with this error: [paste the error]. I'm building an agentic AI application. Explain: (1) what this error means in plain English, (2) what file and line to look at, (3) the exact fix I need to make. Show the corrected code.
```

**Agent loop not working (Week 5):**
```
My ReAct agent built with the Anthropic SDK is not working correctly. Here is my agent loop code: [paste your code]. Here is the error or unexpected behaviour: [describe it]. Tell me: (1) what the root cause is, (2) which specific line to fix, (3) the corrected code. Also tell me what I should add to my logging to catch this type of error faster next time.
```

### Launch & Marketing

**LinkedIn launch post (Week 4):**
```
Help me write a LinkedIn post about my first AI product launch. Context: I just built a Smart Summariser that takes URLs, PDFs, or pasted text and produces 3 different summary styles using the Claude API. I built it in 4 weeks while studying 2 hours per day. Write a post that: (1) opens with what the product does, (2) shares one thing I learned, (3) includes the live URL, (4) ends with a question to spark comments. Keep it under 200 words.
```

**Landing page copy (Week 11):**
```
Help me write landing page copy for my AI product. Product: [describe in 2 sentences]. Write: (1) A headline under 10 words that leads with the outcome, not the technology. (2) A sub-headline that explains what it does and who it's for. (3) 3 feature descriptions — each with: feature name (3 words), what it does (1 sentence), why it matters (1 sentence). (4) A pricing section with one plan at $19/month — list 5 things included. (5) A CTA button label more specific than 'Get Started'.
```

**Product Hunt tagline (Week 12):**
```
Help me write a Product Hunt tagline for my AI product. Product: [describe in 1 sentence]. Requirements: (1) Under 60 characters, (2) Lead with the outcome for the user — not the technology, (3) No buzzwords like 'revolutionary', 'AI-powered', or 'next-gen', (4) Make someone who has never heard of you want to click. Give me 5 options ranked by likely click-through rate.
```

**3-month retrospective post (Week 12):**
```
I just completed a 3-month Agentic AI learning journey and shipped my third product. Help me write a LinkedIn post that tells the full story. Context: I started with no LLM experience in May 2026. I shipped: Month 1 — Smart Summariser, Month 2 — Research Agent, Month 3 — [your product name]. I studied 2 hours per day on weekdays and 5 hours on weekends. Write a post (under 300 words) that: tells the arc of the journey, shows the progression, shares the biggest surprise, and ends with what I'm building next.
```

---

## Key Code Snippets

### Every-Session Commands
```bash
# Activate venv — run this every time you open Terminal
source ~/agentic-ai/.venv/bin/activate

# Run a script
cd ~/agentic-ai
python week01/my_script.py

# Install a package
pip install package-name

# Save work to Git
git add .
git commit -m "What I built today"
git push

# Start Jupyter
jupyter notebook
```

### Claude Model Names (current as of May 2026)
```python
# Use these exact strings in your code
HAIKU   = 'claude-haiku-4-5-20251001'   # cheapest, fastest
SONNET  = 'claude-sonnet-4-6'           # best balance — use for production
OPUS    = 'claude-opus-4-6'             # most capable, most expensive
```

### Minimal Claude API call
```python
import anthropic, os
from dotenv import load_dotenv

load_dotenv()
client = anthropic.Anthropic(api_key=os.getenv('ANTHROPIC_API_KEY'))

def ask_claude(prompt: str, system: str = None) -> str:
    msg = client.messages.create(
        model='claude-haiku-4-5-20251001',
        max_tokens=1024,
        system=system or "You are a helpful assistant.",
        messages=[{'role': 'user', 'content': prompt}]
    )
    return msg.content[0].text
```

### Check API usage (monthly spend)
- Anthropic: https://console.anthropic.com/settings/usage
- DeepSeek:  https://platform.deepseek.com/usage
- OpenAI:    https://platform.openai.com/usage

---

## Milestone Tracker

| Week | Milestone | Status |
|------|-----------|--------|
| Week 2 | Can write and explain 5 prompt techniques for the same task | [ ] |
| Week 4 | Smart Summariser live at public URL — shown to 2+ real people | [ ] |
| Week 6 | Agent with 2+ tools + persistent ChromaDB memory across sessions | [ ] |
| Week 8 | Research Agent live — answers better than 30-minute Google search | [ ] |
| Week 10 | Tracing on, retries working, 5 tests passing, cost logged per run | [ ] |
| Week 12 | Live product with landing page, pricing, and first user or first dollar | [ ] |

---

*Last updated: May 2026 | Agentic AI 3-Month Learning Plan for Gaurav Verma*
