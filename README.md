# Project Proposal Share Package

Project title:

```text
Robustness Evaluation of Toxicity Detection Models under Text Perturbations
```

This folder contains the shareable files requested for the project proposal submission, except for the presentation file. The presentation `.pptx` will be submitted separately.

## What To Submit

Recommended GitHub upload:

| File or folder | Purpose | Upload? |
|---|---|---|
| `README.md` | Overview of this share package | Yes |
| `jigsaw_toxicity_robustness_shareable.zip` | Shareable clean, augmented, and perturbed evaluation datasets | Yes |
| `models_textcnn_core.zip` | Main TextCNN checkpoints and model notes | Yes |
| `training_recipes_results.zip` | Training recipes, scripts, result tables, and figures | Yes |
| `models_tfidf_mlp_optional_large.zip` | Optional TF-IDF/MLP baseline checkpoints | Optional; large |
| `models_shareable/` | Unzipped model documentation and index | Optional if using zip |
| `training_recipes_results/` | Unzipped recipe/result documentation | Optional if using zip |

The optional TF-IDF/MLP model zip is about 193 MB and may exceed normal GitHub file limits. If upload size is limited, do not upload it. The README and result files still describe those baselines.

## 1. Used Dataset

Dataset source:

```text
Jigsaw Unintended Bias in Toxicity Classification
```

Mirror used during this project:

```text
Intuit-GenSRF/jigsaw-unintended-bias
```

Binary label rule:

```text
target >= 0.5 -> toxic
target < 0.5  -> non-toxic
```

Balanced split:

| Split | Non-toxic | Toxic | Total |
|---|---:|---:|---:|
| Train | 5,000 | 5,000 | 10,000 |
| Validation | 1,000 | 1,000 | 2,000 |
| Test | 1,000 | 1,000 | 2,000 |

Dataset package:

```text
jigsaw_toxicity_robustness_shareable.zip
```

Contents:

```text
jigsaw_subset_14k_clean.csv
train_augmented_targeted_100.csv
test_clean_and_perturbed_eval.csv
README.md
manifest.json
column_schema.csv
reproducibility/perturbations.py
```

## 2. Used Models

Main uploaded model package:

```text
models_textcnn_core.zip
```

Included TextCNN checkpoints:

| Model | Role |
|---|---|
| `textcnn_clean_longer.pt` | Clean TextCNN baseline |
| `textcnn_aug_25_general.pt` | 25% general perturbation augmentation |
| `textcnn_aug_100_targeted.pt` | Final targeted robustness defense |

SOTA-style reference model:

```text
unitary/unbiased-toxic-roberta
https://huggingface.co/unitary/unbiased-toxic-roberta
```

This RoBERTa model is public, so the checkpoint is not re-uploaded here.

Optional baseline models:

```text
models_tfidf_mlp_optional_large.zip
```

These contain word-level TF-IDF MLP and character n-gram TF-IDF MLP baselines. They are optional because the zip file is large.

## 3. Training Recipes And Results

Main recipe/results package:

```text
training_recipes_results.zip
```

It contains:

```text
README.md
requirements.txt
reports/*.csv
reports/*.md
figures/*.png
scripts/*.py
```

The README inside that zip explains:

```text
dataset preprocessing
perturbation generation
TextCNN training
TF-IDF/MLP baseline training
RoBERTa reference evaluation
F1 Drop, ASR, and Toxic Recall Drop metrics
main result tables and interpretation
```

## 4. Main Result Summary

Clean F1 comparison:

| Model | Clean F1 |
|---|---:|
| RoBERTa reference | 0.830 |
| TextCNN clean | 0.814 |
| TextCNN targeted augmentation | 0.827 |

Combined perturbation robustness:

| Model | F1 Drop | ASR |
|---|---:|---:|
| RoBERTa reference | 0.117 | 10.8% |
| TextCNN clean | 0.086 | 13.2% |
| TextCNN targeted augmentation | 0.028 | 5.7% |

Toxic-only combined evaluation:

| Model | Clean Toxic Recall | Perturbed Toxic Recall | Recall Drop | ASR / Evasion |
|---|---:|---:|---:|---:|
| RoBERTa reference | 0.718 | 0.566 | 0.152 | 10.8% |
| TextCNN clean | 0.828 | 0.676 | 0.152 | 13.2% |
| TextCNN targeted augmentation | 0.846 | 0.804 | 0.042 | 5.7% |

Main interpretation:

```text
Clean F1 alone is not enough for trustworthy toxicity moderation.
Targeted perturbation augmentation made TextCNN more stable under the tested text-obfuscation threat model.
This does not claim that TextCNN is generally better than RoBERTa.
```

## 5. Reproducibility Notes

The exact scripts used for preprocessing, perturbation, training, and evaluation are included in:

```text
training_recipes_results.zip
```

The exported dataset also includes the perturbation code used to generate shareable perturbed examples.

Recommended citation note for the report or GitHub README:

```text
This project uses a balanced subset derived from the Jigsaw Unintended Bias in Toxicity Classification dataset and evaluates robustness under rule-based text perturbations.
```
