## Chapter 5: ML Lifecycle, Evaluation Metrics, and Deep Learning Intuition — Practice Questions

**Q1.** A customer support team wants to answer 'what is your return policy?' style questions using a fixed set of 50 known FAQ topics. Response text never changes and must be 100% accurate and auditable. Which approach BEST fits this requirement?

A) Fine-tune a large language model on the FAQ dataset
B) Train a supervised classification model with embeddings and a neural network
C) Build a rule-based system with keyword/intent matching to the 50 fixed answers
D) Deploy a general-purpose LLM with retrieval-augmented generation (RAG)

<details>
<summary>Answer</summary>

**Correct: C**

Fixed, small, unchanging answer set with a hard requirement for 100% accuracy and auditability is the textbook case for a rule-based/deterministic system — no training data drift, no hallucination risk, fully traceable logic.

**Why the others are wrong:**
- Fine-tuning an LLM adds cost, latency, and non-deterministic output risk for a problem that doesn't need generative flexibility.
- A trained classifier still has non-zero error rate and needs retraining/monitoring — overkill and less accurate than deterministic matching for exactly 50 fixed answers.
- RAG is for open-ended, frequently changing knowledge bases — introduces hallucination risk the requirement explicitly forbids.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A fraud detection model flags transactions as fraudulent (positive class). Only 0.5% of transactions are actually fraudulent. The team wants to minimize missed fraud cases even if it means more false alarms. Which metric should be prioritized when tuning the decision threshold?

A) Accuracy
B) Precision
C) R-squared
D) Recall

<details>
<summary>Answer</summary>

**Correct: D**

Recall = TP/(TP+FN) measures how many actual fraud cases were caught. Minimizing missed fraud (false negatives) directly maps to maximizing recall, even at the cost of precision.

**Why the others are wrong:**
- Accuracy is misleading on a 0.5% imbalanced dataset — predicting 'not fraud' for everything gives 99.5% accuracy while catching zero fraud.
- Precision measures false alarm rate (TP/(TP+FP)) — optimizing this would reduce false alarms but increase missed fraud, the opposite of the stated goal.
- R-squared is a regression metric and does not apply to a classification problem.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A regression model predicting house prices has a few extreme outlier listings (mansions worth 50x the median). The team wants an error metric that is less sensitive to these outliers when reporting typical model performance. Which metric should they choose?

A) RMSE (Root Mean Squared Error)
B) R-squared
C) Log loss
D) MAE (Mean Absolute Error)

<details>
<summary>Answer</summary>

**Correct: D**

MAE averages absolute errors linearly, so outliers contribute proportionally rather than being squared — making it far less sensitive to extreme values than RMSE.

**Why the others are wrong:**
- RMSE squares errors before averaging, so large outlier errors are amplified disproportionately — the opposite of what's wanted here.
- R-squared measures variance explained overall but is also heavily distorted by outliers and doesn't report 'typical' error magnitude in interpretable units.
- Log loss is a classification metric for probabilistic predictions, not applicable to a price regression problem.

</details>

---

**Q4.** A data science team retrains a fraud model weekly. Six months later, no one can reproduce the exact model that is currently in production because the training data snapshot, hyperparameters, and library versions used at the time were never recorded. Which practice would have PREVENTED this problem?

A) Using a larger training dataset each time
B) Increasing the number of cross-validation folds
C) Switching from a rule-based system to a supervised model
D) Logging experiments with MLflow or Weights & Biases, capturing data version, hyperparameters, code commit, and environment for every run

<details>
<summary>Answer</summary>

**Correct: D**

Experiment tracking tools log the exact combination of data version, code, hyperparameters, and environment per run, enabling exact reproduction of any past model — this directly solves the stated problem.

**Why the others are wrong:**
- Dataset size has nothing to do with reproducibility of a specific past run.
- Cross-validation fold count affects evaluation robustness during training, not the ability to reconstruct a historical model artifact.
- Switching model paradigms doesn't address the tracking/versioning gap; the same reproducibility problem would recur.

</details>

---

**Q5.** A small team of two data scientists wants a lightweight, open-source tool primarily to log and compare experiment runs and package models for deployment, without needing a hosted collaborative dashboard for a large distributed team. Which tool is the more natural fit as described?

A) Weights & Biases
B) Apache Airflow
C) MLflow
D) Kubernetes

<details>
<summary>Answer</summary>

**Correct: C**

MLflow is open-source, can run fully self-hosted/local, and its core strengths are experiment tracking, model packaging (MLflow Models), and a model registry — matching a small team's lightweight needs.

**Why the others are wrong:**
- Weights & Biases is optimized for hosted, collaborative dashboards and visualization at scale for larger teams — heavier than needed here and typically a paid hosted service for teams.
- Apache Airflow is a workflow/pipeline orchestration tool, not an experiment tracking tool.
- Kubernetes is a container orchestration platform for deployment infrastructure, unrelated to experiment tracking.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** A team needs an image classifier for a niche medical imaging task but has only 800 labeled images — far too few to train a CNN from scratch. Which approach BEST addresses this constraint?

A) Train a deep CNN from random initialization on the 800 images
B) Use a rule-based image thresholding system instead
C) Use transfer learning: start from a pretrained CNN (e.g., trained on ImageNet) and fine-tune the final layers on the 800 images
D) Increase the learning rate significantly to speed up convergence on the small dataset

<details>
<summary>Answer</summary>

**Correct: C**

Transfer learning reuses feature representations learned from large datasets, requiring far fewer labeled examples to fine-tune for a new, related task — the standard solution to small-data deep learning problems.

**Why the others are wrong:**
- Training a deep CNN from scratch on 800 images will severely overfit due to insufficient data.
- Rule-based thresholding cannot capture the complex visual patterns needed for medical image classification.
- Increasing learning rate does not solve a data scarcity problem and can cause training instability.

</details>

---

**Q7.** A team is tuning hyperparameters for a model on a dataset with only 300 samples. Standard 5-fold cross-validation is showing high variance in performance across folds. Which adjustment is the MOST appropriate next step?

A) Reduce k to 2-fold cross-validation to speed up training
B) Abandon cross-validation and evaluate only on the full training set
C) Switch to leave-one-out cross-validation (LOOCV) to use nearly all data for training on each fold
D) Increase the learning rate to reduce variance

<details>
<summary>Answer</summary>

**Correct: C**

With very small datasets, LOOCV maximizes training data per fold (n-1 samples), reducing variance from small validation splits — a well-known exam-tested remedy for high-variance CV on small datasets.

**Why the others are wrong:**
- Reducing k to 2 shrinks the training set per fold further and typically increases bias/variance issues, not reduces them.
- Evaluating only on training data causes severe overfitting bias and gives no honest generalization estimate.
- Learning rate is a training hyperparameter unrelated to cross-validation variance from small sample sizes.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** In the transformer architecture, what is the primary purpose of the self-attention mechanism?

A) It allows the model to weigh the relevance of every other token in the sequence when computing a representation for a given token, regardless of distance
B) It reduces the dimensionality of input embeddings before classification
C) It replaces the need for tokenization entirely
D) It compresses the model to run efficiently on CPUs without GPUs

<details>
<summary>Answer</summary>

**Correct: A**

Self-attention computes weighted relationships between all token pairs in a sequence in parallel, letting the model capture long-range dependencies without the sequential bottleneck of RNNs — this is the core innovation transformers introduced.

**Why the others are wrong:**
- Dimensionality reduction is not the function of attention; embeddings and projection layers handle representation size separately.
- Tokenization still must occur before any transformer processing — attention operates on token embeddings, not raw text.
- Attention does not inherently make models CPU-efficient; transformers are typically compute/GPU-intensive due to attention's quadratic cost in sequence length.

</details>

---

