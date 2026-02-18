# MultiPhysio‑HRC: Multimodal Physiological Signals Dataset for Industrial Human‑Robot Collaboration

> Official companion repository for the paper **“MultiPhysio‑HRC: Multimodal Physiological Signals Dataset for Industrial Human‑Robot Collaboration.”** This repo hosts code, docs, and assets to reproduce our preprocessing, feature extraction, and baseline models.

<p align="center">
  <a href="https://arxiv.org/abs/2510.00703"><img alt="arXiv" src="https://img.shields.io/badge/Paper-arXiv-b31b1b?logo=arxiv"></a>
  <a href="https://github.com/automation-robotics-machines/MultiPhysio-HRC"><img alt="GitHub Repo" src="https://img.shields.io/badge/Code-GitHub-black"></a>
  <a href="https://zenodo.org/records/18668043"><img alt="Dataset" src="https://img.shields.io/badge/Dataset-Zenodo-brightgreen"></a>
  <a href="#citation"><img alt="Cite this" src="https://img.shields.io/badge/Cite-this-blue"></a>
</p>

---

## ✨ TL;DR
- **What:** A public **multimodal dataset** (EEG, ECG, EDA, RESP, EMG, voice, facial AUs) collected across **real industrial‑like HRC**, cognitive tasks, VR stressors, and resting baselines.
- **Why:** To study **stress, cognitive load, and emotion** for **human‑aware robotics**.
- **Also:** Code to **reproduce preprocessing, feature extraction, and paper baselines**.

--- 

## Access

**Dataset:** [https://zenodo.org/records/18668043](https://zenodo.org/records/18668043)

**Paper (PDF):** [https://arxiv.org/abs/2510.00703](https://arxiv.org/abs/2510.00703)

**GitHub (code, preprocessing, baselines):** [https://github.com/automation-robotics-machines/MultiPhysio-HRC](https://github.com/automation-robotics-machines/MultiPhysio-HRC)

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

## Media
<p align="center">
  <em>Figures and demo videos will be added here.</em>
</p>

---

## Dataset at a Glance
**Participants**
- Day 1: 52 subjects; 
- Day 2: 42 subjects.

_Some participants retired from the public release of the dataset, therefore there is a discrepancy with respect to the numbers mentioned in the paper._

**Sessions & Tasks**
- **Day 1 – Baseline and Stress Induction**
    - Rest
    - Cognitive tasks (Stroop, N-back, Arithmetic, Hanoi Tower)
    - Breathing exercise
    - Virtual Reality task (Richie’s Plank Experience)

- **Day 2 – Manual and Robot-Assisted Disassembly**
    - Rest
    - Manual battery disassembly
    - Collaborative disassembly with a Fanuc CRX-20 cobot, using voice commands

**Modalities**
- **Physio**: ECG, EDA, EMG, RESP @ 256 Hz (Bitbrain Versatile Bio); EEG: 12‑channel dry EEG (Bitbrain Diadem); **Voice** recordings; **Facial AUs** (down‑sampled for efficiency).

**Ground truth**
- Per‑task: **STAI‑Y1**, **NASA‑TLX**, **SAM**; At start: **NARS**.

**Ethics**
- Conducted under institutional approval and with informed consent; see paper for details.

---

## Citation
If you use **MultiPhysio‑HRC** or this code, please cite the paper:

```bibtex
@article{robotics14120184,
      AUTHOR = {Bussolan, Andrea and Baraldo, Stefano and Avram, Oliver and Urcola, Pablo and Montesano, Luis and Gambardella, Luca Maria and Valente, Anna},
      TITLE = {MultiPhysio-HRC: A Multimodal Physiological Signals Dataset for Industrial Human-Robot Collaboration},
      JOURNAL = {Robotics},
      VOLUME = {14},
      YEAR = {2025},
      NUMBER = {12},
      ARTICLE-NUMBER = {184},
      URL = {https://www.mdpi.com/2218-6581/14/12/184},
      ISSN = {2218-6581},
      DOI = {10.3390/robotics14120184}
}
```

---

## Acknowledgments & Funding
- **Horizon Europe — FLUENTLY** (Grant **101058680**)
- **Eurostars — !2309‑Singularity**
- We thank all participants and the technical staff who supported the acquisition campaign.

---

## Ethics & License

This dataset was collected under institutional ethical approval (SUPSI), with informed consent from all participants.
- **Code:** Licensed under the [MIT License](https://opensource.org/licenses/MIT).  
- **Dataset:** Released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).  

---

## Contact
- Lead contact: **andrea.bussolan@supsi.ch**
- Issues & questions: please open a GitHub issue.

---

*Maintainers:* Andrea Bussolan, Stefano Baraldo.