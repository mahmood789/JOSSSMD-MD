---
# IMPORTANT: Update Title, Authors, Affiliations, Date, and Bibliography file name.
title: '786MIII MD/SMD MetaAnalysis: An Interactive Dashboard for Continuous Outcome Meta-Analysis in R'
tags:
  - R
  - Shiny
  - meta-analysis
  - systematic review
  - evidence synthesis
  - continuous outcomes
  - standardized mean difference
  - mean difference
  - visualization
  - research software
authors:
  # List authors who meet JOSS contribution criteria
  - name: Mahmood Ahmad
   
  - name: Abdullahi Noori # Correct spelling if needed
  
  - name: Parichatra Homhuan

  - name: Manpreet Kour
  - 
affiliations:
 -Royal Free Hospital, London, UK
# Add more affiliations if needed
date: 22 April 2025 # Set to submission date


---

# Summary

We developed `786MIIISMD-MD`, an R [@RCoreTeam] Shiny [@RShiny] application to simplify conducting meta-analyses of continuous outcomes. Researchers working with data reported as means, standard deviations, and sample sizes can use this tool to calculate pooled Mean Differences (MD) or Standardized Mean Differences (SMD), such as Hedges' g [@Hedges1985]. The app provides an interactive platform to generate forest plots, assess heterogeneity ($I^2$, $\tau^2$), check for publication bias using various tests (e.g., Egger's test [@Egger1997]) and funnel plot variations, explore heterogeneity through meta-regression, subgroup analysis, and sensitivity analyses. It integrates core functionalities from established packages like `meta` [@metaPackage], `metafor` [@metaforPackage], `dmetar` [@dmetarPackage], and `bayesmeta` [@bayesmetaPackage] within an accessible dashboard environment, facilitating both analysis and visualization for evidence synthesis.

# Statement of Need

Performing a thorough meta-analysis involves numerous steps beyond calculating a pooled effect size. Researchers need to assess heterogeneity, investigate potential publication bias, potentially explore moderators through meta-regression, and conduct sensitivity analyses. While R offers excellent packages for these tasks, navigating the different functions and synthesizing the results requires considerable coding effort and statistical understanding. This can be a hurdle, especially for those primarily focused on the clinical or biological aspects of a systematic review, or for students learning these methods.

`786MIIISMD-MD` aims to lower this barrier for continuous outcome data (means/SDs). We wanted a tool that allows users to:
* Upload their data easily in a standard format.
* Quickly calculate and visualize the main meta-analysis results (SMD or MD).
* Immediately access and explore standard checks for heterogeneity and publication bias through integrated plots and tests.
* Perform common advanced analyses like meta-regression, subgroup analysis, and cumulative analysis without writing custom code.
* Easily customize and download publication-quality plots and results tables.

By bringing these components together in an interactive dashboard, `MetaAnalysisApp` allows researchers to focus more on interpreting the results and exploring the robustness of their findings, making the process more efficient and accessible.

# Functionality

The application interface, built with `bs4Dash` [@bs4Dash], uses a sidebar to navigate between different analysis stages.

**Workflow:**
Users typically start by uploading a CSV file containing `author`, `meanintervention`, `sdintervention`, `totalintervention`, `meancontrol`, `sdcontrol`, `totalcontrol`, and optional columns like `year`, `subgroup`, or moderators (`Reg`, `Reg2`, `Reg3`). On the "Data & Options" tab, they select the effect measure (SMD or MD), relevant methods (e.g., SMD type like Hedges' g, heterogeneity estimator like REML), and the meta-analysis model (Fixed or Random Effects).

Key analysis modules include:

* **Meta-Analysis Results:** Presents the core output from `meta::metacont`, including the pooled effect (SMD or MD), confidence interval, $I^2$, $\tau^2$, and Q-test results.
* **Forest Plots:** Displays forest plots using `meta::forest` in standard, JAMA, and RevMan5 styles, with customization options. Alternative visualizations like Drapery, Radial, Beeswarm (`ggbeeswarm` [@ggbeeswarm]), and L'Abbé plots are also provided for exploring the data.
* **Publication Bias:** Offers tools to assess bias, including funnel plots (`meta::funnel`), trim-and-fill analysis (`meta::trimfill`), limit meta-analysis (`meta::limitmeta`), P-curve analysis (`dmetar::pcurve`), and results from Egger's and Begg's tests (`meta::metabias`).
* **Heterogeneity & Influence:** Summarizes heterogeneity statistics ($I^2$, $\tau^2$) and provides diagnostic plots via `dmetar::InfluenceAnalysis`, such as Baujat plots [@Baujat2002] and leave-one-out plots showing changes in the effect estimate and $I^2$. Numerical leave-one-out results from `meta::metainf` are also available.
* **Meta-Regression:** Allows investigation of continuous moderators (`Reg`, `Reg2`, `Reg3`) using `meta::metareg`. Includes results tables, bubble plots (`meta::bubble`), moderator correlation checks (`PerformanceAnalytics` [@PerformanceAnalytics]), and basic residual plots.
* **Advanced Analyses:** Facilitates cumulative meta-analysis (`meta::metacum`), subgroup analysis (`meta::metabin` with `byvar`), and Bayesian meta-analysis (`bayesmeta::bayesmeta`).

Users can download plots as PNG files and numerical results as text files throughout the app.

# Availability

**Operating system:** Platform independent (requires R).
**Programming language:** R (>= 4.0 recommended)
**Dependencies:** shiny, bs4Dash, meta, dmetar, metafor, ggplot2, ggbeeswarm, fontawesome, shinyjs, dplyr, magrittr, bayesmeta, PerformanceAnalytics. *(Optional: car)*.
**Installation & Reproducibility:** Includes an `renv.lock` file [@renv] allowing for reproducible dependency installation via `renv::restore()`. See README for details.
**License:** Apache License 2.0.
**Source Code Repository:** https://github.com/mahmood789/JOSSSMD-MD
**Archived Version:** 
# Acknowledgements

We thank the Ahmadiyya Muslim Research Association and Luciano Candilio for their support. 

# References

*(References are managed in the paper.bib file)*
