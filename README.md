# Where Is the Chokepoint? A Network Analysis of Southeast Asian Sexual-Exploitation Flows

Benjamin Summerlin | GEOG 594A GEOINT capstone, Penn State | August 2026

Portfolio page: https://bensummerlin-gis.github.io/trafficking-network.html

## Problem

Anti-trafficking resources are limited, and the countries that could receive them are not interchangeable. This project asks one question: which Southeast Asian country, if any, is the primary chokepoint in the regional sexual-exploitation network, and what explains its position?

## Data

- **CTDC Global Synthetic Dataset**, 2026 release (Counter-Trafficking Data Collaborative, hosted by IOM): 268,515 records, 2002 to 2024. The dataset is synthetic. It is generated under differential privacy (epsilon 12) to protect individuals while keeping population-level patterns. **It is not included here.** See [data/README.md](data/README.md) for where to download it.
- Scope: sexual exploitation only. A record is included if one of seven Southeast Asian origin countries (Cambodia, Indonesia, Laos, Myanmar, the Philippines, Thailand, Vietnam) is its origin or its destination. Domestic records, where origin and destination are the same country, are taken out of the network and reported separately.
- The resulting network has 1,271 cross-border records, 71 countries and 158 corridors.

All results are at the country level. CTDC records only an origin and a destination for each case, with no transit country, so network position here is a structural measure, not a claim about the route any victim travelled.

## Method in plain terms

1. **Build the network.** Each country is a node, and each origin-to-destination pair is a directed corridor weighted by its number of records.
2. **Betweenness centrality.** This counts how often a country sits on the shortest paths between other countries, which is one way to state "chokepoint" in math. It is computed both with and without corridor volume.
3. **Stress tests.** Each origin country is removed in turn to see how much the network breaks apart, and a cut-vertex test finds the countries whose removal splits the network.
4. **Community detection (Louvain).** This finds groups of countries that are more tightly linked to each other than to the rest of the network.
5. **Structured analysis.** Five competing hypotheses, one per candidate country, are tested against political, economic, social and infrastructure evidence using Analysis of Competing Hypotheses.

## Key findings (from the paper)

- **No single dominant chokepoint.** Cambodia (weighted betweenness 0.1716) and Thailand (0.1653) are co-central. Indonesia, Vietnam and the Philippines complete a leading five, the same five under either weighting.
- **Three methods agree.** Betweenness, node removal and the cut-vertex test single out the same five countries. Exactly five countries are cut vertices: Cambodia, Indonesia, the Philippines, Thailand and Vietnam.
- **Thailand is the best-supported transit candidate.** It has no inconsistencies in the hypothesis matrix, and none of its records with a recorded destination are domestic.
- **Most Cambodian trafficking never crosses a border.** 678 Cambodian records are domestic, 90.6% of the 748 with a recorded destination.
- **Volume is not position.** Vietnam has the most records (518) but ranks fifth on unweighted betweenness. The United States receives 348 records but has a betweenness of 0.0098.
- **Interdiction and prevention reach different populations.** The country where cross-border interdiction would have the most structural effect is not the country carrying the most harm.

## Notebooks

Run them in this order. Each one writes its tables to `outputs/` for the next.

| Notebook | Paper appendix | What it does |
|---|---|---|
| `A_network_construction_and_centrality.ipynb` | Appendix A | Filters the data, builds the corridor network, computes betweenness and degree, the domestic vs cross-border split, transitivity and path lengths. |
| `D_demographic_analysis.ipynb` | Appendix D | Gender and age shares for five origin countries, computed over records with a known value. |
| `B_structural_tests_and_figures.ipynb` | Appendix B (also part of D) | Node-removal simulation, cut-vertex test, Louvain communities, node-link graph, origin-destination matrix, missing-destination chart, volume vs betweenness charts, and the seven-country demographic composition chart. It also keeps a null-model test (A3) that was completed but left out of the paper, labeled as such. |
| `C_country_set_robustness.ipynb` | Appendix C | Re-runs centrality with all eleven Southeast Asian states. |
| `E_flow_map_geometry.ipynb` | Appendix E | Builds straight corridor lines between country centroids for the flow map, which was styled in ArcGIS Pro. |

## How to run

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
# put the CTDC CSV in data/ (see data/README.md)
jupyter notebook
```

Then run A, D, B, C and E in that order. Notebook E also needs the country centroid table described in `data/README.md`.

## Requirements

Python 3.10 or newer, with pandas, networkx, numpy, matplotlib, seaborn, geopandas, shapely, pyogrio and pyproj (see `requirements.txt`). The original analysis ran on pandas 2.3.3, networkx 3.5 and geopandas 1.1.4.

## Data credit

Source: Counter-Trafficking Data Collaborative (CTDC), May 2026. https://www.ctdatacollaborative.org/page/global-synthetic-dataset. Used under the CTDC terms of use (https://www.ctdatacollaborative.org/page/terms-use) for non-commercial research. CTDC and IOM do not endorse this analysis.

## Use of AI

An AI assistant helped with analysis code, figures, drafting and editing. All analytic decisions, interpretations and conclusions are my own, and I reviewed and verified all output.
