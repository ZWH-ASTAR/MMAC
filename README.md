# MMAC-Bench: A Multimodal Multilingual Asian Cultural Benchmark

Official repository for **MMAC-Bench**, a multimodal and multilingual benchmark for evaluating cultural understanding and reasoning in vision-language and language models.

The dataset is hosted on Hugging Face:

**Dataset:** https://huggingface.co/datasets/ZWHTXY/MMAC-Bench

## Overview

MMAC-Bench is designed to evaluate model performance on culturally grounded question answering across multiple Asian regions and languages. The benchmark contains both text-only and multimodal examples, including image-based questions and audio-related resources.

The dataset includes two splits:

* `text_only`: text-only question-answering examples.
* `multi_modal`: multimodal examples with image and speech/audio paths.

Each example may contain fields such as:

* `country`
* `region_code`
* `language`
* `modality`
* `question`
* `option1`, `option2`, `option3`, `option4`
* `correct_options`
* `category`
* `knowledge_point`
* `multi_step_reasoning`
* `image`
* `standard_english_audio`
* `english_with_accent_audio`
* `none_english_audio`

## Installation

```bash
pip install -U datasets huggingface_hub
```

## Load the Dataset

You can directly load the dataset from Hugging Face:

```python
from datasets import load_dataset

ds = load_dataset("ZWHTXY/MMAC-Bench")

print(ds)
print(ds["text_only"][0])
print(ds["multi_modal"][0])
```

Load one split only:

```python
from datasets import load_dataset

text_only = load_dataset("ZWHTXY/MMAC-Bench", split="text_only")
multi_modal = load_dataset("ZWHTXY/MMAC-Bench", split="multi_modal")
```

## Filter by Country or Language

```python
from datasets import load_dataset

ds = load_dataset("ZWHTXY/MMAC-Bench")

china_text = ds["text_only"].filter(
    lambda x: x["country"] == "China"
)

singapore_tamil_mm = ds["multi_modal"].filter(
    lambda x: x["country"] == "Singapore" and x["language"] == "Tamil"
)
```

## Download the Full Dataset Repository

To download the full Hugging Face repository, including raw JSON files, images, and audio files:

```python
from huggingface_hub import snapshot_download

local_dir = snapshot_download(
    repo_id="ZWHTXY/MMAC-Bench",
    repo_type="dataset",
)

print(local_dir)
```

Alternatively, you can use the Hugging Face CLI:

```bash
pip install -U huggingface_hub
hf download ZWHTXY/MMAC-Bench --repo-type dataset
```

For users who prefer Git:

```bash
git lfs install
git clone https://huggingface.co/datasets/ZWHTXY/MMAC-Bench
```

## Repository Structure

This GitHub repository contains code and documentation for using MMAC-Bench.

```text
MMAC-Bench/
├── README.md
├── scripts/
│   ├── load_dataset.py
│   └── evaluate.py
├── examples/
│   └── sample_usage.ipynb
├── results/
│   └── example_results.json
└── requirements.txt
```

The dataset files are not stored in this GitHub repository. Please download the dataset from Hugging Face.

## Example Usage

```python
from datasets import load_dataset

dataset = load_dataset("ZWHTXY/MMAC-Bench", split="text_only")

for example in dataset.select(range(3)):
    print("Question:", example["question"])
    print("Options:", example["option1"], example["option2"], example["option3"], example["option4"])
    print("Answer:", example["correct_options"])
    print()
```

## License

The dataset is released under the **CC BY 4.0** license. Please check the Hugging Face dataset page for the latest license information.

## Citation

If you use MMAC-Bench in your research, please cite our paper:

```bibtex
@inproceedings{yourbibkey2026mmacbench,
  title     = {MMAC-Bench: A Multimodal Multilingual Asian Cultural Benchmark},
  author    = {Author One and Author Two and Author Three},
  booktitle = {Proceedings of XXX},
  year      = {2026}
}
```

## Contact

For questions about the dataset or benchmark, please open an issue in this GitHub repository or contact the authors.
