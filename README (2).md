# 🔭 VisionaryX — Free AI Agent (No API Key)

VisionaryX is a simple AI agent that runs inside a **Jupyter Notebook**, fully **locally**.
No OpenAI / Gemini / Anthropic API key needed — just run and chat.

## ✨ Features

| Feature | Example |
|---|---|
| 🧮 Calculator | `calculate 12*(3+4)` |
| 🕒 Date & time | `what is the time` |
| 🌐 Web search (DuckDuckGo, no key) | `search latest python version` |
| 🗒️ Notes | `remember my exam is on Friday` → `recall` |
| 💬 General chat | any question (uses a small open-source Qwen model) |

If the model can't be loaded (low RAM / no internet), VisionaryX automatically falls back to **tools-only mode**.

## 📁 Files

```
VisionaryX/
├── VisionaryX.ipynb   # the agent
├── requirements.txt   # dependencies
└── README.md
```

## 🚀 Run locally

```bash
git clone https://github.com/<your-username>/VisionaryX.git
cd VisionaryX
pip install -r requirements.txt
jupyter notebook VisionaryX.ipynb
```

Then click **Run → Run All Cells** and chat in the last cell. Type `exit` to stop.

> First run downloads the model (~3 GB for 1.5B). After that it works offline for chat/tools
> (web search still needs internet).

## ☁️ Run on Google Colab (free GPU)

1. Upload `VisionaryX.ipynb` and `requirements.txt` to Colab (or open from GitHub).
2. Run all cells.

## ⚙️ Settings (Cell 2)

| Setting | Meaning |
|---|---|
| `MODEL_NAME` | `Qwen/Qwen2.5-1.5B-Instruct` (default). Use `Qwen/Qwen2.5-0.5B-Instruct` for low RAM |
| `USE_LLM` | `False` = tools-only mode (instant, no download) |
| `MAX_NEW_TOKENS` | Max reply length |

## 🧠 How it works

1. **Router** checks if your message needs a tool (math, time, search, notes).
2. **Tools** run safely (the calculator uses `ast`, not `eval`).
3. **Brain** (local LLM) answers general chat and summarizes search results.

## ➕ Add your own tool

```python
def my_tool(arg: str) -> str:
    return "result"

TOOLS["my_tool"] = my_tool
# then add a rule for it inside route()
```

## 🛠️ Troubleshooting

- **Out of memory** → switch to the 0.5B model or set `USE_LLM = False`.
- **Slow replies** → CPU is slow for LLMs; use Colab GPU or the 0.5B model.
- **Web search fails** → check your internet connection.

## 📄 License

MIT — free to use and modify.
