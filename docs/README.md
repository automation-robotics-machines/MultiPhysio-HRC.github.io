# MultiPhysio‑HRC: Multimodal Physiological Signals Dataset for Industrial Human‑Robot Collaboration

> Official companion repository for the paper **“MultiPhysio‑HRC: Multimodal Physiological Signals Dataset for industrial Human‑Robot Collaboration.”** This repo hosts code, docs, and assets to reproduce our preprocessing, feature extraction, and baseline models.

<p align="center">
  <a href="#citation"><img alt="Cite this" src="https://img.shields.io/badge/Cite-this-blue"></a>
  <a href="#getting-started"><img alt="Python" src="https://img.shields.io/badge/Python-3.9%2B-blue"></a>
  <a href="#license"><img alt="License" src="https://img.shields.io/badge/License-TBD-lightgrey"></a>
  <a href="https://tinyurl.com/MultiPhysio-HRC"><img alt="Dataset" src="https://img.shields.io/badge/Dataset-MultiPhysio--HRC-brightgreen"></a>
  <img alt="Status" src="https://img.shields.io/badge/Status-Active-success">
</p>

---

## ✨ TL;DR
- **What:** A public **multimodal dataset** (EEG, ECG, EDA, RESP, EMG, voice, facial AUs) collected across **real industrial‑like HRC**, cognitive tasks, VR stressors, and resting baselines.
- **Why:** To study **stress, cognitive load, and emotion** for **human‑aware robotics**.
- **Also:** Code to **reproduce preprocessing, feature extraction, and paper baselines**.

**Dataset:** https://tinyurl.com/MultiPhysio-HRC  
**Paper (PDF):** `paper/` (this repo)  

---

## Table of Contents
- [Overview](#overview)
- [Highlights](#highlights)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [Dataset at a Glance](#dataset-at-a-glance)
- [Data Schema](#data-schema)
- [Reproducing the Paper Baselines](#reproducing-the-paper-baselines)
- [Results (from the paper)](#results-from-the-paper)
- [FAQ](#faq)
- [Citation](#citation)
- [Acknowledgments & Funding](#acknowledgments--funding)
- [License](#license)
- [Contact](#contact)

---

## Overview
**MultiPhysio‑HRC** is a multimodal dataset and toolkit for **mental‑state estimation** in **industrial Human‑Robot Collaboration (HRC)**. It combines **physiological signals** (EEG, ECG, EDA, EMG, respiration) with **voice** and **facial action units**, collected under **realistic HRC, manual tasks, VR stressors, cognitive tasks, and rest**.

Use it to study **stress**, **cognitive load**, **valence/arousal/dominance**, and to build **human‑aware** adaptive robotic systems.

---

## Highlights
- **Industrial‑like HRC**: battery disassembly with a collaborative robot (voice‑controlled), plus manual sessions.
- **Diverse conditions**: cognitive load tasks (Stroop, N‑Back, arithmetic, Tower of Hanoi), guided breathing, VR height exposure, and rest.
- **Rich ground truth**: STAI‑Y1 (stress), NASA‑TLX (workload), SAM (valence, arousal, dominance); NARS at start.
- **Multimodal**: EEG (12‑ch dry), ECG, EDA, RESP, EMG at 256 Hz; voice; facial AUs (reduced fps for efficiency).
- **Baselines**: Ready‑to‑run pipelines + models for regression/classification of stress and cognitive load.

---

## Repository Structure
```
.
├─ paper/                          # Camera‑ready or preprint PDF, figures (optional)
├─ docs/
│  ├─ dataset_overview.md          # Modalities, tasks, questionnaires, ethics
│  ├─ data_schema.md               # File formats, splits, naming, timestamps
│  └─ benchmarks.md                # Baseline setups & expected metrics
├─ src/
│  ├─ dataprep/                    # Loading, syncing, cleaning
│  ├─ features/                    # Physio, EEG, voice, AUs feature extraction
│  ├─ models/                      # Baselines (RF/AB/XGB), utils
│  └─ eval/                        # Metrics, LOSO CV, reporting
├─ notebooks/
│  ├─ 01_quicklook.ipynb           # Explore a subject & modalities
│  ├─ 02_extract_features.ipynb    # End‑to‑end feature extraction
│  └─ 03_train_baselines.ipynb     # Reproduce results from the paper
├─ examples/
│  └─ minimal_pipeline.py          # Scripted end‑to‑end run
├─ requirements.txt                # Python deps
├─ pyproject.toml                  # (optional) for modern builds
├─ CITATION.cff                    # Paper metadata (fill in DOI when available)
└─ README.md                       # You are here
```

> **Tip:** If you keep raw data outside the repo, set `MULTIPHYSIO_HRC_DATA` env var to the dataset root to avoid passing paths around.

---

## Getting Started
### 1) Install
```bash
# create a clean env (conda or mamba recommended)
conda create -n mphrc python=3.10 -y
conda activate mphrc

# install dependencies
pip install -r requirements.txt
```

### 2) Download the dataset
- Visit **https://tinyurl.com/MultiPhysio-HRC** and follow the instructions to obtain access and download files.
- Keep the raw data in a folder of your choice and set:
```bash
export MULTIPHYSIO_HRC_DATA=/path/to/MultiPhysio-HRC
```

### 3) Sanity‑check a subject
```bash
jupyter lab  # then open notebooks/01_quicklook.ipynb
```

---

## Dataset at a Glance
**Participants**
- Day 1: 55 subjects; Day 2: 42 subjects.

**Sessions & Tasks**
- **Day 1**: Rest → Cognitive tasks (Stroop, N‑Back, Mental Arithmetic, Tower of Hanoi; ticking clock & error buzzer for pressure) → Guided Breathing → VR (height exposure).
- **Day 2**: Rest → **Manual** battery disassembly → **Collaborative** disassembly with a voice‑controlled cobot (Fanuc CRX‑20).

**Modalities**
- **Physio**: ECG, EDA, EMG, RESP @ 256 Hz (Bitbrain Versatile Bio); EEG: 12‑channel dry EEG (Bitbrain Diadem); **Voice** recordings; **Facial AUs** (down‑sampled for efficiency).

**Ground truth**
- Per‑task: **STAI‑Y1**, **NASA‑TLX**, **SAM**; At start: **NARS**.

**Ethics**
- Conducted under institutional approval and with informed consent; see paper for details.

---

## Data Schema
> The exact file tree may differ depending on distribution. Below is a **reference schema** used by this repo’s loaders.

```
MultiPhysio-HRC/
├─ participants.tsv                       # demographics & metadata
├─ day1/
│  ├─ sub-XXXX/
│  │  ├─ physio/
│  │  │  ├─ ecg.tsv.gz                    # 256 Hz; UTC timestamps
│  │  │  ├─ eda.tsv.gz
│  │  │  ├─ emg.tsv.gz
│  │  │  └─ resp.tsv.gz
│  │  ├─ eeg/
│  │  │  └─ eeg.tsv.gz                    # 12 channels (AF7,Fp1,Fp2,AF8,F3,F4,P3,P4,PO7,O1,O2,PO8)
│  │  ├─ video/
│  │  │  └─ webcam.mp4                    # optional, when available
│  │  ├─ audio/
│  │  │  └─ mic.wav
│  │  └─ labels/
│  │     ├─ stai_y1.csv
│  │     ├─ nasa_tlx.csv
│  │     └─ sam.csv
│  └─ ...
├─ day2/
│  └─ sub-XXXX/                           # same structure; includes manual vs HRC flags per segment
└─ derivatives/
   ├─ features_physio.parquet             # 60s windows; ~250 features
   ├─ features_eeg.parquet                # 5s windows; bandpowers & entropies
   ├─ features_voice.parquet              # MFCC stats, jitter/shimmer, etc.
   └─ aus.parquet                         # 2 fps AU probabilities (20 AUs)
```

- **Timestamps & Sync:** All streams carry timestamps; loaders align them per task/segment.
- **Windows:** Physio features on 60 s windows; EEG on 5 s windows; AUs at 2 fps.

---

## Reproducing the Paper Baselines
**End‑to‑end (script):**
```bash
python examples/minimal_pipeline.py \
  --data $MULTIPHYSIO_HRC_DATA \
  --modality physio \
  --task regression --label STAI \
  --cv loso --report out/report_physio_stai.json
```

**Notebooks:**
1. `02_extract_features.ipynb` – computes features for Physio/EEG/Voice/AUs.
2. `03_train_baselines.ipynb` – trains RF / AdaBoost / XGBoost for regression & 3‑class classification (Low/Med/High) based on per‑subject z‑like thresholds.

**Models:** RandomForest, AdaBoost, XGBoost. Evaluation uses **Leave‑One‑Subject‑Out (LOSO)**. Features & labels are min–max normalized within‑subject as in the paper.

---

## Results (from the paper)
- **Regression (STAI‑Y1 & NASA‑TLX):** Physiological features yield the **lowest RMSE**, stronger than EEG and Voice.
- **3‑Class Classification (Stress & Cognitive Load):** Physiological features achieve the **highest F1**, with EEG close behind for cognitive load; Voice trails Physio/EEG.

> See `docs/benchmarks.md` for expected ranges and how we compute the Low/Med/High bins per subject.

---

## FAQ
**Q: How do I get access to raw videos or robot logs?**  
A: See the dataset page. Some assets may require additional request/agreements.

**Q: Can I use this dataset for commercial work?**  
A: Check the **dataset page license** and this repo’s **LICENSE**. If in doubt, open an issue.

**Q: Are there ready‑made splits?**  
A: We default to **Leave‑One‑Subject‑Out**. Utility functions can generate stratified splits by task/condition.

---

## Citation
If you use **MultiPhysio‑HRC** or this code, please cite the paper:

```bibtex
@article{MultiPhysioHRC2025,
  title   = {MultiPhysio-HRC: Multimodal Physiological Signals Dataset for industrial Human-Robot Collaboration},
  author  = {Bussolan, Andrea and Baraldo, Stefano and Avram, Oliver and Urcola, Pablo and Montesano, Luis and Gambardella, Luca Maria and Valente, Anna},
  year    = {2025},
  journal = {TBD},
  volume  = {TBD}, number = {TBD}, pages = {TBD},
  doi     = {TBD},
}
```

> A `CITATION.cff` file is included; please update DOI/venue once available.

---

## Acknowledgments & Funding
- **Horizon Europe — FLUENTLY** (Grant **101058680**)
- **Eurostars — !2309‑Singularity**
- We thank all participants and the technical staff who supported the acquisition campaign.

---

## License
- **Code:** see [LICENSE](LICENSE). (We recommend a permissive license such as MIT/Apache‑2.0.)
- **Dataset:** see the dataset page for the applicable data license and usage terms.

---

## Contact
- Lead contact: **andrea.bussolan@supsi.ch**
- Issues & questions: please open a GitHub issue.

---

*Maintainers:* Andrea Bussolan, Stefano Baraldo.