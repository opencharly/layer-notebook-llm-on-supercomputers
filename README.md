# notebook-llm-on-supercomputers

The **LLMs on Supercomputers** course notebook collection as a charly *data layer* —
15 Jupyter notebooks from TU Wien's AI Factory Austria, seeded into the workspace
volume of a Jupyter image at deploy time.

The `notebook-llm-on-supercomputers` candy ships no packages, no services and no
dependencies. Its whole job is to stage `data/llms_on_supercomputers/` into the
`workspace` volume's `llms_on_supercomputers/` subdirectory, so a freshly deployed
JupyterLab pod has the course material ready on first open.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `notebook-llm-on-supercomputers` |
| Type | Data-only — no packages, no services, no dependencies |
| Volume | `workspace` → `/workspace` (supplied by the jupyter base) |
| Data | `data/llms_on_supercomputers` → `workspace` volume, dest `llms_on_supercomputers` |
| Notebooks | 15 `.ipynb` files across 4 course days |
| Supporting data | `datasets/` CSVs (booking, code review, health Q&A), `notebooks.yaml`, `simplified_output.json` |

## Course contents

The collection is organized by day, with the filename prefix naming the day:

| Prefix | Day | Notebooks |
|---|---|---|
| `D0_*` | Setup | Bazzite environment setup, GPU verification, Ollama connectivity |
| `D1_*` | Prompt engineering | LangChain prompting, templates/parsing, chaining, LLM evaluation, LLM-as-a-Judge, prompt optimization |
| `D2_*` | Retrieval-augmented generation | RAG with pandas, RAG with LangChain + ChromaDB |
| `D3_*` | Fine-tuning on one GPU | Transformer architecture, PyTorch and HuggingFace fine-tuning, quantization, PEFT/LoRA, Unsloth |

The `D0`–`D2` notebooks talk to an Ollama server through the `OLLAMA_HOST`
environment variable; the `D3` fine-tuning notebooks run locally against a GPU and
need no server.

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list — for example the
`jupyter-ml-notebook` box does exactly this:

```yaml
jupyter-ml-notebook:
  candy:
    # the named box's value is the box BODY; `base:` and the `candy:` list are its keys
    base: fedora-nonfree
    candy:
      - '@github.com/opencharly/layer-notebook-llm-on-supercomputers:v2026.240.0119'
      # ... other notebook data layers
```

Deploy the box; `charly config`/`charly update` copies the staged data into the
workspace volume at `<workspace>/llms_on_supercomputers/`. Open
`http://localhost:8888` and navigate to `llms_on_supercomputers/`.

## Layout

- `charly.yml` — the `notebook-llm-on-supercomputers:` candy entity (the `data:`
  mapping and the `plan:` checks) plus the embedded `skill:` entity.
- `data/llms_on_supercomputers/` — the 15 notebooks and their supporting datasets.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-jupyter:notebook-llm-on-supercomputers` — the collection,
  its contents, and the notebook compatibility notes.
- Sibling data layers: `/charly-jupyter:notebook-ollama`,
  `/charly-jupyter:notebook-openrouter`, `/charly-jupyter:notebook-templates`,
  `/charly-jupyter:notebook-finetuning`.
- Consuming box: `/charly-jupyter:jupyter-ml-notebook`.
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella.
