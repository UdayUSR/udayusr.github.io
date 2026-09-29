---
title: "PromptTriage: A Multi-Class Detection and Defense Framework for Prompt Injection Attacks in LLM-Integrated Applications"
collection: publications
category: under_review
permalink: /publication/prompt-triage-llm-defense
status: ""
authors: "Mahbuba Jahan Minu, <strong>Uday Shankar Roy</strong>"
date: 2026-02-01
venue: "Under Review"
citation: "Minu, M. J., & Roy, U. S. (2026). PromptTriage: A Multi-Class Detection and Defense Framework for Prompt Injection Attacks in LLM-Integrated Applications. Under Review."
excerpt: "Develops a proactive multi-class defense framework that categorizes prompt injection attacks into four structured threat classes and dynamically maps each class to a type-specific defense action, reducing attack success from 16/50 to 1/50 while sanitizing or blocking 48 of 50 attacks."
---

## Abstract
Prompt injection attacks pose severe security threats to large language model (LLM) agents and integrated applications, allowing untrusted user inputs to hijack system prompts and trigger unauthorized tool invocations. Existing defenses typically treat injection detection as a binary classification problem, lacking the granular context required to safely recover from ambiguous inputs. 

To address this limitation, we introduce **PromptTriage**, a multi-class detection and proactive defense framework that categorizes prompt injection vectors into four distinct threat classes and maps each category to an optimal mitigation strategy (e.g., selective sanitization, context isolation, or dynamic blocking). Evaluating PromptTriage against a Qwen2.5-1.5B-Instruct agent demonstrated a reduction in attack success rate from 16/50 down to 1/50, successfully neutralizing or blocking 48 out of 50 adversarial payloads while preserving task utility.

**Status:** Under Review (Targeting top-tier AI/Security venue)
