# SMS Spam Classification

A machine learning project to classify SMS messages as **Spam** or **Ham** using NLP techniques. The project explores multiple vectorization and classification approaches to find the most accurate and reliable pipeline for spam detection.

---

## Problem Statement

The goal is to build a model that can detect spam messages based on the text content of SMS data. Spam messages often contain certain patterns, keywords, and formatting that differentiate them from legitimate (ham) messages. The challenge lies in capturing those patterns effectively through preprocessing and modeling.

---

## Dataset

The original dataset contains **5,572 SMS messages** labeled as either `"ham"` or `"spam"`. Each message is stored in two columns:
- `v1`: The label (`ham` or `spam`)
- `v2`: The message content

To improve the class balance and enhance the spam detection performance, an additional set of **24 spam messages** was generated and appended to the training data. These new spam samples were designed to mimic real-world scam messages and helped stabilize class distribution.

---

## Preprocessing Steps

1. Removed duplicates and unnecessary columns
2. Lowercased the text and removed punctuation
3. Tokenized and removed stopwords
4. Performed stemming using the Porter Stemmer
5. Engineered a few simple features (message length, word count)

---

## Vectorization

Three different vectorizers were tested:
- CountVectorizer
- TfidfVectorizer
- HashingVectorizer (removed later)

**Issue Faced**: While experimenting with `HashingVectorizer`, the training time significantly increased (over 10 minutes), and interpretability decreased since it does not preserve feature names. This made it harder to analyze word importance and model behavior. The vectorizer was eventually removed from the pipeline.

---

## Models Tried

The following classifiers were evaluated with different vectorizers:
- Logistic Regression
- Multinomial Naive Bayes
- Bernoulli Naive Bayes
- Random Forest
- SVM (LinearSVC)
- SGDClassifier
- Decision Tree

Each combination was evaluated using accuracy score, and the best performing pipeline was selected based on test set results.

---

## Best Model

- Classifier: `SGDClassifier`
- Vectorizer: `CountVectorizer`
- Accuracy: ~98.65%

This model provided the best trade-off between speed and performance, making it ideal for deployment.

---

## Evaluation

A confusion matrix and classification report were generated to analyze false positives and false negatives. The model showed excellent precision and recall for both spam and ham classes.

Additional test messages (unseen data) were also passed through the model to validate its generalization performance.

---

## Files in This Repository

### sms_spam_classifier.ipynb  
The main notebook containing the complete implementation of an SMS spam detection model using machine learning. It includes preprocessing, EDA, feature extraction, model training, evaluation, and improvements with additional synthetic spam messages.

### images/  
EDA plots and evaluation visuals:
- EDA 1: Distribution of Spam vs Ham (`output_image_1.png`)
- EDA 2: Distribution of Message Lengths Ham vs  Spam (`output_image_2.png`)
- EDA 3: Top 10 Classifier-Vectorizer Combinations by Accuracy (`output_image_3.png`)
- EDA 4: Confusion Matrix Heatmap (`output_image_4.png`)
- EDA 5: Classification Report Heatmap (`output_image_5.png`)

### models/  
Serialized components for model reuse and deployment:
- `best_model.pkl`: Best Model
- `best_vectorizer.pkl`: Best Vectorizer
- `preprocess_function.pkl`: Function used to clean and preprocess incoming messages
