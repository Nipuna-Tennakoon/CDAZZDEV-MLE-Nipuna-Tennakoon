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
