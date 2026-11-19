# GSM8K: Chain-of-Thought and Supervised Fine-Tuning Coursework

A small NLP coursework notebook exploring zero-shot chain-of-thought prompting and a supervised fine-tuning setup for Meta Llama 3.2 3B Instruct on GSM8K math problems.

## What is in this repository

- `SmallProject1.ipynb`: original coursework notebook, with the embedded access token replaced by environment-variable authentication.
- Uses a subset of **200 training examples** and **50 test examples**.
- Includes model loading, tokenization, zero-shot generation, and a Trainer-based fine-tuning attempt.

This is a coursework prototype. It is separate from my TabRL and LLM safety projects.

## Current state and limitations

The saved notebook is not a completed or validated benchmark:

- The original fine-tuning execution ends in a RuntimeError.
- The original zero-shot scoring checks whether the entire reference explanation appears in decoded output. It does not extract and compare final numeric answers.
- The saved zero-shot score should not be used as a reliable measure of model performance.
- `Trainer.evaluate()` reports a loss, which is not directly comparable with generated-answer accuracy.
- Generation assumes CUDA. Model loading uses FP16 and automatic device mapping; a CPU-only environment is not supported as written.
- The notebook defines two preprocessing functions. A cleanup should consolidate them, handle padding labels explicitly, and align evaluation prompts.
- Dependencies are not pinned, and this cleanup has not rerun model inference or training.

## Running the original experiment

1. Obtain access to the gated `meta-llama/Llama-3.2-3b-Instruct` model and accept its license.
2. Use a suitable CUDA environment. The notebook does not include a validated minimum VRAM requirement.
3. Set a newly created Hugging Face access token in the notebook kernel's environment under `HF_TOKEN`. Never paste a token into a committed cell.
4. Open `SmallProject1.ipynb`, review the limitations above, and inspect the code before running it.

For hosted notebooks, configure the secret through the hosting service and explicitly make it available as `HF_TOKEN` to the Python kernel. A local `.env` file is not automatically loaded by this notebook.

## Recovery plan

- Replace substring scoring with final-answer exact-match evaluation on generated continuation text.
- Use consistent prompts before and after training.
- Fix training placement and padding-label handling, then rerun the experiment.
- Record exact dependency versions, model revision, hardware, seed, and measured results.

## Data and model

- [GSM8K](https://huggingface.co/datasets/openai/gsm8k)
- [Meta Llama 3.2 3B Instruct](https://huggingface.co/meta-llama/Llama-3.2-3B-Instruct)

Dataset and model terms continue to apply. No model weights are included.

