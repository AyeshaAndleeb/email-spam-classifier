# Email Spam Classifier

Classifying emails as spam or legitimate from their text, using natural language processing and classical machine learning. Trained and evaluated on more than 83,000 real emails.

![Python](https://img.shields.io/badge/Python-3.10-3776AB?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit__learn-ML-F7931E?logo=scikit-learn&logoColor=white)
![NLP](https://img.shields.io/badge/NLP-TF--IDF-6A4C93)
![F1](https://img.shields.io/badge/F1-98.6%25-2a9d8f)
![License](https://img.shields.io/badge/License-MIT-blue)

## About

Spam is more than a nuisance; it is the main delivery route for phishing and scams. This project trains a model that reads the raw text of an email and decides whether it is spam or ham (legitimate). It walks through the full process end to end: exploring the data, cleaning the text, turning words into TF-IDF features, comparing several models, and explaining what the final model actually learned.

## Results at a glance

The best model was a **Linear SVM**, evaluated on a held-out set of 16,680 emails.

| Metric | Score |
|:-------|:------|
| Accuracy | 98.6% |
| Precision | 98.3% |
| Recall | 99.0% |
| F1 | 98.6% |
| ROC-AUC | 0.998 |

Out of 16,680 test emails it misclassified only 240: 153 real emails flagged as spam, and 87 spam that slipped through.

Full model comparison:

| Model | Accuracy | Precision | Recall | F1 |
|:------|:---------|:----------|:-------|:---|
| Linear SVM (final) | 98.6% | 98.3% | 99.0% | 98.6% |
| Random Forest | 98.5% | 98.3% | 98.9% | 98.6% |
| Logistic Regression | 98.4% | 98.0% | 99.0% | 98.5% |
| Naive Bayes | 96.3% | 96.5% | 96.5% | 96.5% |

## Dataset

| | |
|:--|:--|
| Name | Email Spam Classification Dataset |
| Size | 83,448 emails (about 53% spam, 47% ham) |
| Fields | `text` (the email body), `label` (1 = spam, 0 = ham) |
| Source | [Kaggle](https://www.kaggle.com/datasets/purusinghvi/email-spam-classification-dataset) |

The notebook detects the text and label columns automatically, so it does not break if a column is named differently.

## How it works

1. **Explore** the data: spam vs ham balance, message length, the most common words in each class, and word clouds.
2. **Clean** the text: lowercase, strip URLs, numbers and punctuation, remove stop words, and apply stemming.
3. **Vectorise** with TF-IDF inside a pipeline, so it is fitted on the training data only and never leaks into the test set.
4. **Compare** four models (Naive Bayes, Logistic Regression, Linear SVM, Random Forest) on the same split.
5. **Validate** with stratified 5-fold cross-validation, then tune the best model with grid search.
6. **Explain and save**: inspect the words that most signal spam, review misclassified emails, and export the pipeline so it can score any new email in one call.

## What's in this repo

```
email-spam-detection/
├── email-spam-classifier.ipynb    the full notebook (code, analysis, results)
├── requirements.txt               dependencies
├── README.md
└── spamshield_model.joblib        saved pipeline (created when the notebook runs)
```

## Notes and honest caveats

- Public spam datasets separate cleanly, so ~98% here is expected and higher than a real inbox would see.
- The model reads text only; it ignores the sender, links, HTML and attachments that production filters depend on.
- It is English-only, and spam keeps evolving, so a model trained once needs regular retraining to stay sharp.

In short, this is a strong, interpretable baseline for email text classification rather than a finished production filter.

## Tech stack

Python, pandas, NumPy, scikit-learn, NLTK, TF-IDF, matplotlib, seaborn, wordcloud.

## References

- [Email Spam Classification Dataset, Kaggle](https://www.kaggle.com/datasets/purusinghvi/email-spam-classification-dataset)
- [scikit-learn](https://scikit-learn.org/) and [NLTK](https://www.nltk.org/) documentation

Inspired by my cybersecurity and information security coursework.
