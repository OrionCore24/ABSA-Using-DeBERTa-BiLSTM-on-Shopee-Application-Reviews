# Aspect-Based Sentiment Analysis (ABSA) on Shopee Reviews

This project explores **aspect-based sentiment analysis (ABSA)** for Shopee app reviews collected from the Google Play Store. It combines a fine-tuned DeBERTa model for aspect–sentiment auto-labeling with a BiLSTM classifier trained on the human-verified dataset.

> **Research project:** Undergraduate thesis  
> **Primary language:** Python  
> **Task:** Multi-label aspect-based sentiment analysis

## Project Overview

The workflow uses a public Trustpilot ABSA dataset to fine-tune DeBERTa, then applies the model to Shopee reviews. The automatically generated labels are reviewed by human annotators before being used to train and evaluate the final BiLSTM model.

### Pipeline

1. **Trustpilot dataset preparation**  
   Lightly reformat and preprocess the public annotated Trustpilot ABSA dataset.

2. **DeBERTa fine-tuning**  
   Fine-tune `DeBERTa-v3-small` for joint multi-label aspect–sentiment prediction. The workflow includes threshold tuning and conflict resolution.

3. **Shopee review preprocessing and auto-labeling**  
   Prepare Shopee Google Play Store reviews, translate them into English where needed, and use the fine-tuned DeBERTa model to generate aspect–sentiment labels.

4. **Human verification**  
   Review the auto-generated labels using four annotators, majority voting, and adjudication when needed. The verified data becomes the final dataset for downstream training.

5. **BiLSTM training and evaluation**  
   Train and compare BiLSTM configurations using the verified dataset. Random undersampling is applied to the training split to address class imbalance; validation and test data remain untouched by resampling.

## Aspect Categories

The final aspect setup contains **13 aspects** (Packaging is excluded):

- Information
- Product features
- Item quality
- App experience
- Pricing
- Product availability
- Payment
- Delivered product status
- Shipping
- Return process
- Refund process
- Customer service
- Trust

Each aspect is represented using positive/negative sentiment labels. General review sentiment may be handled separately during the dataset preparation stage, depending on the source dataset.

## Models and Methods

- **DeBERTa-v3-small** — fine-tuned for multi-label aspect–sentiment prediction and used to auto-label Shopee reviews.
- **BiLSTM** — trained on the human-verified Shopee dataset for the final classification task.
- **Threshold tuning and conflict resolution** — used to refine DeBERTa's multi-label predictions.
- **Human annotation** — four annotators, majority voting, and adjudication for disagreements.
- **Random undersampling** — applied only to the training data to reduce class imbalance.
- **Evaluation metrics** — accuracy, precision, recall, F1-score, macro F1-score, and weighted F1-score, as applicable to each phase.

## Evaluation

The following BiLSTM results were recorded in an earlier experiment:

| Metric | Result |
|---|---:|
| Accuracy | 87.43% |
| Macro F1-score | 82.30% |
| Weighted F1-score | 87.51% |
| Negative-class F1-score | 91.83% |
| Positive-class F1-score | 72.76% |

These values should be treated as previously recorded experimental results. Update this section if the final, reproducible evaluation differs.

## Repository Structure

The exact structure depends on the files included in this repository. A possible organization is:

```text
.
├── data/                  # Datasets (omit private/raw data from public repositories)
├── notebooks/             # Data preparation, fine-tuning, labeling, and experiments
├── src/                   # Reusable preprocessing and modeling code
├── outputs/               # Evaluation results and generated artifacts
├── requirements.txt       # Python dependencies
└── README.md
```

Adjust this tree to match the actual repository. Do not commit private datasets, credentials, API keys, virtual environments, model checkpoints, or other large/generated files unless they are intentionally meant to be public.

## Getting Started

### 1. Clone the repository

```bash
git clone <YOUR_REPOSITORY_URL>
cd <YOUR_REPOSITORY_FOLDER>
```

### 2. Create and activate a virtual environment

**Windows (PowerShell):**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**macOS / Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

If the repository includes `requirements.txt`:

```bash
pip install -r requirements.txt
```

Otherwise, install the libraries required by the notebooks and scripts. Exact versions should be documented in the project environment file to support reproducibility.

### 4. Prepare the datasets

Place the required datasets in the paths expected by the notebooks or scripts. Public Trustpilot data and Shopee review data may have separate access and privacy conditions. The private/raw Shopee dataset is not included in this repository unless explicitly stated.

### 5. Run the workflow

Run the notebooks or scripts in the intended order:

1. Trustpilot reformatting and preprocessing
2. DeBERTa fine-tuning and threshold tuning
3. Shopee preprocessing and DeBERTa auto-labeling
4. Human verification and final dataset preparation
5. BiLSTM training and evaluation

Check each notebook's configuration and dataset paths before running it. Training requirements depend on the chosen model configuration and available hardware.

## Data and Reproducibility Notes

- Confirm the original license and terms of use for each dataset before redistribution.
- Do not publish private or sensitive review data without authorization.
- Keep train, validation, and test splits separate. Apply undersampling only to the training set.
- Record random seeds, preprocessing settings, model checkpoints, thresholds, and package versions for reproducibility.
- Results may vary with dataset versions, random seeds, hardware, and training configuration.

## Limitations

- Auto-generated labels can contain errors; human verification is an important part of the workflow.
- Performance may differ across aspects because of class imbalance and variation in the number of examples.
- Translation can change the meaning or sentiment of a review.
- Reported metrics should be interpreted in the context of the split strategy and class distribution.

## Acknowledgements

This project uses a public Trustpilot ABSA dataset as a source for model fine-tuning and Shopee Google Play Store reviews for the target-domain analysis. Please add the dataset's official citation, original source link, and any relevant paper references here.

## Author

**[Your Name]**  
Undergraduate thesis project — Aspect-Based Sentiment Analysis
