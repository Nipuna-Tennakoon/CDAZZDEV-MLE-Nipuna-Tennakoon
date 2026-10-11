# Citations

This file documents all AI-tool assistance and adapted open-source code used in this
repository, as required by Section 2.2 of the assessment.

## AI assistance

| # | Tool | Scope | Prompt (summary) | Date |
|---|------|-------|------------------|------|
| 1 | Claude (claude-opus-5-5), Cowork | Project scaffold: `pyproject.toml`, `.gitignore`, `.env.example`, folder layout | "Initialize the project with uv and create the data / models / .env structure" | 2026-10-10 |
| 2 | Claude (claude-opus-5-5), Cowork | `task2_genai/notebooks/01_data_generation.ipynb`, `task2_genai/prompts/teacher_skin_intake.md` | "Create a synthetic data generation notebook adapted from my llm-fine-tuning-medical-chat project, using free-tier teacher models" | 2026-10-10 |
| 3 | Claude (claude-opus-5-5), Cowork | `task2_genai/notebooks/02_finetuning.ipynb` (QLoRA config, W&B integration, per-epoch loss callback, merge + Hub push) | "Create a fine-tuning notebook as developed in my llm-fine-tuning project, configured with Weights & Biases for metric monitoring" | 2026-10-10 |
| 4 | Claude (claude-opus-5-5), Claude Code | Scope change from skin intake to general-practice intake: `task2_genai/prompts/teacher_gp_intake.md` (renamed from `teacher_skin_intake.md`), system prompt, concern taxonomy and quality-gate patterns in `01_data_generation.ipynb`, W&B / Hub names in `02_finetuning.ipynb`, README | "Convert the skin symptom-intake agent into a general practitioner intake agent that asks general questions about any body part, only gathers symptoms, and never diagnoses or suggests medication" | 2026-10-11 |
| 5 | Claude (claude-opus-5-5), Claude Code | `01_data_generation.ipynb` teacher pool: OpenAI GPT-4.1-mini / GPT-4o-mini as primary teachers with parallel workers, free tiers made optional | "Update the code to use my OpenAI API key for data generation" | 2026-10-11 |

## Adapted code

| # | Source | Used in | Notes |
|---|--------|---------|-------|
| 1 | Author's own prior project `llm-fine-tuning-medical-chat` (private, MedirAI) - `notebooks/data_synthesis.ipynb`, `prompts/symptom_gathering_synthetic.md` | `01_data_generation.ipynb` | Quality gate, exact + PubMedBERT semantic de-duplication and leakage checks re-used; teacher pool moved to OpenAI (GPT-4.1-mini / GPT-4o-mini) with optional free-tier Groq / OpenRouter, generation stratified by concern, split changed to 80/10/10, diversity analysis added |
| 2 | Author's own prior project `llm-fine-tuning-medical-chat` - `notebooks/training.ipynb` | `02_finetuning.ipynb` | Prompt/target split with `-100` label masking and LoRA target modules re-used; MLflow replaced by Weights & Biases, full-FT/LoRA replaced by 4-bit NF4 QLoRA, merge + Hub push added |
| 3 | Dettmers et al., *QLoRA: Efficient Finetuning of Quantized LLMs* (2023) - https://arxiv.org/abs/2305.14314 | `02_finetuning.ipynb` | NF4 + double quantisation, all-linear-layer LoRA, paged 8-bit AdamW, max grad norm 0.3 |
| 4 | `NeuML/pubmedbert-base-embeddings` - https://huggingface.co/NeuML/pubmedbert-base-embeddings | `01_data_generation.ipynb` | Sentence embeddings for near-duplicate detection |

## Teacher-model prompts

The full system prompt used for synthetic data generation is stored in
`task2_genai/prompts/` and printed in the appendix cell of the data-generation notebook.
