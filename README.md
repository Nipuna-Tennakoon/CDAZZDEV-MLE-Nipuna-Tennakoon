# CDAZZDEV-MLE-Nipuna-Tennakoon

Submission repository for the **CDAZZDEV Senior Machine Learning Engineer** technical assessment.

## Environment setup

The project is managed with [uv](https://docs.astral.sh/uv/).

```bash
# install uv (once)
curl -LsSf https://astral.sh/uv/install.sh | sh

# create the virtual environment and install locked dependencies
uv sync

# register the kernel for Jupyter / VS Code
uv run python -m ipykernel install --user --name cdazzdev-mle
```

Python is pinned to **3.12** (`.python-version`) to match the Google Colab runtime.

## Secrets

Copy `.env.example` to `.env` and fill in your keys. `.env` is git-ignored — no API keys or
tokens are ever committed. On Google Colab the notebooks read the same names from
**Colab Secrets** instead.

## Repository layout

```
.
├── task2_genai/            # Task 2 - Generative AI (domain fine-tuning)
│   ├── data/               # synthetic dataset (train / val / test JSONL)
│   ├── models/             # local checkpoints & merged model (git-ignored)
│   ├── notebooks/          # executable notebooks (run on Colab T4)
│   ├── prompts/            # teacher-model prompts
│   └── reports/            # charts and metric summaries
├── CITATIONS.md            # AI-tool and open-source citations
├── .env.example            # template for required secrets
└── pyproject.toml / uv.lock
```

## Task 2 - Generative AI: General-Practice Symptom-Intake Agent

**Use case (medical triage):** a small, patient-facing model that runs the intake step before
a general practitioner (GP) consultation. It covers concerns in **any part of the body**
(fever, cough, headache, stomach, urinary, joints, skin, mood, sleep, ...) and asks short,
calm, one-at-a-time questions at **general-practice depth** - broad, plain-language questions
that give the doctor enough for a first impression, not specialist work-ups.

The agent **only gathers symptoms**:

- it never diagnoses, names or hints at a possible condition, or lists causes;
- it never recommends, prescribes or comments on medicines, doses, treatments or self-care;
- when the patient asks "what do I have?" or "what should I take?", it defers to the doctor
  and keeps gathering symptoms;
- it closes by recapping the symptoms and handing them over to the clinician, and the only
  action it ever directs is emergency care for red flags (e.g. chest pain with breathlessness).

| Notebook | Purpose |
|---|---|
| `task2_genai/notebooks/01_data_generation.ipynb` | Synthetic dataset from free-tier teacher models (Groq Llama-3.3-70B / GPT-OSS-120B, OpenRouter), dedup, diversity analysis, 80/10/10 split |
| `task2_genai/notebooks/02_finetuning.ipynb` | QLoRA (4-bit NF4) fine-tuning of Qwen2.5-1.5B-Instruct on a Colab T4, justified hyperparameters, per-epoch train/val loss tracked in Weights & Biases, `merge_and_unload()` and push to Hugging Face Hub |

Run order: `01_data_generation.ipynb` -> `02_finetuning.ipynb`.
