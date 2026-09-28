# Smoking Cessation Social Media Sentiment Analysis

An NLP and machine learning project examining sentiment patterns in public social-media discussions related to smoking cessation.

## Project Overview

Smoking cessation is a major public-health priority, particularly because tobacco use is associated with substantial respiratory and chronic-disease burden. Social-media discussions provide an opportunity to examine how people communicate about quitting smoking, health concerns, support, challenges, and cessation strategies.

This project applies natural language processing (NLP), exploratory data analysis, and supervised machine learning to characterize sentiment in smoking-cessation-related social-media content.

### Research Question

**How can NLP methods characterize sentiment and recurring themes in public smoking-cessation discussions, with particular attention to respiratory-health relevance, engagement patterns, and methodological limitations?**

## Dataset

The analytical sample contains **9,998 social-media posts** selected from a larger smoking-related dataset.

Sentiment distribution:

| Sentiment | Posts | Percentage |
|---|---:|---:|
| Positive | 4,944 | 49.45% |
| Neutral | 2,625 | 26.26% |
| Negative | 2,429 | 24.30% |
| **Total** | **9,998** | **100%** |

To protect privacy and respect data-distribution restrictions, the public repository does not redistribute raw social-media identifiers or the original source dataset.

## Analytical Workflow

The project follows an end-to-end NLP workflow:

1. Data validation and cleaning
2. Exploratory data analysis
3. Sentiment distribution analysis
4. Engagement analysis
5. Text preprocessing and lemmatization
6. Term-frequency analysis
7. TF-IDF feature engineering
8. Logistic Regression classification
9. Multinomial Naive Bayes classification
10. Precision, recall, F1-score, and confusion-matrix evaluation
11. Misclassification/error analysis
12. Logistic Regression feature interpretation
13. Exploratory public-health contextual analysis

## Exploratory Findings

Positive sentiment represented approximately **49.45%** of the analytical sample, followed by neutral (**26.26%**) and negative (**24.30%**) content.

Engagement distributions were highly right-skewed. Negative-sentiment posts showed higher observed mean engagement on several measures, including replies and likes. These results represent descriptive associations and should not be interpreted as evidence that sentiment caused differences in engagement.

After removing dominant smoking-cessation query terms, frequently observed terms included `cigarette`, `help`, `try`, `want`, `people`, `need`, `good`, `stop`, `vaping`, `tobacco`, and related concepts.

## Machine Learning

Text was represented using **TF-IDF features**, including unigrams and bigrams. The final TF-IDF representation contained **5,097 features**.

Two supervised classifiers were evaluated:

| Model | Accuracy | Macro F1 | Weighted F1 |
|---|---:|---:|---:|
| Logistic Regression | **0.6880** | **0.6704** | **0.6915** |
| Multinomial Naive Bayes | 0.6625 | 0.6112 | 0.6438 |

Logistic Regression achieved higher accuracy and F1 scores on the held-out test set.

The classifiers were evaluated against the **existing sentiment labels contained in the dataset**. These results should therefore be interpreted as agreement with the dataset's labeling framework rather than accuracy against independently adjudicated human sentiment.

## Logistic Regression Performance

Class-specific Logistic Regression performance:

| Sentiment | Precision | Recall | F1-score |
|---|---:|---:|---:|
| Negative | 0.5802 | 0.6029 | 0.5913 |
| Neutral | 0.6019 | 0.7429 | 0.6650 |
| Positive | 0.8182 | 0.7007 | 0.7549 |

The model correctly classified **1,376 of 2,000 test observations**.

Error analysis identified **624 misclassifications**. Positive-to-neutral and positive-to-negative errors were the most frequent error patterns.

## Model Interpretability

Logistic Regression coefficients were examined to identify textual features associated with each predicted sentiment class.

### Negative-associated features

Examples included:

`bad`, `cancer`, `lung_cancer`, `stop`, `kill`, `die`, `death`, `stress`, `risk`, `struggle`

### Positive-associated features

Examples included:

`free`, `help`, `love`, `good`, `support`, `great`, `healthy`, `care`, `hope`, `success`

### Neutral-associated features

Examples included:

`quitsmoking`, `smoking`, `smoke`, `hypnosis`, `weed`, `gum`, `vape`, `cessation`

The results suggest that the classifier learned semantically plausible distinctions. Negative classifications were associated with adverse health outcomes, difficulty, and negative affect, whereas positive classifications were associated with support, encouragement, health, and successful cessation language.

These coefficients describe statistical associations learned by the model and should not be interpreted as causal effects.

## Public-Health Context

Several model-associated terms—including `cancer`, `lung_cancer`, `risk`, `healthy`, `care`, and `support`—illustrate how smoking-cessation conversations intersect with respiratory health, disease risk, behavioral support, and preventive health communication.

An exploratory comparison was also conducted using an existing COVID-related indicator. Only **134 posts (1.34%)** were COVID-flagged, so this analysis should be interpreted cautiously.

| COVID indicator | Positive | Neutral | Negative |
|---|---:|---:|---:|
| No | 49.19% | 26.50% | 24.31% |
| Yes | 68.66% | 8.21% | 23.13% |

Because of the small COVID-related subset and the observational nature of the data, these differences are descriptive only.

## Error Analysis

Social-media language creates several NLP challenges, including:

- sarcasm and humor
- emojis
- ambiguous wording
- short or context-poor posts
- slang
- mixed sentiment
- health terminology with strong emotional connotations

Manual examination of misclassified observations demonstrated that these contextual features can produce disagreements between the TF-IDF classifier and the dataset's existing labels.

## Ethics and Data Governance

Social-media research requires careful consideration of privacy, consent, platform policies, and the potential identifiability of users.

This repository therefore emphasizes aggregate results and analytical code rather than redistribution of raw social-media content or user identifiers.

No conclusions about individual users' health status, smoking behavior, or clinical condition should be inferred from the analysis.

## Limitations

Key limitations include:

- The sample may not represent the broader population of people who smoke or attempt smoking cessation.
- Social-media users are not representative of all demographic groups.
- Existing sentiment labels are not treated as independently validated human ground truth.
- Sarcasm, humor, emojis, slang, and contextual language remain challenging for TF-IDF-based models.
- Engagement metrics are highly right-skewed.
- Observed associations should not be interpreted causally.
- The COVID-related subset is small.
- Platform-specific and temporal effects may influence observed language patterns.

## Technologies

- Python
- pandas
- NumPy
- scikit-learn
- TF-IDF
- Logistic Regression
- Multinomial Naive Bayes
- Matplotlib
- NLP text preprocessing
- Jupyter Notebook

## Repository Structure

```text
smoking-cessation-sentiment-analysis/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── data/
│   └── README.md
│
├── notebooks/
│   ├── 01_data_cleaning_eda.ipynb
│   ├── 02_sentiment_analysis.ipynb
│   └── 03_machine_learning.ipynb
│
├── src/
│   ├── preprocessing.py
│   └── modeling.py
│
└── outputs/
    ├── figures/
    └── model_results/
```

## Future Work

Potential extensions include human annotation of a validation subset, transformer-based sentiment classification, more extensive temporal modeling, topic modeling, and external validation using additional smoking-cessation datasets.

## Purpose

This project was developed as a data-science portfolio project exploring the intersection of **NLP, machine learning, health informatics, and public-health communication**.# smoking-cessation-sentiment-analysis
NLP and machine learning analysis of sentiment patterns in public smoking-cessation discussions.
