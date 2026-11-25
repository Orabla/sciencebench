# ScienceBench

A benchmark for bilingual scientific literature understanding, covering **16 tasks and 6,102
samples** from scientific papers and patents in Chinese and English.

## What the benchmark measures

The benchmark evaluates three families of scientific NLP tasks:

- **Structured extraction** — named entity recognition, relation extraction and completion,
  knowledge linking, key-feature and keyword extraction.
- **Classification and matching** — semantic matching and subject or topic classification.
- **Generation and translation** — summarization, title generation, use-case generation,
  technical summarization and Chinese-to-English translation.

Each task ships a deterministic parser and a task-specific metric, so every prediction is scored
from its parsed structure rather than from raw string equality. Metrics include accuracy,
macro-F1, micro-F1, relation-F1, link-F1, keyword-F1, ROUGE-L and BLEU.

## Data

The `data/` directory contains one JSONL file per task plus a `manifest.json` with sample counts
and per-file checksums. Each record follows a common schema:

```json
{
  "id": "unique-id",
  "task": "task-name",
  "lang": "zh | en | zh-en",
  "instruction": "task instruction",
  "input": "input text",
  "output": "reference output",
  "system": "optional system prompt",
  "meta": {"source": "...", "raw_index": 0}
}
```

Use `manifest.json` to pin the exact data release in your experiments.

## Quick start

```python
import json
from pathlib import Path

data = Path("data")
rows = [json.loads(line) for line in (data / "sm.jsonl").open(encoding="utf-8")]
print(len(rows), rows[0]["instruction"])
```

## License

Code in this repository is released under the MIT License. Data are provided for research use;
upstream licensing is documented in `LICENSE-DATA`.

## Citation

If you use this benchmark, please cite the accompanying SciGPT paper.
