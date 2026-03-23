# Zero-Data AI Pipeline
## Soil Microbiome → Mycorrhizal Colonisation → Carbon Sequestration

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/iyerlatha2025-LN/funga-zero-data-ai/blob/main/notebooks/Zero_Data_AI_Funga_Colab.ipynb)

**Author:** Latha Iyer | University of Louisville  
**ORCID:** 0009-0000-8755-8805  
**Contact:** latha.iyer@louisville.edu

---

## ✅ Does it run?

**Yes.** Verified in Google Colab on 23 March 2026.
All 10 cells execute successfully. Runtime under 4 minutes.
Full output PDF is in `docs/`.

```
✓ Cell 1  — Imports
✓ Cell 2  — Public unlabelled database (2,000 samples)
✓ Cell 3  — Self-supervised autoencoder (MSE 0.431)
✓ Cell 4  — Funga labelled field data (360 plots × 18 sites)
✓ Cell 5  — Zero-shot prediction (4 new sites, zero history)
✓ Cell 6  — ANN training  R²=0.652 colonisation
✓ Cell 7  — ACCB Fuse  91.9% coverage (guarantee 90%)
✓ Cell 8  — Carbon accounting  4.28 Mg C/yr
✓ Cell 9  — Full results dashboard
✓ Cell 10 — Summary
```

---

## Overview

A Zero-Data AI pipeline predicting mycorrhizal colonisation success,
forest productivity, and carbon sequestration from soil microbiome
DNA sequencing data — including **zero-shot prediction for brand-new
sites with no historical field data**.

Directly addresses a limitation identified in published ecological research:

> *Iyer & Narasimhan (2010) "Green ICT to Save Himalayas" (ICGREEN,
> Bangalore) found that limited ecological data prevents reliable
> prediction. This pipeline solves that with self-supervised pre-training
> and zero-shot site inference.*

---

## Key Results

| Metric | Value |
|--------|-------|
| Autoencoder MSE (unlabelled data) | 0.431 |
| ANN R² — mycorrhizal colonisation | 0.652 |
| ANN R² — above-ground biomass | 0.373 |
| ACCB empirical coverage | 91.9% (guarantee: 90%) |
| Zero-shot sites | 4 (zero historical data) |
| Portfolio carbon | 4.28 Mg C/yr |

---

## Zero-Data AI — Three Concepts

**1. Self-Supervised Autoencoder**
Learns 4D soil health embeddings from 2,000 unlabelled OTU samples.
No colonisation rates. No biomass. No labels at all.
Architecture: `8 → 16 → 4 → 16 → 8`

**2. Zero-Shot Prediction**
New site described by soil type + pH + moisture only.
Mapped to nearest learned embedding → weighted prediction.
No site-specific training data required.

**3. ACCB Fuse — Novel CI Scaling**
```
Zero-shot CI = q̂ × (1 + nn_distance)
```
New sites automatically get wider intervals.
CI narrows as real data accumulates.
Formal 90% coverage guarantee throughout.
**This formula is not in any existing literature.**

---

## Pipeline

```
Unlabelled public data (2,000 samples)
    ↓ Self-supervised autoencoder
    ↓ 4D soil health embeddings
Funga labelled data (360 plots × 18 sites)
    ↓ Spatial block CV (whole sites held out)
    ↓ ANN: 64 → 32 → 16
    ↓ Multi-output: colonisation + biomass + carbon
Zero-shot new sites (0 historical data)
    ↓ AE embedding → nearest neighbour
    ↓ Weighted prediction
ACCB Fuse
    ↓ Static conformal calibration
    ↓ CI = q̂ × (1 + nn_distance) for zero-shot
    ↓ 90% coverage guarantee
Carbon accounting
    ↓ Per-site Mg C/ha/yr
    ↓ Portfolio CO₂ equivalent
```

---

## Repository Structure

```
funga-zero-data-ai/
│
├── notebooks/
│   └── Zero_Data_AI_Funga_Colab.ipynb   ← Run in Colab
│
├── src/
│   └── zero_data_pipeline.py             ← Full module
│
├── outputs/
│   └── zero_data_dashboard.png           ← Results dashboard
│
├── docs/
│   └── Funga_ZeroDataAI_Pipeline_Analysis.pdf
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

## Quick Start

### Google Colab (recommended — zero setup)
Click the **Open in Colab** badge above.
`Runtime → Run all` — complete in under 4 minutes.

### Local
```bash
git clone https://github.com/iyerlatha2025-LN/funga-zero-data-ai
cd funga-zero-data-ai
pip install -r requirements.txt
python src/zero_data_pipeline.py
```

---

## 2010 → 2025 Method Evolution

| Aspect | 2010 Paper | 2025 Pipeline |
|--------|-----------|---------------|
| Model | MLP (Neurosolutions) | Deep MLP + AE embeddings |
| Spatial | Not addressed | Spatial lag + positional encoding |
| Temporal | None | LSTM + temporal lag |
| Uncertainty | MSE only | Conformal CI (90% guaranteed) |
| New site | Not possible | Zero-shot prediction |
| Privacy | N/A | Federated ACCB Grid |
| Tools | Neurosolutions + Excel | Python / numpy (open source) |

---

## ACCB Framework

The uncertainty layer implements the
**Adaptive Clinical Circuit Breaker (ACCB)**,
a conformal prediction governance framework with three layers:

| Layer | Mechanism |
|-------|-----------|
| Fuse | Static conformal, calibrated once, formal coverage |
| Breaker | Online ACI: `q̂_{t+1} = q̂_t + γ(1−α−err_t)` |
| Grid | Federated multi-site calibration (privacy-preserving) |

ACCB paper: arXiv submission in preparation.

---

## Requirements

```
numpy >= 1.24
pandas >= 1.5
matplotlib >= 3.6
scikit-learn >= 1.2
scipy >= 1.10
statsmodels >= 0.13
```

All pre-installed in Google Colab — no pip installs needed.

---

## Citation

```bibtex
@software{iyer2025zerodataai,
  author    = {Iyer, Latha},
  title     = {Zero-Data AI Pipeline for Soil Microbiome Analysis},
  year      = {2025},
  publisher = {GitHub},
  url       = {https://github.com/iyerlatha2025-LN/funga-zero-data-ai},
  orcid     = {0009-0000-8755-8805}
}
```

---

## License

MIT — free to use with attribution.
