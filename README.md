# 🔧 Prompt Sequencer Tool for ChatGPT

## Overview

Automate sequential prompt execution for ChatGPT or open-source LLMs.
This tool allows you to feed prompts from a file, run them one by one, collect responses, and export the entire output into a single Markdown, TXT, or PDF file. Ideal for developers, educators, and AI builders who want to streamline multi-step content generation workflows.

---

## 1. Problem Statement

Manually entering a long list of prompts into ChatGPT, copying outputs one by one, and stitching them together is time-consuming and inefficient.

This becomes a bottleneck for:

- AI educators
- Content teams
- ML engineers
- Developers generating structured documents or code

There is no native way to batch prompts, automate execution, and export results cleanly - especially in open workflows.

---

## 2. Features

- Load a list of prompts from `.json` or `.txt`
- Automatically execute them using OpenAI or local LLMs
- Collect all responses in order
- Export to `.md`, `.txt`, or `.pdf`
- CLI-first with options for GUI/web UI (optional)

---

## 3. Use Cases

| Use Case             | Description                                   |
| -------------------- | --------------------------------------------- |
| Course Generator     | Input lesson topics, get entire module drafts |
| Dev Docs Creation    | Automate README, CLI help, changelogs         |
| Marketing Automation | Auto-generate blog + tweet + summary per idea |
| Code System Builder  | Prompt multiple service templates in order    |

---

## 4. Tech Stack

- Python 3.8+
- `openai`, `json`, `os`, `argparse`
- PDF export: `fpdf`, `markdown2`
- Optional OSS: `llama-cpp-python`, Hugging Face `transformers`, Ollama, LM Studio

---

## 5. Input Format (JSON)

```json
[
  { "title": "Module 1: Introduction to AI", "prompt": "Explain what AI is in simple terms." },
  { "title": "Module 2: NLP Basics", "prompt": "What is NLP and why is it important?" },
  { "title": "Module 3: BERT Overview", "prompt": "Describe BERT and its architecture." }
]
```

---

## 6. Output Format (Markdown)

```markdown
# Module 1: Introduction to AI
<ChatGPT Response>

# Module 2: NLP Basics
<ChatGPT Response>

# Module 3: BERT Overview
<ChatGPT Response>
```

---

## 7. Code: Using OpenAI GPT-4

```python
import openai, json

openai.api_key = "your_openai_key"

with open("prompts.json", "r") as f:
    prompts = json.load(f)

output = []

for item in prompts:
    res = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": item["prompt"]}]
    )
    response = res.choices[0].message['content']
    output.append(f"# {item['title']}\n\n{response}\n\n")

with open("output.md", "w", encoding="utf-8") as f:
    f.writelines(output)
```

---

## 8. Code: Using Open-Source LLMs (Offline)

```python
from llama_cpp import Llama
import json

llm = Llama(model_path="models/llama-2-7b-chat.ggmlv3.q4_0.bin")

with open("prompts.json", "r") as f:
    prompts = json.load(f)

output = []

for item in prompts:
    response = llm(f"{item['prompt']}", max_tokens=1024)
    output.append(f"# {item['title']}\n\n{response['choices'][0]['text'].strip()}\n\n")

with open("output.md", "w", encoding="utf-8") as f:
    f.writelines(output)
```

---

## 9. Optional Enhancements

- Retry logic & error logging
- CLI flags: `--format`, `--delay`, `--model`
- Export directly to Notion, Google Docs, GitHub Gist
- Streamlit or Flask-based Web UI
- Token usage logs
- LangChain or RAG integration

---

## 10. Contributing

Contributions, bug fixes, or ideas are welcome. Fork the repo, make your changes, and submit a PR.

---

## 11. License

This project is licensed under the MIT License. You are free to use, modify, and distribute this code for personal and commercial purposes, provided you include the original license and copyright notice.

---

## 12. Live Demo / Blog / Docs

📎 Coming Soon: https\://suniltechie.com/blog/chatgpt-batch-tool

---

**Built with ❤️ by Sunil Sharma**

> Helping professionals master AI, full stack systems, and data workflows.

