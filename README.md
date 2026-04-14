## PocketResearch: Multi-Agent AI Research Assistant

PocketResearch is a Python project that runs a multi-agent research pipeline using LangChain + Gemini.

It performs four stages:

1. Search the web for relevant and recent information (Tavily).
2. Read one selected source deeply by scraping page content.
3. Write a structured research report.
4. Critique and score the generated report.

The project includes:

- A Streamlit web app UI (`app.py`).
- A CLI pipeline runner (`pipeline.py`).
- Agent and chain definitions (`agents.py`).
- Web tools for search and scraping (`tools.py`).

---

## How It Works

Pipeline flow:

1. **Search Agent**
	Uses the `web_search` tool to fetch top web results (title, URL, snippet).
2. **Reader Agent**
	Uses the `scrape_url` tool to extract clean text from the most relevant URL.
3. **Writer Chain**
	Combines search + scraped context into a detailed markdown report.
4. **Critic Chain**
	Reviews the report and returns score, strengths, and improvements.

The model backend is Gemini via `langchain-google-genai`.

---

## Tech Stack

- Python 3.13+
- LangChain (`langchain`, `langchain-core`, `langchain-community`)
- Gemini integration (`langchain-google-genai`, `google-generativeai`)
- Tavily API (`tavily-python`)
- Web scraping (`requests`, `beautifulsoup4`)
- UI (`streamlit`)

---

## Project Structure

```text
research_tool/
|- app.py            # Streamlit UI and pipeline execution flow
|- pipeline.py       # CLI pipeline runner
|- agents.py         # LLM setup + agents + writer/critic chains
|- tools.py          # Tavily search and URL scraping tools
|- requirements.txt  # pip dependencies
|- pyproject.toml    # uv/project metadata and dependencies
|- main.py           # minimal placeholder entry script
```

---

## Setup

### 1) Clone and enter project

```bash
git clone <your-repo-url>
cd research_tool
```

### 2) Create and activate virtual environment

On Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

### 3) Install dependencies

Using pip:

```bash
pip install -r requirements.txt
```

Or using uv:

```bash
uv sync
```

### 4) Configure environment variables

Create a `.env` file in the project root:

```env
GEMINI_API_KEY=your_gemini_api_key_here
TAVILY_API_KEY=your_tavily_api_key_here
```

---

## Running the Project

### Streamlit app (recommended)

```bash
streamlit run app.py
``

### CLI pipeline

```bash
python pipeline.py
```

## Current Model Configuration

Defined in `agents.py`:

- Provider: Gemini
- Class: `ChatGoogleGenerativeAI`
- Model: `gemini-2.5-flash`
- Temperature: `0`