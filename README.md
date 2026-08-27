# Spatiotemporal-Exposure-Analysis

**Spatiotemporal Analysis of Air Pollution Exposure Disparities by Race/Ethnicity and Historical Redlining in the Contiguous United States, 2000-2010**

---

**Authors:** Mohsen Nikfarjam and Ehsan Nikfarjam

*Equal co-authorship. Both authors share intellectual responsibility for the project; lead roles are described under [Attribution](#attribution).*

**Date:** 2025-2026

---

## Overview

This project assembles and analyzes a national-scale, analysis-ready panel dataset linking empirically modeled air pollution concentration surfaces - nitrogen dioxide (NO₂) and fine particulate matter (PM₂.₅), decomposed by spatial scale into long-range, mid-range, neighborhood, and near-source components - to U.S. decennial census demographics and digitized Home Owners' Loan Corporation (HOLC) redlining boundaries across more than three million census blocks nationwide.

The analysis quantifies air pollution exposure disparities by race/ethnicity and historical redlining grade at two decennial time points (2000 and 2010), applying population-weighted exposure metrics, inequality indices (Gini index, Atkinson index), and health impact assessment (HIA) to characterize how the pollution burden is distributed across demographic groups and HOLC security grades.

**Headline finding:** 2010 population-weighted NO₂ averaged 16.8 parts per billion (ppb) in HOLC Grade D neighborhoods versus 10.7 ppb in Grade A, with racial and ethnic disparities persisting within every redlining grade - indicating that redlining history alone does not account for the exposure gap.

Nationally, population-weighted NO₂ fell 39 percent (14.63 to 8.93 ppb) and population-weighted PM₂.₅ fell 29 percent (13.27 to 9.44 ug/m<sup>3</sup>) between 2000 and 2010, so the disparities above persist against a background of substantial overall improvement.

Findings are translated into two public-facing ArcGIS StoryMaps (one per author) and a co-authored technical report for non-technical policymakers and regulatory audiences.

---

## Methods

| Component | Detail |
|---|---|
| **Exposure data** | Scale-decomposed NO₂ and PM₂.₅ concentration surfaces (long-range, mid-range, neighborhood, near-source components), third-party empirical models; not produced by this project |
| **Geographic unit** | U.S. census block (3+ million blocks, contiguous United States) |
| **Time points** | 2000 and 2010 (U.S. decennial census years) |
| **Demographic linkage** | U.S. decennial census demographics by race and ethnicity |
| **Redlining linkage** | Digitized HOLC security-grade polygons (1930s to 1940s) |
| **Exposure metrics** | Population-weighted mean NO₂ and PM₂.₅ concentrations, with confidence intervals and weighted quantiles, by demographic group and HOLC grade |
| **Inequality metrics** | Weighted Gini index, Atkinson index, generalized entropy, Theil index, Lorenz curves, disparity ratios, representation ratios; intersectional stratification by race/ethnicity and redlining grade |
| **Health impact assessment** | Concentration-response functions applied to estimate PM₂.₅-attributable premature mortality (all-cause) across racial and ethnic subpopulations |
| **Computation** | Memory-optimized chunked CPU workflow: dtype downcasting, 1,000,000-row chunks, datashader rendering with ProcessPool parallelism |
| **Tools** | Python (GeoPandas, NumPy, SciPy, Pandas), ArcGIS Pro, ArcGIS StoryMaps |

---

## Scope and Limitations

Stated explicitly because each one bounds how the results above should be read.

- **Spatial scale is not emission source category.** The decomposition resolves distance scale (long-range, mid-range, neighborhood, near-source). It does not identify wildfire versus dust versus traffic. Reading a scale as a source type is a proxy interpretation, and this project treats it as one; validating that proxy against source-specific emission inventories is future work, not a result here.
- **Effective sample size.** Three million census blocks are not three million independent observations. Strong spatial autocorrelation means the effective sample size is far below n, so confidence intervals computed under an independence assumption, as those reported here are, are too narrow.
- **Observational design.** All findings are associations. No causal identification strategy is applied, and no regression adjustment is performed; the disparity statistics are stratified descriptive comparisons and distributional indices.
- **Prediction error is not propagated.** The concentration surfaces are modeled estimates with their own uncertainty, which is not carried through into the disparity statistics.
- **Two time points.** 2000 and 2010 only. No intervening trend is estimated and no climate-driven trend is measured.
- **Income is not included.** The decennial census does not publish income at block level, so no income variable enters this analysis.

---

## Data Availability

None of the three input datasets is redistributable, and none is included in this repository. Each is available directly from its provider under that provider's terms:

| Source | Provider | Citation |
|---|---|---|
| NO₂ and PM₂.₅ scale-decomposed surfaces | CACES | Kim et al. (2020), *PLOS ONE* 15(2): e0228535 |
| Census blocks, 2000 and 2010 | IPUMS NHGIS | Manson et al. (2024) |
| HOLC security-grade polygons | Mapping Inequality | Nelson et al. (2023) |

The notebook documents the processing pipeline applied to these inputs.

---

## Repository Contents

| File | Description |
|---|---|
| `Spatiotemporal_Analysis_Overview.ipynb` | Documented Jupyter notebook: panel dataset construction, population-weighted exposure metric computation, Gini and Atkinson inequality analysis, health impact assessment (HIA), and visualization. Figures are embedded and render on GitHub without execution. |

### Viewing the notebook

The notebook renders on GitHub with all 21 figures embedded, so no setup is
needed to read it. Two alternatives, for convenience rather than necessity:

[![nbviewer](https://img.shields.io/badge/render-nbviewer-orange.svg)](https://nbviewer.org/github/Research-Portfolios/Spatiotemporal-Exposure-Analysis/blob/main/Spatiotemporal_Analysis_Overview.ipynb)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Research-Portfolios/Spatiotemporal-Exposure-Analysis/blob/main/Spatiotemporal_Analysis_Overview.ipynb)

- **nbviewer** renders it as a clean document with a linkable table of contents: https://nbviewer.org/github/Research-Portfolios/Spatiotemporal-Exposure-Analysis/blob/main/Spatiotemporal_Analysis_Overview.ipynb
- **Google Colab** opens a runnable copy in the browser, no local install: https://colab.research.google.com/github/Research-Portfolios/Spatiotemporal-Exposure-Analysis/blob/main/Spatiotemporal_Analysis_Overview.ipynb

---

## Authors

**Mohsen Nikfarjam**
GitHub: [mohsennikfarjam](https://github.com/mohsennikfarjam)

**Ehsan Nikfarjam**
GitHub: [ehsannikfarjam](https://github.com/ehsannikfarjam)

---

## Attribution

Mohsen Nikfarjam and Ehsan Nikfarjam are equal co-authors. Equal co-authorship reflects shared intellectual responsibility and approval of the work, while the paragraphs below identify the components each led.

**Mohsen Nikfarjam** led the multi-source data acquisition and integration pipeline that produced the national panel dataset. He conducted the health impact assessment (HIA), applying concentration-response functions to estimate PM₂.₅-attributable premature mortality, and led the inequality-index computation, representation ratios, and intersectional stratification by race/ethnicity and HOLC grade. He published one of the two public ArcGIS StoryMaps.

**Ehsan Nikfarjam** led the disparities methodology and criterion selection. He quantified the racial and ethnic NO₂ burden via population-weighted exposure metrics and published the other public ArcGIS StoryMap for non-technical policymakers.

The panel dataset and technical report were developed jointly, and the manuscript is being prepared jointly. Each StoryMap is individually authored, but both are built from the shared dataset.

---

## Related Outputs

- **Interactive Dashboard - ArcGIS StoryMap (Mohsen Nikfarjam):** https://storymaps.arcgis.com/stories/bfc3ffd784094ad79a5844052b5b40c1
- **Interactive Dashboard - ArcGIS StoryMap (Ehsan Nikfarjam):** https://storymaps.arcgis.com/stories/08b06dc28bf44e968a5e29ed3a913c92
- **Probabilistic well-siting MCDA analysis:** [github.com/Research-Portfolios/Well-Siting-MCDA](https://github.com/Research-Portfolios/Well-Siting-MCDA)
