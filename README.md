<div align="center">

# Felix Mathew

**ML Systems Engineerr**

MS Computer Science — Texas State University · GPA 3.56/4.0 · Thesis defended April 2026
San Marcos, TX · F-1 OPT (STEM) · Seeking H-1B sponsorship

[![LinkedIn](https://img.shields.io/badge/LinkedIn-mathew--felix-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/mathew-felix)
[![Email](https://img.shields.io/badge/Email-felix--mathew%40outlook.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:felix-mathew@outlook.com)
[![PyPI](https://img.shields.io/badge/PyPI-llm--code--validator-3776AB?style=flat-square&logo=pypi&logoColor=white)](https://pypi.org/project/llm-code-validator/)
[![HF Space](https://img.shields.io/badge/HF%20Space-Live%20Demo-FFD21E?style=flat-square&logo=huggingface&logoColor=black)](https://huggingface.co/spaces/mathew-felix/nmt-translator)

</div>

---

## About

I build end-to-end systems — from CUDA/PyTorch research code to production APIs and published packages.

My MS thesis (defended April 2026, IMICS Lab) is a **codec-agnostic, ROI-aware video compression pipeline** for wildlife camera-trap footage under edge constraints: it splits the animal region and the background into separate streams with independent temporal sampling and pluggable codec backends, achieving **97.4% transmitted-size reduction at 36.12 dB ROI PSNR** on a 20-clip held-out test set. Manuscript in preparation with my advisor (co-author).

Alongside the thesis I shipped two public artifacts: a **deterministic INT16 CUDA runtime** for the DCVC-RT codec family that produces cross-device byte-reproducible bitstreams (validated by encoding on an NVIDIA DGX and decoding on an RTX 3070 Ti laptop GPU — matching SHA-256), and **`llm-code-validator`** on PyPI, a static-analysis CLI that detects version-incompatible Python API usage. I also maintain a [live English↔Spanish translation demo](https://huggingface.co/spaces/mathew-felix/nmt-translator) on Hugging Face Spaces.

Before grad school I spent 1.5 years as an Associate Software Engineer at NeoSOFT (CMMI Level 5) — AWS Lambda, MySQL, React → Next.js migration, Agile delivery.

---

## Tech Stack

**Languages**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=cplusplus&logoColor=white)
![CUDA](https://img.shields.io/badge/CUDA-76B900?style=flat-square&logo=nvidia&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=mysql&logoColor=white)

**ML / Systems**

![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![Hugging Face](https://img.shields.io/badge/Hugging%20Face-FFD21E?style=flat-square&logo=huggingface&logoColor=black)
![ONNX](https://img.shields.io/badge/ONNX-005CED?style=flat-square&logo=onnx&logoColor=white)
![FFmpeg](https://img.shields.io/badge/FFmpeg-007808?style=flat-square&logo=ffmpeg&logoColor=white)

**Backend / DevOps**

![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonaws&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)

---

## Featured Projects

### MS Thesis — Neural ROI-Aware Wildlife Video Compression
> Codec-agnostic dual-stream design · PyTorch · MegaDetector · KLT · AMT · Jetson Orin Nano · AV1 / HEVC

ROI-aware video compression for wildlife camera traps under edge constraints. The pipeline treats the animal region and the background as two streams with independent temporal sampling and different codec operating points, so bitrate is spent where it matters for downstream review.

The methodology is **codec-agnostic by design**: the main controlled study fixes a learned neural codec backend (DCVC-RT) so the effect of the dual-stream split can be isolated from codec choice; the deployment study on a Jetson Orin Nano swaps in a portable conventional stack (AV1 for the ROI stream, HEVC for the background stream) and demonstrates the same methodology end-to-end on edge hardware.

| Metric | Result |
|---|---|
| Transmitted-size reduction (held-out 20 clips) | **97.4%** (399.16 MB → 10.36 MB, 38.52× ratio) |
| Mean ROI PSNR | **36.12 dB** |
| Mean ROI MS-SSIM | **0.9758** (vs full-frame 0.9625) |
| ROI-stage detector calls reduced | **93.28%** |
| ROI-stage speedup vs dense detection | **4.41×** |
| ROI-presence recall | **96.24%** |

Defended April 3, 2026 — IMICS Lab, Texas State University. Advisor: Dr. Vangelis Metsis. Manuscript in preparation with thesis advisor (co-author). Funded in part by the BioStream grant.

[![Repo](https://img.shields.io/badge/GitHub-roi--wildlife--video--compression-181717?style=flat-square&logo=github)](https://github.com/mathew-felix/roi-wildlife-video-compression)
[![Library](https://img.shields.io/badge/TXST%20Digital%20Library-Record-blue?style=flat-square)](https://digital.library.txst.edu/items/0756ff05-2091-4363-8d27-6c2f66f7e4c7)

---

### Deterministic Neural Video Codec *(DCVC-RT family)*
> CUDA · PyTorch C++ Extensions · INT16 · rANS · SHA-256 · Apache-2.0

The upstream DCVC-RT codec runs FP16 inference, whose rounding behavior differs across NVIDIA GPU microarchitectures — small numerical divergences accumulate through the entropy context and corrupt reference frames when encode and decode run on different GPUs. This project replaces the FP16 inference path with a signed INT16 arithmetic profile using fixed power-of-two quantization scales, so every multiply-accumulate follows an explicit integer contract and bitstreams are bit-identical across GPUs.

| Metric | Result |
|---|---|
| Cross-device determinism | **SHA-256 match** — encode on NVIDIA DGX, decode on RTX 3070 Ti laptop GPU |
| End-to-end validation clip | 2,593 frames, 1280×720, QP 32 |
| Average RGB PSNR | **28.90 dB** |
| Average RGB MS-SSIM | **0.934** |
| Test suite | 35 tests (CUDA kernel parity, entropy roundtrip, bitstream SHA-256) |
| Size reduction vs original MP4 | **94.27%** (17.45× smaller) |

Native CUDA kernels for INT16 operations; C++ rANS entropy-coding PyTorch extension; calibration pipeline that converts upstream DCVC-RT FP16 checkpoints into INT16 bundles. Apache-2.0 with upstream Microsoft DCVC attribution.

[![Repo](https://img.shields.io/badge/GitHub-deterministic--neural--video--codec-181717?style=flat-square&logo=github)](https://github.com/mathew-felix/deterministic-neural-video-codec)

---

### Institutional English↔Spanish Translation — Transformer + RAG + FastAPI
> PyTorch · FastAPI · ChromaDB · Hugging Face · Docker · MIT

**[▶ Live demo on Hugging Face Spaces](https://huggingface.co/spaces/mathew-felix/nmt-translator)**

Custom encoder-decoder Transformer trained from scratch on a 3.5M English-Spanish sentence-pair corpus (Europarl, TED2020, News Commentary, OpenSubtitles). Deployed behind a FastAPI service with an optional ChromaDB bilingual evidence retrieval layer and an optional GPT reviewer over retrieved context — each response returns the draft, retrieved evidence, review status, final wording, and per-request provenance fields.

| Metric | Result |
|---|---|
| Held-out sacreBLEU | **31.41** |
| Test pairs | 878,564 |
| Training corpus | 3.5M sentence pairs |
| Retrieval index | 50K bilingual pairs · all-MiniLM-L6-v2 |
| Baseline comparison | DeepL, Google Cloud Translate, Azure Custom Translator, MarianMT |

Docker + docker-compose deployment, GitHub Actions CI, six dependency profiles (api / dev / demo / training / rag / gpt), Hugging Face Spaces Gradio deployment.

[![Demo](https://img.shields.io/badge/Live%20Demo-HF%20Spaces-FFD21E?style=flat-square&logo=huggingface&logoColor=black)](https://huggingface.co/spaces/mathew-felix/nmt-translator)
[![Repo](https://img.shields.io/badge/GitHub-english--spanish--translator-181717?style=flat-square&logo=github)](https://github.com/mathew-felix/english-spanish-translator)

---

### llm-code-validator — Python API-Drift Static Analysis *(PyPI)*
> Python · AST · CLI · pre-commit · GitHub Actions · No-LLM-key

```bash
pip install llm-code-validator
```

Static-analysis CLI that scans Python source code without executing it, identifies version-incompatible third-party API usage via AST, and reports issues before runtime. Targeted at codebases that depend on fast-moving libraries — OpenAI, Anthropic, LangChain, LangGraph, LlamaIndex, FastAPI, Pydantic, pandas, NumPy, scikit-learn, SQLAlchemy, PyTorch, Transformers, TensorFlow, ChromaDB, Pinecone, Weaviate, Qdrant, and more.

| Metric | Result |
|---|---|
| Rule database | **68 API-drift rules** · 15 safe fixes · 22 supported libraries |
| Test suite | **84 tests passing** |
| Internal benchmark | precision **1.0** / recall **1.0** |
| Output formats | text · JSON · GitHub Actions annotations |
| Integrations | pre-commit · GitHub Actions · staged-Git scan |
| LLM API keys required | **None** — default checks are 100% local, no network calls |

Supports private/internal signature databases, conservative "safe-fix" preview-and-apply mode, and exit codes appropriate for CI gating.

[![PyPI](https://img.shields.io/pypi/v/llm-code-validator?style=flat-square&logo=pypi&logoColor=white)](https://pypi.org/project/llm-code-validator/)
[![Repo](https://img.shields.io/badge/GitHub-llm--code--validator-181717?style=flat-square&logo=github)](https://github.com/mathew-felix/llm-code-validator)

---

## Experience

**Graduate Teaching Assistant — Texas State University** *(Sep 2025 – Present)*
Lead weekly C++ programming labs for 25–30 undergraduate students in a first-year CS foundation course required of every engineering undergraduate at Texas State. Coordinate workload distribution, grading consistency, and student-support standards across a team of 21 Graduate Instructional Assistants.

**Graduate Instructional Assistant — Texas State University** *(Dec 2024 – Sep 2025)*
Tutored undergraduate students and graded C++ lab submissions for the same first-year CS foundation course. Promoted to Graduate Teaching Assistant after one semester.

**Associate Software Engineer — NeoSOFT Technologies (CMMI Level 5)** *(Aug 2021 – Jan 2023)*
Built AWS Lambda services for a multi-tenant CRM platform. Led a React → Next.js migration with server-side rendering for a media client. Diagnosed and corrected production MySQL data inconsistencies with targeted SQL repair scripts that ran without service interruption.

---

## Education

**MS Computer Science (Thesis Option)** — Texas State University · GPA 3.56/4.0 · Aug 2024 – May 2026
Thesis: *Neural Region-of-Interest-Aware Video Compression for Wildlife Monitoring Under Edge Computing Constraints*
Advisor: Dr. Vangelis Metsis · IMICS Lab

**BTech Computer Science and Engineering** — CSMSS Chh. Shahu College of Engineering (Dr. Babasaheb Ambedkar Technological University) · 2018 – 2021

---

<div align="center">

*Open to Machine Learning Engineer, AI Engineer, and Software Engineer roles — available **July 8, 2026** (F-1 OPT start). STEM OPT extension up to 3 years. **Seeking employers who sponsor H-1B and refile annually until selection.***

[![LinkedIn](https://img.shields.io/badge/Connect%20on%20LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/mathew-felix)

</div>
