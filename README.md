# TFG-Identification-and-Tactical-Analysis-of-Football-Playing-Styles-through-Machine-Learning

# Identification and Tactical Analysis of Football Playing Styles through Machine Learning and Spatiotemporal Event Data

Bachelor's Thesis — Universitat Pompeu Fabra (UPF)
Grau en Enginyeria Matemàtica en Ciència de Dades
Course 2025–2026

**Author:** Biel Domingo Grifell
**Supervisor:** Javier Segovia Aguas

---

## Overview

This repository contains the full codebase developed for the Bachelor's Thesis
*"Identification and Tactical Analysis of Football Playing Styles through Machine
Learning and Spatiotemporal Event Data"*, applied to LaLiga 2015/16.

The project implements an end-to-end machine learning pipeline that:

1. **Extracts** seven possession-adjusted tactical features from StatsBomb's
   open event data of the 380 LaLiga 2015/16 matches.
2. **Discovers** four playing styles via K-Means and a Gaussian Mixture Model.
3. **Validates** the resulting taxonomy through Kruskal-Wallis tests and PCA.
4. **Builds** a 4 × 4 tactical match-up matrix, both raw and adjusted by each
   team's pre-match expected goals (xG) form via multinomial logistic regression.
5. **Quantifies** statistical robustness via per-cell bootstrap confidence
   intervals and a global Pearson chi-square test.
6. **Reads** the adjusted matrix through tournament theory, identifying a
   Condorcet winner and testing for non-transitive cycles.

The four playing styles discovered are: **High-Pressing Possession (C0)**,
**Cautious Possession (C1)**, **Low-Block Counter-Attack (C2)** and
**Direct Set-Piece Attack (C3)**. Once team quality is partialled out,
Cluster 2 emerges as the unique Condorcet winner of the round-robin tournament.

---

---

## Requirements

- Python 3.10 or later
- The Python packages listed in `requirements.txt`

Install them with:

```bash
pip install -r requirements.txt
```

---

## How to reproduce

1. Clone the repository:
```bash
   git clone https://github.com/Bieldogi/TFG-Identification-and-Tactical-Analysis-of-Football-Playing-Styles-through-Machine-Learning.git
   cd TFG-Identification-and-Tactical-Analysis-of-Football-Playing-Styles-through-Machine-Learning
```

2. (Optional but recommended) Create and activate a virtual environment:
```bash
   python -m venv .venv
   source .venv/bin/activate          # macOS / Linux
   .venv\Scripts\activate             # Windows
```

3. Install dependencies:
```bash
   pip install -r requirements.txt
```

4. Open the notebook:
```bash
   jupyter notebook TFG_PlayingStyles_LaLiga.ipynb
```

5. Run the cells in order. Random seeds are fixed (`random_state=42`) so the
   numerical results match those reported in the thesis document.

> **Note:** the notebook downloads StatsBomb event data through the
> `statsbombpy` library, which requires an internet connection on first run.
> Pre-computed feature CSVs are included in the `data/` folder so that the
> downstream analysis can be reproduced without re-fetching the raw events.

---

## Key empirical results

| Result | Value |
|---|---|
| Team-match observations clustered | 760 |
| Optimal number of clusters | K = 4 |
| Matches retained after warm-up filter | 337 |
| Chi-square test of style-pairing × outcome | χ² = 44.274, dof = 26, **p = 0.0141** |
| Multinomial logit training accuracy | 0.579 |
| Condorcet winner of the adjusted matrix | **Cluster 2 — Low-Block Counter-Attack** |
| Transitive ordering on neutral ground | C2 ≻ C1 ≻ C0 ≻ C3 |

---

## Data sources

The project uses the **StatsBomb Open Data** dataset for LaLiga 2015/16
(`competition_id = 11`, `season_id = 27`), publicly available at:

https://github.com/statsbomb/open-data

All event data are accessed at runtime through the `statsbombpy` library;
no raw event data is committed to this repository.

---

## License

This repository is released under the MIT License. See `LICENSE` for details.

The StatsBomb Open Data is subject to its own licensing terms, available at the
StatsBomb open-data repository.

---

## Citation

If you use this code or build on this work, please cite:

> Domingo Grifell, Biel. (2026). *Identification and Tactical Analysis of Football
> Playing Styles through Machine Learning and Spatiotemporal Event Data.*
> Bachelor's Thesis, Universitat Pompeu Fabra.

---

## Acknowledgements

I would like to thank my supervisor, Javier Segovia Aguas, for his guidance
throughout the project, and the StatsBomb team for making high-quality football
event data openly available to the research community.
