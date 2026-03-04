# ASTRA@DravidianLangTech 2026
### Tri-View Transformation Modeling for Telugu Prompt Style Recovery

This repository contains the implementation of the **ASTRA system** submitted to the shared task **Prompt Recovery for LLM in Telugu** at **DravidianLangTech@ACL 2026**.

Our system models stylistic transformation between an original transcript and a rewritten version by explicitly capturing edit operations and combining them with transformer-based representations.

---

# Task Description

The goal of the task is to classify the **stylistic intent** expressed in a rewritten Telugu transcript.

Each instance consists of:

- **ORIGINAL TRANSCRIPTS** – original Telugu text
- **CHANGE STYLE** – rewritten text reflecting a stylistic modification

The system must predict one of the following **9 style categories**:

1. Formal  
2. Informal  
3. Optimistic  
4. Pessimistic  
5. Humorous  
6. Serious  
7. Inspiring  
8. Authoritative  
9. Persuasive  

---

# Method Overview

Our system models style recovery as a **transformation classification problem**.

Instead of classifying the rewritten text alone, we explicitly analyze how the text changes from the original version to the modified version.

The model uses a **Tri-View Representation**:

1️⃣ Original transcript  
2️⃣ Rewritten transcript  
3️⃣ Token-level edit difference representation  

The edit representation is derived using token alignment and records insertion and deletion operations.

All three inputs are encoded using a **shared multilingual transformer encoder (XLM-RoBERTa)**.

A **gating fusion module** learns the importance of each view and combines them into a unified representation for classification.

---

# System Architecture
Original Text ─┐
│
├── Transformer Encoder ──┐
│
Modified Text ─┘ │
│
Edit-Diff Representation ── Transformer Encoder
│
Tri-view fusion (Gated attention)
│
Style classifier
│
Predicted Style

---

# Validation Results

| Metric | Score |
|------|------|
Accuracy | 0.3967
Macro F1 | 0.3856

Validation dataset size: **300 samples**

---

# Repository Structure
ASTRA-DravidianLangTech-2026/

data/
PR_train.xlsx
PR_validation.xlsx
PR_test.xlsx

src/
train_astra_tri.py
predict.py

models/
astra_tri_best.pt

notebooks/
Telugu_PR.ipynb

submission/
submission.csv
