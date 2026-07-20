# AI-Driven Phishing Email Detection Using NLP

A comparative study of four machine learning classifiers for phishing email detection using Natural Language Processing features. Built as part of the Summer Internship Program in AI & ML at the **Indian Institute of Computing and Technology (IICT), New Delhi**.

**Author:** Vetry Shaji  
**Enrollment No:** 942476  
**Institution:** Chinmaya Vishwa Vidyapeeth  
**Year:** 2026

---

## Overview

This project implements and compares four supervised machine learning classifiers — **Logistic Regression**, **Multinomial Naive Bayes**, **Random Forest**, and a **feed-forward Neural Network** — on the task of classifying emails as phishing or legitimate. Text is represented using TF-IDF vectorisation with 5,000 unigram-bigram features on a corpus of 82,190 labelled emails aggregated from six benchmark datasets.

## Key Results

| Model | Accuracy | Precision | Recall | F1 Score |
|---|---|---|---|---|
| Logistic Regression | 0.9825 | 0.9807 | 0.9858 | 0.9832 |
| Multinomial Naive Bayes | 0.9536 | 0.9845 | 0.9257 | 0.9542 |
| Random Forest | 0.9807 | 0.9739 | **0.9894** | 0.9816 |
| Neural Network (MLP) | **0.9844** | **0.9864** | 0.9837 | **0.9850** |

**Recommendation:** Random Forest is the recommended model for deployment because it missed only 91 phishing emails out of 8,569 in the test set — 33% fewer than Logistic Regression and 35% fewer than the Neural Network. In a security context where a missed phishing email can cause a real breach, minimising false negatives outweighs marginal gains in overall F1.

## Honest Finding

A critical examination of feature importance revealed that several of the top-ranked features (`enron`, `aug 2008`, `mailing list`) are artefacts of the source datasets rather than genuine phishing indicators. This suggests the model has partly learned to identify the *source* of the email rather than whether it is truly phishing — a form of source leakage inherent to multi-corpus training sets. Cross-domain validation is recommended before real-world deployment.

## Dataset

The dataset used is the publicly available **Phishing Email Dataset** by Naser Abdullah Alam, published on Kaggle (2024). It combines six well-known email corpora:

- Nazario (phishing)
- Enron (legitimate corporate email)
- CEAS 2008 (anti-spam competition)
- Nigerian Fraud (advance-fee scams)
- SpamAssassin (filter testing)
- Ling-Spam (linguist mailing list)

**Download:** https://www.kaggle.com/datasets/naserabdullahalam/phishing-email-dataset

The raw dataset is not included in this repository (~100 MB). Download it from Kaggle and place `phishing_email.csv` in the project root before running the notebook.

## Repository Structure

```
phishing-email-detection-nlp/
├── Phishing_Detection.ipynb          # Main Jupyter notebook
├── Phishing_Report_IEEE_Vetry.docx   # IEEE-format research report
├── Phishing_Detection_Presentation.pptx  # Presentation slides
├── results/
│   ├── model_comparison.png          # Performance bar chart
│   ├── confusion_matrices.png        # Confusion matrices (all 4 models)
│   ├── feature_importance.png        # Top features from Random Forest
│   └── model_comparison_results.csv  # Numeric results table
├── requirements.txt                  # Python dependencies
└── README.md
```

## Tech Stack

- **Python 3.10+**
- **pandas, numpy** — data manipulation
- **scikit-learn** — TF-IDF, classifiers, evaluation metrics
- **nltk** — tokenization, stopwords, lemmatization
- **matplotlib, seaborn** — visualisation
- **Jupyter Notebook** — development environment

## How to Reproduce

1. Clone this repository:
   ```bash
   git clone https://github.com/YOUR_USERNAME/phishing-email-detection-nlp.git
   cd phishing-email-detection-nlp
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Download `phishing_email.csv` from the Kaggle link above and place it in the project root.

4. Open the notebook in Jupyter:
   ```bash
   jupyter notebook Phishing_Detection.ipynb
   ```

5. Run cells top to bottom. Total runtime is approximately 5–10 minutes on a modern laptop, with Random Forest and the Neural Network being the longest steps.

## Methodology

1. **Data Cleaning** — Length filter to remove outliers (20 to 20,000 characters).
2. **Feature Extraction** — TF-IDF vectorisation with 5,000 features and unigram + bigram tokens.
3. **Train-Test Split** — 80/20 stratified sampling.
4. **Model Training** — Four classifiers trained on the identical feature matrix.
5. **Evaluation** — Accuracy, precision, recall, F1 score, and confusion matrices.

## Limitations and Future Work

- **Source leakage** — top features include dataset artefacts; cross-domain evaluation needed.
- **Pre-cleaned text** — URLs, HTML, and punctuation were already stripped, preventing extraction of structural features.
- **Single train-test split** — k-fold cross-validation would provide more robust estimates.
- **No transformer baseline** — fine-tuning DistilBERT would test whether classical ML has hit a ceiling.
- **No live deployment** — a Streamlit web interface is the natural next step.

## References

1. N. A. Alam, "Phishing Email Dataset," Kaggle, 2024. [Online]. Available: https://www.kaggle.com/datasets/naserabdullahalam/phishing-email-dataset
2. F. Pedregosa et al., "Scikit-learn: Machine Learning in Python," *Journal of Machine Learning Research*, vol. 12, pp. 2825–2830, 2011.
3. L. Breiman, "Random forests," *Machine Learning*, vol. 45, no. 1, pp. 5–32, 2001.
4. J. Ramos, "Using TF-IDF to determine word relevance in document queries," in *Proc. First Instructional Conf. Machine Learning*, 2003.

## License

MIT License — see [LICENSE](LICENSE) for details.

## Acknowledgements

Grateful thanks to the Indian Institute of Computing and Technology (IICT) for the internship opportunity, and to Chinmaya Vishwa Vidyapeeth for academic support throughout the program.
