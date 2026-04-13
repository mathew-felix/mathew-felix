<div align="center">

# Felix Mathew

**ML Engineer · AI Engineer · Software Engineer**

MS Computer Science — Texas State University (Thesis, Apr 2026) · GPA 3.5/4.0
San Marcos, TX · F-1 OPT · STEM Extension Eligible

[![LinkedIn](https://img.shields.io/badge/LinkedIn-mathew--felix-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/mathew-felix)
[![Email](https://img.shields.io/badge/Email-felix--mathew%40outlook.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:felix-mathew@outlook.com)

</div>

---

## About

My MS thesis designed a 4-stage neural compression system combining YOLOv9 object detection, KLT optical flow propagation, DCVC-RT learned video compression, and AMT deep frame interpolation — achieving **97.4% transmitted-size reduction** on GPU and Jetson edge hardware. Separately I trained a custom PyTorch Transformer to **31.41 sacreBLEU** on a 4.39M-pair corpus and deployed it behind a FastAPI service with a ChromaDB RAG retrieval layer — **[try it live](https://huggingface.co/spaces/mathew-felix/nmt-translator)**. I also built an **8-node LangGraph agent** that detects hallucinated and deprecated library APIs in LLM-generated Python code.

---

## Tech Stack

**Languages**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=cplusplus&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=mysql&logoColor=white)

**ML / AI**

![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![Hugging Face](https://img.shields.io/badge/Hugging%20Face-FFD21E?style=flat-square&logo=huggingface&logoColor=black)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat-square&logo=openai&logoColor=white)
![LangGraph](https://img.shields.io/badge/LangGraph-1C3C3C?style=flat-square&logo=langchain&logoColor=white)
![W&B](https://img.shields.io/badge/Weights_%26_Biases-FFBE00?style=flat-square&logoColor=black)

**Backend / DevOps**

![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonaws&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)

---

## Featured Projects

### Neural ROI-Aware Video Compression *(MS Thesis)*
> PyTorch · YOLOv9 · DCVC-RT · KLT Optical Flow · AMT · Docker · Jetson Orin Nano

4-stage compression pipeline for wildlife camera traps on edge hardware. Transmits only detected regions of interest rather than full frames.

| Metric | Result |
|---|---|
| Transmitted-size reduction | **97.4%** (38.52× ratio) |
| ROI MS-SSIM | **0.9758** vs full-frame 0.9625 |
| Detector call reduction via KLT | **93.28%** |
| KLT speedup vs dense detection | **4.41×** |
| ROI-presence recall | **96.24%** |
| Test set | 20 held-out wildlife video clips |

Each stage evaluated on PSNR, MS-SSIM, LPIPS, and downstream detector proxy AP50 across ROI and full-frame regions. Validated on NVIDIA RTX 3070 Ti and Jetson Orin Nano. Packaged as a Docker image with SHA256-verified model downloads.

[![Repo](https://img.shields.io/badge/GitHub-nevc--dcvc-181717?style=flat-square&logo=github)](https://github.com/mathew-felix/nevc-dcvc)

---

### English-to-Spanish NMT Transformer + Translation Service
> PyTorch · Hugging Face · FastAPI · ChromaDB · LangGraph · OpenAI · Docker · W&B

**[▶ Live Demo on Hugging Face Spaces](https://huggingface.co/spaces/mathew-felix/nmt-translator)**

Custom encoder-decoder Transformer trained from scratch on a 4.39M-pair corpus (Europarl, TED2020, News Commentary, OpenSubtitles), deployed behind a FastAPI service with a ChromaDB retrieval layer and a GPT-4o-mini revision step for domain-specific text.

| Metric | Result |
|---|---|
| sacreBLEU (test set) | **31.41** |
| Test pairs | 878,564 held-out pairs |
| Training corpus | 4.39M sentence pairs |
| Training | 30 epochs · batch 640 · RTX PRO 6000 Blackwell |
| Retrieval index | 50K Europarl pairs · all-MiniLM-L6-v2 |
| Baseline comparison | Helsinki-NLP/opus-mt-en-es · 50-sentence cross-domain benchmark |

LangGraph routing layer with two registered OpenAI-schema tools — routes domain-specific requests through RAG, general requests through the offline NMT model.

[![Demo](https://img.shields.io/badge/Live%20Demo-HF%20Spaces-FFD21E?style=flat-square&logo=huggingface&logoColor=black)](https://huggingface.co/spaces/mathew-felix/nmt-translator)
[![Repo](https://img.shields.io/badge/GitHub-english--spanish--translator-181717?style=flat-square&logo=github)](https://github.com/mathew-felix/english-spanish-translator)

---

### LLM Code Hallucination Validator
> LangGraph · GPT-4o-mini · FastAPI · Pydantic v2 · Python ast

8-node LangGraph agent that detects hallucinated imports, deprecated methods, and incorrect API signatures in LLM-generated Python code. Uses `ast`-based static extraction matched against a hand-labeled library breaking-change database, with a GPT-4o-mini supervisor selecting which specialist validators to activate per request.

| Metric | Result |
|---|---|
| Agent precision / recall | **76.6% / 72.0%** |
| Labeled issues evaluated | 82 issues · 50 test cases |
| Dictionary baseline | 86.7% / 80.2% (documented trade-off) |
| Confidence filter | 0.6 threshold before report emission |
| Fallback | Deterministic path when LLM unavailable |

Pydantic v2 schemas enforce typed structure at every LangGraph state transition. Exposed via `POST /validate` on FastAPI.

[![Repo](https://img.shields.io/badge/GitHub-llm--code--validator-181717?style=flat-square&logo=github)](https://github.com/mathew-felix/llm-code-validator)

---

## Experience

**Graduate Teaching Assistant — Texas State University** *(Aug 2025 – Present)*
Led C++ programming labs for 25–30 undergraduate students. Supervised 21 Graduate Instructional Assistants handling tutoring and lab grading across a first-year CS foundation course required of all engineering undergraduates.

**Graduate Instructional Assistant — Texas State University** *(Jan 2025 – Jul 2025)*
Tutored undergraduate students and graded C++ lab submissions for the same first-year CS foundation course. Promoted to GTA after one semester.

**Associate Software Engineer — Neosoft Technologies** *(Aug 2021 – Jan 2023)*
Built AWS Lambda functions for a production CRM platform. Collaborated on a React-to-Next.js migration with server-side rendering for a media client. Resolved data inconsistencies across a production MySQL CRM database.

---

## Education

**MS Computer Science (Thesis Option)** — Texas State University · GPA 3.5/4.0 · Aug 2024 – May 2026
Thesis: *Neural Region-of-Interest-Aware Video Compression for Wildlife Monitoring Under Edge Computing Constraints* · Graduate Merit Fellow 2024–2025

**BTech Computer Science and Engineering** — Dr. Babasaheb Ambedkar Technological University · GPA 8.56/10.0 · 2018 – 2021

---

<div align="center">

*Open to entry-level ML Engineering, AI Engineering, and Software Engineering roles — available May 2026.*
*Authorized to work in the U.S. (F-1 OPT, STEM extension eligible).*

[![LinkedIn](https://img.shields.io/badge/Connect%20on%20LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/mathew-felix)

</div>
