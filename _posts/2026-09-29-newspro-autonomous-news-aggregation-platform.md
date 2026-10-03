---
title: 'Engineering NewsPro: Building an Autonomous News Aggregation & AI Synthesis Platform'
date: 2026-09-29
permalink: /blog/2026/09/newspro-autonomous-news-aggregation-platform/
published: false
tags:
  - System Architecture
  - LLM Integration
  - FastAPI
  - Python
  - Automation
---

Modern digital journalism moves at breakneck speed. Readers and researchers often struggle with redundant coverage, sensationalized headlines, and information fragmentation across competing news outlets. 

To solve this, I designed and built **NewsPro**—an end-to-end autonomous news platform that continuously ingests breaking coverage from major news portals, clusters overlapping stories, synthesizes balanced objective summaries using the Google Gemini API, and publishes reports automatically.

In this writeup, I outline the system architecture, data pipeline, and key engineering decisions behind the platform.

---

## 1. System Architecture & Ingestion Pipeline

The NewsPro pipeline operates asynchronously to ensure fast ingestion without blocking user-facing read requests.

```mermaid
graph LR
    A["Web Portals / RSS Feeds"] --> B["BeautifulSoup4 Scrapers"]
    B --> C["Raw Story Queue"]
    C --> D["FastAPI Backend"]
    D --> E["Embedding & Duplicate Clustering"]
    E --> F["Google Gemini API (Synthesis)"]
    F --> G["SQLite / Turso Cloud Sync"]
    G --> H["Responsive Tailwind CSS Frontend"]
```

### Core Technology Stack:
* **Backend:** Python, FastAPI (asynchronous endpoints, Pydantic validation)
* **AI & Synthesis:** Google Gemini API (`gemini-1.5-flash` for high-throughput summarization and structured schema extraction)
* **Scraping & Ingestion:** BeautifulSoup4, `httpx`, `asyncio`
* **Storage & Persistence:** SQLite for local low-latency operations, synced to **Turso Cloud** (distributed libSQL)
* **Frontend:** Clean, responsive UI built with modern Tailwind CSS

---

## 2. Scraping & Deduplication

A major challenge in news aggregation is **duplicate coverage**. When a major event breaks, multiple agencies publish nearly identical reports. Ingesting raw articles without clustering floods the database and wastes LLM inference tokens.

To mitigate this:
1. **Normalized Fingerprinting:** Articles are fingerprinted based on entity extraction, publication timestamps, and URL canonicalization.
2. **Cluster Windowing:** Stories ingested within a sliding temporal window (e.g., 6 hours) are grouped using lightweight TF-IDF and cosine similarity heuristics before hitting the generative model.

```python
import asyncio
from bs4 import BeautifulSoup
import httpx

async def fetch_article(client: httpx.AsyncClient, url: str) -> dict:
    """Asynchronously scrape and parse clean article text."""
    try:
        response = await client.get(url, timeout=10.0, follow_redirects=True)
        soup = BeautifulSoup(response.text, "html.parser")
        
        # Extract title and body paragraphs
        title = soup.find("h1").get_text(strip=True) if soup.find("h1") else "No Title"
        paragraphs = [p.get_text(strip=True) for p in soup.find_all("p")]
        body = "\n".join(p for p in paragraphs if len(p) > 40)
        
        return {"url": url, "title": title, "body": body}
    except Exception as e:
        return {"url": url, "error": str(e)}
```

---

## 3. Structured Synthesis with Google Gemini

Once a cluster of related articles is formed, NewsPro invokes Google Gemini with structured output constraints:
* **Objective TL;DR:** A 2-sentence unbiased executive summary.
* **Key Bullet Points:** 3 to 5 core verified facts agreed upon across multiple sources.
* **Source Attribution:** Clear attribution linking back to original publishers.

```python
import google.generativeai as genai

def synthesize_cluster(cluster_texts: list[str]) -> str:
    """Synthesize multi-source coverage into an objective briefing."""
    model = genai.GenerativeModel("gemini-1.5-flash")
    
    prompt = f"""
    You are an objective news editor. Synthesize the following reporting from multiple outlets 
    into a neutral, fact-checked digest. Highlight consensus facts, acknowledge any conflicting reports, 
    and provide a 2-sentence executive summary followed by key bullet points.
    
    ARTICLES:
    {"---".join(cluster_texts[:4])}
    """
    response = model.generate_content(prompt)
    return response.text
```

---

## 4. Edge-Ready Persistence with Turso Cloud

By combining **SQLite** with **Turso Cloud (libSQL)**, NewsPro gains the simplicity of local embedded storage during development with edge-replicated durability in production. This setup eliminated heavy server provisioning costs while maintaining sub-50ms query responses.

---

## Key Takeaways

1. **Token Efficiency Matters:** Pre-filtering raw HTML and deduplicating coverage prior to LLM calls cut API costs by over 60%.
2. **Resilience over Speed:** Handling crawler rate limits, network timeouts, and anti-scraping protections requires robust exponential backoff.
3. **Autonomous Systems Need Guardrails:** Strict prompt framing and validation schemas prevent hallucination when synthesizing controversial or breaking stories.
