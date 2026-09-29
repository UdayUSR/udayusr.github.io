---
title: "Unmasking Shortcut Learning in IoT Intrusion Detection: A Forensic, Multi-Paradigm Evaluation of Feature Dependence and Data Leakage"
collection: publications
category: under_review
permalink: /publication/shortcut-learning-iot-intrusion-detection
status: ""
authors: "<strong>Uday Shankar Roy</strong>, Mahbuba Jahan Minu"
date: 2026-02-15
venue: "Under Review (Preprint available on arXiv)"
arxiv: "https://arxiv.org/abs/2609.28725"
paperurl: "https://arxiv.org/pdf/2609.28725"
citation: "Roy, U. S., & Minu, M. J. (2026). Unmasking Shortcut Learning in IoT Intrusion Detection: A Forensic, Multi-Paradigm Evaluation of Feature Dependence and Data Leakage. arXiv preprint arXiv:2609.28725."
excerpt: "Exposes how ML-based Network Intrusion Detection Systems (NIDS) achieve misleading near-perfect benchmark performance by exploiting dataset shortcuts (such as static IP addresses and timestamp artifacts) rather than learning genuine attack patterns. Evaluates feature dependence and data leakage across tree-based and linear paradigms."
---

## Abstract
Machine Learning-based Network Intrusion Detection Systems (ML-NIDS) are frequently deployed to safeguard Internet-of-Things (IoT) ecosystems, often reporting near-perfect F1-scores on benchmark datasets. However, high benchmark performance frequently collapses when models are evaluated against realistic network traffic or out-of-distribution shifts. 

In this work, we conduct a forensic, multi-paradigm empirical evaluation exposing pervasive **shortcut learning** and subtle data leakage in standard IoT intrusion datasets. We demonstrate that models heavily exploit non-causal statistical artifacts—such as static host IP addresses, flow timing biases, and predictable port sequences—rather than learning intrinsic attack behavior. Furthermore, we reveal that vulnerability to shortcut features varies dramatically by architecture: tree-based models aggressively memorize timestamp patterns, whereas linear baselines fail to leverage temporal cues. We propose a feature-sanitized evaluation protocol to establish true operational robustness in IoT network defenses.

**Preprint:** [arXiv:2609.28725 [cs.CR]](https://arxiv.org/abs/2609.28725)  
**PDF:** [Download via arXiv](https://arxiv.org/pdf/2609.28725)  
**Status:** Under Review
