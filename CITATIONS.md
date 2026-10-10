# Citations

This file documents all AI-tool assistance and adapted open-source code used in this
repository, as required by Section 2.2 of the assessment.

## AI assistance

| # | Tool | Scope | Prompt (summary) | Date |
|---|------|-------|------------------|------|
| 1 | Claude (claude-opus-5-5), Cowork | Project scaffold: `pyproject.toml`, `.gitignore`, `.env.example`, folder layout | "Initialize the project with uv and create the data / models / .env structure" | 2026-10-10 |
| 2 | Claude (claude-opus-5-5), Cowork | `task2_genai/notebooks/01_data_generation.ipynb`, `task2_genai/prompts/teacher_skin_intake.md` | "Create a synthetic data generation notebook adapted from my llm-fine-tuning-medical-chat project, using free-tier teacher models" | 2026-10-10 |

## Adapted code

| # | Source | Used in | Notes |
|---|--------|---------|-------|
| 1 | Author's own prior project `llm-fine-tuning-medical-chat` (private, MedirAI) - `notebooks/data_synthesis.ipynb`, `prompts/symptom_gathering_synthetic.md` | `01_data_generation.ipynb` | Quality gate, exact + PubMedBERT semantic de-duplication and leakage checks re-used; teacher pool moved to free-tier Groq / OpenRouter, generation stratified by concern, split changed to 80/10/10, diversity analysis added |
| 2 | `NeuML/pubmedbert-base-embeddings` - https://huggingface.co/NeuML/pubmedbert-base-embeddings | `01_data_generation.ipynb` | Sentence embeddings for near-duplicate detection |

## Teacher-model prompts

The full system prompt used for synthetic data generation is stored in
`task2_genai/prompts/` and printed in the appendix cell of the data-generation notebook.
