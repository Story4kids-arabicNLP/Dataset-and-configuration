# Story4Kids: Culturally Aligned Arabic Children’s Stories

This repository accompanies the paper “Crafting Culturally Aligned Arabic Stories for Children with Large Language Models” (ArabicNLP 2025).
It provides the Story4Kids dataset and training configurations used for generating culturally and morally aligned Arabic children’s stories.

---

## Contents

* `dataset/` → Annotated dataset of 714 Arabic children’s stories

  * Each story includes:

    * Text (in Modern Standard Arabic)
    * Age range label
    * Moral lesson annotation
    * Thematic topic annotation

* `configs/` → Training & evaluation configurations

  * LoRA fine-tuning configs
  * Prompt templates
  * Evaluation settings

* `examples/` → Example generated stories for different age ranges and morals

---

## Dataset Description

* **Size**: 714 stories
* **Language**: Modern Standard Arabic (MSA)
* **Annotations**:

  * **Age range** (e.g., 3–5, 6–8, 9–12)
  * **Moral lesson** (e.g., honesty, generosity, patience)
  * **Thematic topic** (e.g., friendship, courage, respect)

Annotation was carried out by **five Arabic-fluent experts** with 12+ years of formal training.
Inter-annotator agreement (Fleiss’ Kappa, on 100 stories):

* Age range: **0.74** (substantial)
* Moral lessons: **0.71** (substantial)
* Thematic topics: **0.65** (moderate)

Disagreements were resolved by consensus, yielding a gold standard set.

---

## Training Setup

We fine-tuned several LLMs using **Supervised Fine-Tuning (SFT)** with **LoRA**:

1. **Phase 1 – Initial Instruction Tuning**

   * Smaller models (Noon, Jais)
   * Objective: benchmark instruction-following, age alignment, and moral clarity

2. **Phase 2 – Scaling to Gemini 2.0**

   * Larger model (>1T params)
   * Objective: Emphasis on fully Arabic-curated outputs to improve fluency, moral consistency, and prompt adherence

3. **Phase 3 – Final Alignment Tuning**

   * Refinement phase with GPT-4 assisted checkpoint selection
   * Objective: Explicit focus on alignment. Maximize moral coherence, age-appropriateness, and cultural fidelity

---

## Evaluation

We used both **automatic metrics** and **human expert evaluation**:

* **Automatic**: BLEU, Distinct-n, MT-Bench, AlpacaEval, HELENA sentiment match
* **Human**: Expert ratings on:

  * Age appropriateness
  * Fluency & coherence
  * Moral clarity
  * Cultural alignment

---

## Usage

### Load the dataset

```python
import pandas as pd

```

### Run with configs

```bash
# Example: fine-tune with LoRA configs
python train.py --config configs/gemini_lora.yaml
```

---

## Citation

If you use this dataset or configurations, please cite our paper:

```bibtex
@inproceedings{story4kids2025,
  title={Crafting Culturally Aligned Arabic Stories for Children with Large Language Models},
  author={Houssam Eddine Boukhalfa, Selma Mani, Larbi Said Chikh, Mohamed Hadj Ameur, Ahmed Guessom},
  booktitle={ArabicNLP 2025},
  year={2025}
}
```

---

## Contact

For questions, reach out to:
Selma Mani – \[selma.mani@ensia.edu.dz]
Larbi Said Chikh – \[larbi.saidchikh@ensia.edu.dz]
Houssam Eddine Boukhalfa – \[houssam-eddine.boukhalfa@ensia.edu.dz]
Mohamed Hadj Ameur – \[mohamed.hadj.ameur@ensia.edu.dz]
Ahmed Guessom – \[ahmed.guessoum@ensia.edu.dz]
