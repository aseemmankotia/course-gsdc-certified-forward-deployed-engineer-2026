## Chapter 5 Cheat Sheet: ML Lifecycle, Metrics & Deep Learning

### Decision Framework: Rule-Based vs ML vs LLM
| Approach | Best When | Avoid When |
|---|---|---|
| Rule-based | Fixed, small, deterministic outputs; audit/traceability required | Inputs vary widely, patterns hard to enumerate |
| Classic ML | Structured/tabular data, clear labels, interpretability matters | Open-ended language generation needed |
| LLM | Unstructured language, generation, ambiguous/open-ended tasks | Deterministic accuracy or auditability required |

### Learning Paradigms
- **Supervised**: labeled data, predicts known target (classification/regression)
- **Unsupervised**: no labels, finds structure (clustering, dimensionality reduction)
- **Reinforcement**: agent learns via reward/penalty through environment interaction

### Classification Metrics
| Metric | Formula | Use When |
|---|---|---|
| Accuracy | (TP+TN)/Total | Balanced classes only |
| Precision | TP/(TP+FP) | False positives costly |
| Recall | TP/(TP+FN) | False negatives costly (fraud, disease) |
| F1 | 2·P·R/(P+R) | Imbalanced data, need balance |

### Regression Metrics
| Metric | Sensitive to Outliers? | Notes |
|---|---|---|
| MAE | No (linear) | Robust, interpretable in original units |
| RMSE | Yes (squared) | Penalizes large errors heavily |
| R² | Moderate | Variance explained, 0-1 scale |

### Cross-Validation & Tuning
- k=5 or k=10: standard default
- LOOCV (k=n): small datasets, high compute cost
- Grid search: exhaustive, small search space
- Random/Bayesian search: large hyperparameter spaces

### Experiment Tracking: MLflow vs W&B
| Feature | MLflow | Weights & Biases |
|---|---|---|
| Hosting | Self-hosted/open-source | Hosted-first (SaaS) |
| Strength | Model registry, packaging | Visualization, team dashboards |
| Best fit | Small teams, lightweight | Larger teams, rich collaboration |

### Reproducibility Checklist
Log per run: data version, code commit hash, hyperparameters, environment/library versions, model artifact + version tag.

### Deep Learning / NLP Glossary
- **CNN**: convolutional layers extract spatial features (images)
- **Transfer learning**: fine-tune pretrained model on small task-specific data
- **Tokenization**: text → subword tokens (BPE, WordPiece) before embedding
- **Embeddings**: dense vectors capturing semantic similarity
- **Attention**: weighs relevance of all tokens to each other, enables long-range context
- **Transformer**: architecture built on self-attention, replaced RNNs for most NLP tasks
- **HuggingFace**: library/hub providing pretrained transformer models and tokenizers

### Common Exam Traps
1. Choosing accuracy on imbalanced datasets (wrong — use precision/recall/F1)
2. Picking LLM/fine-tuning when a simple rule-based system suffices
3. Confusing MAE (robust) vs RMSE (outlier-sensitive)
4. Forgetting that reproducibility requires versioning data AND code AND environment, not just the model file
