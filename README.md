# NLP notebooks

Small NLP experiments. At the moment there is one notebook.

## Spam detection with TF-IDF and a random forest

[`Spam_mail.ipynb`](Spam_mail.ipynb) classifies messages as spam or ham.

**Method**

1. Split the data 80/20 into train and test (`random_state=42`)
2. Turn each message into a TF-IDF vector, fitted on the training split only
3. Train a `RandomForestClassifier` with 100 trees

**Result on the test split (1,115 messages)**

| Class | Precision | Recall | F1 | Messages |
|---|---|---|---|---|
| ham | 0.97 | 1.00 | 0.99 | 958 |
| spam | 1.00 | 0.84 | 0.91 | 157 |

Accuracy is 0.978. The more useful reading is per class: no legitimate message was flagged as spam, and 16% of the spam got through. Accuracy alone hides that, because only 14% of the test messages are spam.

**Running it**

The notebook was written in Google Colab and reads `/content/email.csv`, a table with the columns `Category` (ham or spam) and `Message`. The data file is not part of this repository. Upload it to Colab, or change the path in the cell that loads the data.

Requirements: `pandas`, `scikit-learn`.

**Possible next steps**

- A linear model (logistic regression or a linear SVM) as a baseline, which is usually strong on TF-IDF features
- Class weights or a lower decision threshold to raise spam recall
- Cross-validation in place of a single split
