# AI Research Crew

Multi-agent AI research system built with [crewAI](https://crewai.com). Two agents collaborate to research a topic and produce a structured report.

## Agents

- **Researcher** — Searches the web for the latest developments on a given topic
- **Reporting Analyst** — Synthesizes research findings into a detailed markdown report

## Tools

- `ScrapeWebsiteTool` — enables the researcher to fetch and read web page content (no API key required)
- `CustomTool` — placeholder for additional tooling (see `src/my_project/tools/custom_tool.py`)

## Setup

**Requirements:** Python >=3.10 <3.14, [UV](https://docs.astral.sh/uv/)

```bash
pip install uv
cd my_project
crewai install
```

### Environment Variables

Copy or rename `.env` with the following:

```env
OPENROUTER_API_KEY=sk-or-v1-...
OPENAI_API_BASE=https://openrouter.ai/api/v1
MODEL=openrouter/nvidia/nemotron-3-super-120b-a12b:free
```

You can swap the model for any [OpenRouter-compatible model](https://openrouter.ai/models) by changing `MODEL`.

## Usage

```bash
crewai run
```

To change the research topic, edit the `inputs` dict in `src/my_project/main.py`:

```python
inputs = {
    'topic': 'AI LLMs',
    'current_year': str(datetime.now().year)
}
```

Output is written to `report.md`.

### Other Commands

```bash
crewai test -n 2 -m gpt-4o-mini   # Evaluate crew performance
crewai train -n 5 -f training.json   # Train with examples
```

## Customizing

- `src/my_project/config/agents.yaml` — agent roles, goals, backstories
- `src/my_project/config/tasks.yaml` — task descriptions and expected outputs
- `src/my_project/crew.py` — agent logic, tools, and crew configuration
- `src/my_project/main.py` — entry point and runtime inputs

## Project Structure

```
my_project/
├── src/my_project/
│   ├── config/
│   │   ├── agents.yaml
│   │   └── tasks.yaml
│   ├── tools/
│   │   └── custom_tool.py
│   ├── crew.py
│   └── main.py
├── knowledge/
│   └── user_preference.txt
├── .env
├── pyproject.toml
└── README.md
```
