# vLLM Chatbot Lab (AMD MI300)

Hands-on notebook where I built a simple chatbot on top of an open-source LLM served with **vLLM**, running on an **AMD MI300 GPU** in the AMD Developer Cloud.

> **Credit:** This notebook is based on the *"Building Your First AI Chatbot"* lab from the AMD Developer Cloud. The lab structure and explanatory text are theirs. I completed and ran it, and my own additions are listed under [My additions](#my-additions).

## What it covers

1. **Inference basics**: what happens when you send input to a trained model and get output back
2. **Loading a model with vLLM**: `Qwen/Qwen3-4B-Instruct-2507` on a single MI300
3. **A multi-turn chatbot**: a chat loop that keeps conversation history in a list of `{role, content}` messages
4. **System prompts**: changing the bot's behavior (Shakespeare, pirate) with a `system` message
5. **Sampling parameters**: how `temperature`, `max_tokens`, and `top_p` change the output
6. **A small UI**: an `ipywidgets` interface with sliders for the parameters above

## Stack

| Component | Details |
|---|---|
| Inference engine | vLLM 0.26.0 |
| Model | Qwen3-4B-Instruct-2507 (bfloat16) |
| Hardware | AMD Instinct MI300 (AMD Developer Cloud, ROCm) |
| Language | Python 3.12 |
| UI | ipywidgets |

## Running it

This notebook needs a GPU that vLLM supports. It will not run on a CPU-only machine or in a browser-based Python environment.

```bash
pip install vllm ipywidgets jupyter
jupyter notebook chatbot_vllm.ipynb
```

On an NVIDIA GPU (Colab, Kaggle, etc.) the code should work as-is. The "MI300" strings in the print statements are just labels.

The first cell downloads the model from Hugging Face, so expect a delay on the first run. Setting an `HF_TOKEN` avoids rate-limit warnings.

## Key takeaways

- `llm.chat()` is stateless. The chatbot "remembers" only because the full message list is re-sent on every turn.
- A system prompt is just the first message in that list with `role: "system"`, and it changes the bot's behavior noticeably.
- Lower `temperature` gives more predictable output, and higher values give more varied output. `top_p` limits how many candidate tokens the model samples from.
- vLLM makes serving an open model to a chat loop only a few lines of code.

## My additions

<!-- Fill this in with what you changed. Delete the section if you add nothing. -->

- [ ] Fixed the widget chatbot so it keeps conversation history across messages (the original sends each message alone)
- [ ] Added an experiment with a non-English system prompt (e.g. Urdu / Pashto) and notes on how the model handled it
- [ ] Other: _describe here_

## Notes

- Saved cell outputs are from a real run on the AMD Developer Cloud.
- All model rights belong to the Qwen team; see the [model card](https://huggingface.co/Qwen/Qwen3-4B-Instruct-2507) for its license.
