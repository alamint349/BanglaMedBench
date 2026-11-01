# BanglaMedBench

### A Native Bangla Benchmark for Evaluating Medical Language Models

Bangla is the sixth most spoken language in the world, with more than 230 million speakers across Bangladesh and eastern India. Yet, despite its large speaker population, Bangla remains substantially underrepresented in medical natural language processing (NLP) evaluation.

Existing multilingual medical benchmarks often exclude Bangla or represent it through machine-translated English medical examinations. Such benchmarks conflate medical reasoning with translation quality and therefore provide limited evidence about how well language models understand medical content expressed naturally in Bangla.

**BanglaMedBench** is a native Bangla medical benchmark designed to evaluate medical knowledge, language understanding, register robustness, and dialectal variation in Bangla.

Rather than translating existing English examinations, BanglaMedBench is constructed from Bangla-medium allied-health curricula, national public-health protocols, and expert-authored clinical vignettes.

---

## Overview

BanglaMedBench evaluates whether language models can maintain medical competence across the linguistic conditions encountered in real-world Bangla-speaking clinical environments.

The benchmark consists of a primary set of **\NUM{} multiple-choice questions** spanning **\NUM{} clinical and preclinical domains**, together with three controlled evaluation axes:

1. **English Parallel Set**  
   Item-matched English versions of Bangla questions, allowing us to distinguish language-dependent failures from failures caused by missing medical knowledge.

2. **Register-Controlled Set**  
   Semantically matched clinical questions expressed in:
   - Formal Bangla
   - Naturally code-mixed clinical Bangla
   - Romanised Bangla

3. **Dialectal Patient-Narrative Set**  
   Identical clinical presentations expressed using regional varieties including:
   - Sylheti
   - Chittagonian
   - Rangpuri

This design allows BanglaMedBench to move beyond a single aggregate accuracy score and investigate **where and why medical language models fail in Bangla**.

---

## Why BanglaMedBench?

Medical communication in Bangladesh and other Bangla-speaking communities involves a linguistic mismatch.

Medical education is frequently delivered through English-language textbooks, examinations, and terminology, while communication with patients often occurs in Bangla, including informal code-mixing and regional dialects.

Consequently, evaluating a model only on formal, standard Bangla medical questions does not fully capture its potential clinical usefulness.

We therefore investigate three related questions:

> **Does a model know the medicine?**

> **Can the model express and understand that knowledge in Bangla?**

> **Can the model maintain that competence when Bangla becomes informal, code-mixed, romanised, or dialectal?**

BanglaMedBench is designed to separate these factors.

---

## Benchmark Structure

```text
BanglaMedBench
│
├── Main Benchmark
│   └── Formal Bangla Medical MCQs
│
├── Axis I: English Parallel
│   └── Item-matched English questions
│
├── Axis II: Register Control
│   ├── Formal Bangla
│   ├── Code-mixed Clinical Bangla
│   └── Romanised Bangla
│
└── Axis III: Dialectal Narratives
    ├── Sylheti
    ├── Chittagonian
    └── Rangpuri
```

---

## Dataset Composition

| Component | Language / Variety | Purpose |
|---|---|---|
| Main Benchmark | Formal Bangla | Core medical knowledge evaluation |
| English Parallel | English | Separate language effects from medical knowledge |
| Register-Controlled | Formal Bangla | Standard clinical register |
| Register-Controlled | Code-mixed Bangla | Realistic clinical communication |
| Register-Controlled | Romanised Bangla | Informal digital communication |
| Dialectal Narratives | Sylheti | Regional robustness |
| Dialectal Narratives | Chittagonian | Regional robustness |
| Dialectal Narratives | Rangpuri | Regional robustness |

Detailed dataset statistics will be reported in the accompanying paper and released with the benchmark.

---

## Medical Domains

The benchmark covers **\NUM{} clinical and preclinical domains**.

The current domain taxonomy includes:

- `TODO: Domain 1`
- `TODO: Domain 2`
- `TODO: Domain 3`
- `TODO: Domain 4`
- `TODO: Domain 5`
- `...`

Each item is associated with a domain label to enable domain-level analysis.

---

## Data Sources

BanglaMedBench is intentionally **not constructed by translating an existing English medical examination**.

Questions are developed from three primary sources:

### 1. Bangla-Medium Allied-Health Curricula

Educational materials and curricula used in Bangla-medium allied-health training provide the foundation for assessing foundational medical and clinical knowledge.

### 2. National Public-Health Protocols

Relevant national public-health guidance and clinical protocols are used to construct questions grounded in healthcare practice in Bangladesh.

### 3. Expert-Authored Clinical Vignettes

Clinical vignettes are authored and reviewed by domain experts to represent realistic patient presentations and medical reasoning scenarios.

All questions undergo a structured quality-control process before inclusion.

---

## Annotation and Quality Control

Each benchmark item is associated with structured metadata.

Example:

```json
{
  "item_id": "BMB_000001",
  "domain": "TODO",
  "question": "TODO",
  "options": [
    "A. TODO",
    "B. TODO",
    "C. TODO",
    "D. TODO"
  ],
  "answer": "B",
  "language": "bn",
  "register": "formal",
  "source_type": "expert_authored",
  "difficulty": "TODO"
}
```

Where applicable, additional metadata includes:

- Medical domain
- Question type
- Language
- Register
- Dialect
- Source category
- Difficulty
- Correct answer
- Clinical presentation category
- Item-matching identifier

---

## Evaluation Axes

### 1. Medical Knowledge vs. Language

The item-matched English parallel set enables direct comparison between:

```text
Bangla Question
      │
      ▼
   Model
      │
      ▼
 Bangla Accuracy
      │
      │ compare
      ▼
English Parallel
      │
      ▼
English Accuracy
```

A substantial Bangla–English performance gap may indicate that a model possesses relevant medical knowledge but struggles to access or apply it in Bangla.

---

### 2. Register Robustness

We evaluate the same underlying clinical content across multiple linguistic registers:

```text
Formal Bangla
      │
      ├──► Code-mixed Bangla
      │
      └──► Romanised Bangla
```

This allows us to measure whether models remain medically competent when users move away from formal written Bangla.

---

### 3. Dialect Robustness

The dialectal evaluation keeps the underlying clinical presentation fixed while varying its linguistic realization.

For example:

```text
Same Clinical Presentation
          │
 ┌────────┼─────────┐
 ▼        ▼         ▼
Sylheti  Chittagonian  Rangpuri
```

This isolates the effect of dialectal variation from differences in medical content.

---

## Models Evaluated

We benchmark models across four categories:

### Proprietary Models

- `TODO: Model`
- `TODO: Model`
- `TODO: Model`

### Open-Weight Models

- `TODO: Model`
- `TODO: Model`
- `TODO: Model`

### Indic-Centric Models

- `TODO: Model`
- `TODO: Model`

### Medical-Specialised Models

- `TODO: Model`
- `TODO: Model`

The exact model versions, inference configurations, prompts, and decoding parameters are provided in the evaluation configuration files.

---

## Evaluation Protocol

Unless otherwise specified, models are evaluated using a multiple-choice question-answering setup.

We report:

- Overall accuracy
- Domain-level accuracy
- Bangla vs. English accuracy
- Register-level accuracy
- Dialect-level accuracy
- Performance degradation relative to formal Bangla
- Performance degradation relative to English
- Tokenisation statistics
- Accuracy–tokenisation relationships

For reproducibility, we release the complete prompts and raw model outputs.

---

## Tokenisation Analysis

BanglaMedBench additionally investigates whether subword tokenisation contributes to performance degradation.

For each model, we measure the tokenisation cost of equivalent content across languages and linguistic conditions.

We investigate the relationship between:

```text
Bangla Tokenisation Cost
            │
            ▼
   Linguistic Representation
            │
            ▼
     Medical Accuracy
```

This analysis helps determine whether performance degradation is associated with the way models represent Bangla text at the token level.

---

## Key Findings

> **TODO: Replace this section with the final headline findings after experiments are complete.**

Our experiments show that:

- `TODO: Main finding`
- `TODO: Bangla vs. English finding`
- `TODO: Code-mixing finding`
- `TODO: Dialect finding`
- `TODO: Tokenisation finding`
- `TODO: Model-family finding`

Overall, the results suggest that medical competence measured on standard English or formal Bangla does not necessarily translate into robust performance across the linguistic diversity encountered in Bangla-speaking clinical settings.

---

## Repository Structure

```text
BanglaMedBench/
│
├── README.md
│
├── data/
│   ├── main/
│   │   └── banglamedbench_main.jsonl
│   │
│   ├── english_parallel/
│   │   └── english_parallel.jsonl
│   │
│   ├── register/
│   │   ├── formal_bangla.jsonl
│   │   ├── code_mixed.jsonl
│   │   └── romanised_bangla.jsonl
│   │
│   └── dialect/
│       ├── sylheti.jsonl
│       ├── chittagonian.jsonl
│       └── rangpuri.jsonl
│
├── evaluation/
│   ├── prompts/
│   ├── configs/
│   ├── scripts/
│   └── evaluate.py
│
├── analysis/
│   ├── accuracy/
│   ├── tokenisation/
│   ├── dialect/
│   └── visualisation/
│
├── outputs/
│   ├── predictions/
│   └── aggregate_results/
│
├── examples/
│   └── example_questions.jsonl
│
├── LICENSE
├── CITATION.cff
└── requirements.txt
```

---

## Quick Start

### Clone the repository

```bash
git clone https://github.com/TODO/BanglaMedBench.git
cd BanglaMedBench
```

### Install dependencies

```bash
pip install -r requirements.txt
```

### Load the dataset

```python
import json

with open(
    "data/main/banglamedbench_main.jsonl",
    "r",
    encoding="utf-8"
) as f:
    examples = [json.loads(line) for line in f]

print(f"Number of examples: {len(examples)}")
print(examples[0])
```

### Run evaluation

```bash
python evaluation/evaluate.py \
    --data data/main/banglamedbench_main.jsonl \
    --model TODO \
    --output outputs/predictions/
```

### Run register evaluation

```bash
python evaluation/evaluate.py \
    --data data/register/code_mixed.jsonl \
    --model TODO \
    --output outputs/predictions/code_mixed/
```

---

## Example Item

### Formal Bangla

```text
প্রশ্ন:
TODO: Example medical question in Bangla.

A. উত্তর ১
B. উত্তর ২
C. উত্তর ৩
D. উত্তর ৪
```

**Correct answer:** `B`

### Code-Mixed Version

```text
TODO: Example naturally code-mixed clinical Bangla question.
```

### Romanised Version

```text
TODO: Example romanised Bangla question.
```

### Dialectal Version

```text
TODO: Example dialectal patient narrative.
```

The underlying clinical information remains matched across variants wherever possible.

---

## Reproducibility

We aim to make every benchmark result reproducible.

The repository therefore includes:

- Dataset files
- Dataset metadata
- Evaluation prompts
- Model configurations
- Raw model outputs
- Evaluation scripts
- Tokenisation analysis
- Statistical analysis
- Visualization scripts
- Environment specifications

Model-specific restrictions may prevent redistribution of certain model weights or APIs. In such cases, we provide the exact model identifier and inference configuration required to reproduce the evaluation.

---

## Data Splits

The benchmark uses controlled splits to reduce information leakage and enable robust evaluation.

```text
Dataset
│
├── Development / Validation
│
├── Test
│
└── Controlled Evaluation Sets
    ├── English Parallel
    ├── Register
    └── Dialect
```

Exact split sizes and construction procedures are documented in the dataset card.

---

## Intended Use

BanglaMedBench is intended for:

- Medical NLP research
- Multilingual language-model evaluation
- Bangla NLP research
- Medical question answering
- Cross-lingual evaluation
- Low-resource language research
- Dialect robustness research
- Code-mixed language evaluation
- Analysis of language-model tokenisation
- Benchmarking medical language models

The benchmark is primarily a **research and evaluation resource**.

---

## Out-of-Scope Use

BanglaMedBench should **not** be used as:

- A clinical diagnostic system
- A substitute for professional medical advice
- A medical certification examination
- A tool for making decisions about individual patients
- Evidence that a model is safe for deployment in healthcare

Performance on this benchmark does not establish clinical safety, reliability, or suitability for real-world medical decision-making.

---

## Ethical Considerations

BanglaMedBench is designed to evaluate language-model capabilities rather than individual patients.

The benchmark does not contain personally identifiable patient information.

Because medical language can involve sensitive clinical concepts, researchers should avoid interpreting benchmark performance as evidence of clinical competence in real-world settings.

Particular care is also required when interpreting dialect-level results. Lower performance on a dialect should not be interpreted as a deficit of the speakers of that dialect; it reflects limitations in the evaluated models and their training or representation of that linguistic variety.

---

## Limitations

BanglaMedBench has several limitations.

### Linguistic Coverage

Bangla is highly diverse across geographic, social, and communicative contexts. The benchmark currently focuses on selected registers and three dialectal varieties and therefore cannot represent the full linguistic diversity of Bangla.

### Clinical Coverage

Although the benchmark covers multiple clinical and preclinical domains, it cannot represent the full breadth of medical knowledge or clinical decision-making.

### Multiple-Choice Format

Multiple-choice questions provide a controlled evaluation setting but do not capture all aspects of real clinical communication, such as history taking, dialogue, uncertainty management, or longitudinal reasoning.

### Expert Authorship

Expert-authored questions provide important quality control but may still reflect the assumptions and perspectives of the authors.

### Tokenisation

Tokenisation cost is only one possible explanation for differences in model performance. Other factors, including pretraining data, instruction tuning, multilingual representation, model architecture, and alignment, may also contribute.

---

## Citation

If you use BanglaMedBench in your research, please cite:

```bibtex
@misc{banglamedbench2026,
  title        = {BanglaMedBench: A Native Bangla Benchmark for Medical Language Models},
  author       = {TODO},
  year         = {2026},
  howpublished = {\url{https://github.com/TODO/BanglaMedBench}},
  note         = {Benchmark and evaluation framework for Bangla medical NLP}
}
```

---

## License

The dataset, code, and annotations are released under:

**TODO: License**

Please check the individual data-source terms where applicable.

---

## Contact

For questions, dataset issues, or collaboration inquiries:

**Author:** TODO  
**Email:** TODO  
**Repository:** TODO

---

## Acknowledgements

We thank the medical-domain experts, annotators, language contributors, and researchers who contributed to the construction and evaluation of BanglaMedBench.

We also acknowledge the broader Bangla NLP and multilingual NLP research communities whose work motivated this benchmark.

---

## Project Status

🚧 **Research Preview**

BanglaMedBench is currently under active development.

The following components will be updated as the project progresses:

- [ ] Final dataset statistics
- [ ] Final domain taxonomy
- [ ] Expert annotation documentation
- [ ] Benchmark test set
- [ ] Model evaluation results
- [ ] Tokenisation analysis
- [ ] Dialect analysis
- [ ] Data license
- [ ] Dataset card
- [ ] Reproducibility package
- [ ] Paper preprint

**Current version:** `v0.1.0`