# Smoking Cessation Social Media Sentiment Analysis

**Author: Swapnik Hazari**

An NLP and machine learning project examining sentiment patterns in public social-media discussions related to smoking cessation.

## Project Overview

Smoking cessation is a major public-health priority because tobacco use is associated with substantial respiratory and chronic-disease burden. Public social-media discussions provide an opportunity to examine how people communicate about quitting smoking, health concerns, support, challenges, and cessation strategies.

This project applies natural language processing (NLP), exploratory data analysis, and supervised machine learning to characterize sentiment and linguistic patterns in smoking-cessation-related social-media content.

### Research Question

**How can NLP methods characterize sentiment and recurring themes in public smoking-cessation discussions, with particular attention to respiratory-health relevance, engagement patterns, and methodological limitations?**

## Dataset

The final analytical sample contains **10,000 social-media posts** selected from a substantially larger smoking-related source dataset using stratified sampling.

| Sentiment | Posts | Percentage |
|---|---:|---:|
| Positive | 4,945 | 49.45% |
| Neutral | 2,626 | 26.26% |
| Negative | 2,429 | 24.29% |
| **Total** | **10,000** | **100.00%** |

A fixed random seed (`42`) was used during sample construction to support reproducibility while preserving the source sentiment distribution.

To protect privacy and respect data-distribution restrictions, this repository does **not** redistribute the original source dataset, raw social-media identifiers, usernames, URLs, conversation identifiers, or other direct identifiers.

## Analytical Workflow

The project follows an end-to-end NLP and machine-learning workflow:

1. Stratified sample construction
2. Data-quality validation
3. Data preparation
4. Exploratory data analysis
5. Sentiment distribution and temporal analysis
6. Engagement analysis
7. Text and term-frequency analysis
8. TF-IDF feature engineering
9. Logistic Regression classification
10. Multinomial Naive Bayes classification
11. Model comparison
12. Error analysis
13. Logistic Regression feature interpretation
14. Exploratory public-health contextual analysis
15. Limitations and responsible interpretation

## Exploratory Findings

Positive sentiment represented **49.45%** of the analytical sample, followed by neutral (**26.26%**) and negative (**24.29%**) content.

Engagement distributions were highly right-skewed, with many observations receiving no engagement. Negative-sentiment posts showed higher observed mean engagement across replies, reposts, likes, and quotes in this analytical sample.

These findings represent **descriptive associations** and should not be interpreted as evidence that sentiment caused differences in engagement.

After removing dominant smoking-cessation query terms and a text-processing artifact, frequently observed informative terms included `cigarette`, `help`, `day`, `like`, `try`, `want`, `people`, `need`, `good`, `stop`, `vaping`, and `tobacco`.

## Machine Learning

Post text was represented using **TF-IDF features** containing unigrams and bigrams. English stop words were removed, very rare terms were excluded, and sublinear term-frequency scaling was applied.

The final training TF-IDF matrix contained **5,125 features**.

The data were divided into an **80% training set (8,000 observations)** and a **20% held-out test set (2,000 observations)** using stratified sampling.

Two supervised classifiers were evaluated:

| Model | Accuracy | Macro Precision | Macro Recall | Macro F1 | Weighted F1 |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | **0.6845** | 0.6640 | **0.6796** | **0.6673** | **0.6886** |
| Multinomial Naive Bayes | 0.6550 | **0.6725** | 0.5845 | 0.6031 | 0.6363 |

Logistic Regression produced higher overall accuracy, macro recall, macro F1, and weighted F1 on the held-out test set. Multinomial Naive Bayes produced slightly higher macro precision.

> **Evaluation note:** The classifiers were evaluated against the existing sentiment labels contained in the dataset. These results therefore represent agreement with the dataset's labeling framework rather than accuracy against independently adjudicated human sentiment.

## Logistic Regression Performance

Class-specific Logistic Regression performance was:

| Sentiment | Precision | Recall | F1-score |
|---|---:|---:|---:|
| Negative | 0.5793 | 0.6091 | 0.5938 |
| Neutral | 0.5911 | 0.7352 | 0.6553 |
| Positive | 0.8218 | 0.6946 | 0.7529 |

The classifier correctly predicted **1,369 of 2,000** held-out observations, corresponding to **68.45% accuracy**.

The positive class achieved the highest F1-score, while performance on negative and neutral observations demonstrated the greater difficulty of distinguishing those categories using TF-IDF features.

## Error Analysis

Logistic Regression produced **631 model-label disagreements** on the held-out test set.

The observed misclassification patterns were:

| Existing Label | Predicted Negative | Predicted Neutral | Predicted Positive |
|---|---:|---:|---:|
| Negative | — | 101 | 89 |
| Neutral | 79 | — | 60 |
| Positive | 136 | 166 | — |

The largest individual disagreement pattern was **positive → neutral (166 observations)**, followed by **positive → negative (136 observations)**.

Social-media language presents several challenges for conventional NLP models, including slang, profanity, humor, contextual ambiguity, short messages, and mixed sentiment. In addition, apparent classification errors may reflect noise or ambiguity in the existing reference labels.

For this reason, these cases are interpreted as **model-label disagreements rather than definitive model errors**.

## Model Interpretability

Logistic Regression coefficients were examined to identify textual features that provided relatively strong predictive evidence for each sentiment class.

### Negative-associated features

Examples included:

`bad`, `shit`, `stop`, `cancer`, `fuck`, `kill`, `lung_cancer`, `die`, `hate`, `death`, `stress`, `difficult`, `hard`, and `risk`

### Positive-associated features

Examples included:

`help`, `free`, `love`, `good`, `like`, `great`, `support`, `happy`, `care`, `healthy`, `hope`, `success`, and `proud`

### Neutral-associated features

Examples included:

`quitsmoking`, `smoking`, `smoke`, `hypnosis`, `quit smoking`, `weed`, `cessation`, and `gum`

The learned coefficients show substantively interpretable patterns. Negative classifications were associated with adverse health outcomes, risk, difficulty, and negative affect, whereas positive classifications were associated with support, encouragement, health, hope, and success.

Neutral classifications were more strongly associated with descriptive or topic-oriented smoking-cessation terminology.

These coefficients represent **predictive associations learned from the training data** and should not be interpreted as causal relationships or general measures of word importance.

## Public-Health Context

Several model-associated terms—including `cancer`, `lung_cancer`, `risk`, `healthy`, `care`, `help`, and `support`—illustrate how smoking-cessation conversations intersect with respiratory health, disease risk, behavioral support, and preventive-health communication.

An exploratory analysis was also conducted using an existing COVID-related indicator.

Only **134 observations (1.34%)** of the analytical sample were identified as COVID-related.

| COVID Indicator | Positive | Neutral | Negative |
|---|---:|---:|---:|
| Not COVID-related | 49.19% | 26.51% | 24.31% |
| COVID-related | 68.66% | 8.21% | 23.13% |

The COVID-related subgroup showed a higher proportion of positive sentiment and a lower proportion of neutral sentiment within this analytical sample.

Because the subgroup is small and the data are observational, these comparisons are **exploratory and descriptive only**. They should not be interpreted as population-level or causal effects.

## Ethics and Data Governance

Social-media research requires careful consideration of privacy, platform policies, data governance, and the potential identifiability of individual users.

This repository therefore emphasizes analytical methods and aggregate results rather than redistribution of raw social-media records.

Raw social-media identifiers and source records are not distributed through the repository.

No conclusions about an individual user's health status, smoking behavior, treatment history, or clinical condition should be inferred from this analysis.

## Limitations

Several limitations should be considered when interpreting the results:

- The classifiers were evaluated against existing sentiment labels rather than independently adjudicated human annotations.
- The 10,000-record analytical sample may not capture every linguistic or temporal pattern contained in the substantially larger source dataset.
- TF-IDF does not fully capture contextual meaning, sarcasm, emojis, mixed sentiment, or complex linguistic relationships.
- Some residual text-processing artifacts, including features containing `amp`, remained in the modeling vocabulary.
- Informal social-media language, slang, profanity, humor, and context-dependent expressions can complicate sentiment classification.
- Engagement metrics were highly right-skewed, with many posts receiving no engagement.
- Observed relationships between sentiment and engagement are descriptive and should not be interpreted causally.
- Social-media users are not necessarily representative of the broader population of people who smoke or attempt smoking cessation.
- The COVID-related subgroup contained only 134 observations and should therefore be interpreted cautiously.
- Platform-specific and temporal effects may influence the observed language patterns.

## Technologies

- Python
- pandas
- NumPy
- scikit-learn
- TF-IDF
- Logistic Regression
- Multinomial Naive Bayes
- Matplotlib
- ijson
- Jupyter Notebook

## Repository Structure

```text
smoking-cessation-sentiment-analysis/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   └── README.md
└── notebooks/
    └── 01_smoking_cessation_sentiment_analysis.ipynb
```

Additional source-code and output directories can be added as the project is extended.

## Future Work

Potential extensions include:

- Human annotation of a validation subset
- Transformer-based sentiment classification
- Topic modeling
- More extensive temporal analysis
- External validation using additional smoking-cessation datasets
- Improved text normalization and artifact removal
- Comparison of traditional machine-learning methods with contextual language models

## Purpose

This project was developed as a data-science portfolio project exploring the intersection of **natural language processing, machine learning, health informatics, and public-health communication**.

The project emphasizes not only predictive modeling, but also reproducibility, model interpretation, responsible evaluation, and appropriate handling of social-media data.
