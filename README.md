
# MetaAnalysisApp: Meta-Analysis Dashboard for Continuous Outcomes (SMD/MD)

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE.md)
**An Interactive R Shiny Application for Meta-Analysis of Continuous Data (Standardized Mean Difference / Mean Difference)**

## Overview

This application provides a comprehensive, interactive dashboard designed to streamline the process of conducting meta-analyses for **continuous outcome data** (e.g., comparing means between intervention and control groups). Users can upload study data (mean, standard deviation, and sample size per group) in CSV format and perform a wide range of analyses using the `meta` R package [@metaPackage] as the primary engine.

Key functionalities include:

* Calculating pooled effect sizes, primarily Standardized Mean Difference (SMD) or Mean Difference (MD), using various methods.
* Generating publication-quality forest plots (Standard, JAMA, RevMan5 styles) with customization options.
* Assessing publication bias through funnel plots and associated statistical tests (e.g., Egger's test [@Egger1997], P-curve [@Simonsohn2014]).
* Evaluating statistical heterogeneity using measures ($I^2$, $\tau^2$, Q-statistic) and diagnostic plots (e.g., Baujat [@Baujat2002], Influence plots).
* Performing meta-regression to explore potential sources of heterogeneity using study-level moderators.
* Conducting subgroup and cumulative meta-analyses.
* Running sensitivity analyses (Leave-One-Out).
* Performing Bayesian meta-analysis.

The tool aims to make these standard and advanced meta-analysis techniques accessible through a user-friendly graphical interface built with R [@RCoreTeam], Shiny [@RShiny], and `bs4Dash` [@bs4Dash], leveraging robust backend packages like `metafor` [@metaforPackage], `dmetar` [@dmetarPackage], and `bayesmeta` [@bayesmetaPackage] for specific calculations and diagnostics.

## Features

* **Data Import:** Upload study data via CSV file.
* **Effect Measures:** Choose between Standardized Mean Difference (SMD) and Mean Difference (MD).
* **Analysis Methods:**
    * Select SMD calculation method (Hedges' g, Cohen's d, Glass' delta) when using SMD.
    * Choose heterogeneity estimator (REML, PM, DL, EB, SJ).
    * Select Fixed Effect or Random Effects model.
* **Forest Plots:**
    * Standard forest plot with prediction interval.
    * JAMA-style forest plot.
    * RevMan5-style forest plot.
    * Customizable appearance (colors, labels, text size).
    * Alternative visualizations: Drapery plot, Radial (Galbraith) plot, Beeswarm plot (`ggbeeswarm` [@ggbeeswarm]), L'Abbé plot (less common for continuous data).
* **Publication Bias Assessment:**
    * Standard and contour-enhanced funnel plots.
    * Trim and Fill analysis and plot.
    * Limit Meta-Analysis (standard and shrunken) plots.
    * Egger's regression test and Begg's rank test output.
    * P-curve analysis and plot.
    * Albatross plot (sample size vs. significance).
* **Heterogeneity & Influence Analysis:**
    * Text summary ($I^2$, $\tau^2$, Q-statistic).
    * Baujat plot.
    * Influence diagnostics plots (overall influence, effect size change, I² change via `dmetar`).
    * Leave-One-Out analysis results (`meta::metainf`).
    * Outlier detection (`meta::find.outliers`).
* **Meta-Regression:**
    * Perform meta-regression with up to three continuous moderator variables (columns named `Reg`, `Reg2`, `Reg3`).
    * Bubble plots (`meta::bubble`) for visualizing moderator effects.
    * Moderator correlation plots (`PerformanceAnalytics` [@PerformanceAnalytics]) and matrix.
    * Basic diagnostic outputs (Residual plot, AIC/BIC for single moderator model).
* **Advanced Analyses:**
    * Cumulative meta-analysis (requires `year` column).
    * Subgroup analysis (requires `subgroup` column).
    * Bayesian meta-analysis (using `bayesmeta`).
* **Visualization & Export:**
    * Interactive plots within the dashboard.
    * Download options for all generated plots (PNG format) and analysis results (TXT format).

## Installation

**Prerequisites:**

* R (version 4.0 or later recommended).
* RStudio (Recommended IDE, but not strictly required).

**Steps:**

1.  **Clone the Repository:**
    ```bash
    git clone [Link to Your Repository, e.g., [https://github.com/your_username/MetaAnalysisAppSMD.git](https://github.com/your_username/MetaAnalysisAppSMD.git)]
  

2.  **Install Dependencies:**
    This project uses `renv` for package management to ensure reproducibility.

    * Open the project in RStudio or navigate to the project directory in your R console.
    * Run the following command in the R console to install all required packages from the `renv.lock` file (if provided):
        ```R
        renv::restore()
        ```
    * **Note:** Key dependencies include `shiny`, `bs4Dash`, `meta`, `dmetar`, `metafor`, `bayesmeta`, `ggplot2`, `ggbeeswarm`, `dplyr`, `magrittr`, `shinyjs`, `fontawesome`, `PerformanceAnalytics`. Ensure these are installed if not using `renv`. Bayesian analysis requires `bayesmeta`. VIF calculation (optional, mentioned in code comments) requires `car`.

## Usage

1.  **Launch the Application:**
    Open R/RStudio in the project directory and run:
    ```R
    shiny::runApp()
    ```
    This will launch the Meta-Analysis Dashboard in your default web browser.

2.  **Prepare Input Data:**
    * Create a CSV file containing your study data.
    * **Required Columns:**
        * `author` (character): Unique study identifier (e.g., Smith 2020).
        * `meanintervention` (numeric): Mean of the outcome in the intervention group.
        * `sdintervention` (numeric): Standard deviation of the outcome in the intervention group.
        * `totalintervention` (numeric): Number of participants in the intervention group (used as `n.e`).
        * `meancontrol` (numeric): Mean of the outcome in the control group.
        * `sdcontrol` (numeric): Standard deviation of the outcome in the control group.
        * `totalcontrol` (numeric): Number of participants in the control group (used as `n.c`).
    * **Optional Columns:**
        * `year` (numeric): Publication year for cumulative meta-analysis.
        * `subgroup` (character/factor): Grouping variable for subgroup analysis.
        * `Reg`, `Reg2`, `Reg3` (numeric): Continuous moderator variables for meta-regression.
    * *(See `sample_data_continuous.csv` in this repository for an example)*

3.  **Upload Data & Set Options:**
    * Navigate to the "Data & Options" tab.
    * Click "Browse" to upload your prepared CSV file.
    * Select the desired "Effect Measure" (SMD or MD).
    * If using SMD, select the "SMD Method" (e.g., Hedges' g).
    * Choose the "Heterogeneity Estimator" and "Effect Model" (Random/Fixed).
    * Adjust Plotting Options as needed (ranges, colors, etc.).
    * If performing meta-regression, select a moderator for the default Bubble Plot display.

4.  **Explore Results:**
    * Use the sidebar menu to navigate through different analysis tabs.
    * View generated plots and statistical outputs in the main panel.
    * Use the download buttons to save plots (PNG) and text results (TXT).

## Sample Data

A sample CSV file (`sample_data_continuous.csv`) is included in this repository to demonstrate the required data format and allow testing of the application's features.

## Contributing

Contributions are welcome! 


## Authors

* Mahmood Ahmad, MBBS
* Abdullahi Noori, MBBS
* Parichatra Homhuan, MBBS
* Manpreet Kour, MBBS

*(Ensure all listed authors meet JOSS contribution criteria)*

## Acknowledgements

We acknowledge the support and encouragement from the Ahmadiyya Muslim Research Association and Luciano Candilio.

## License

This project is licensed under the Apache License, Version 2.0 - see the [LICENSE.md](LICENSE.md) file for details. *(Ensure LICENSE.md exists and contains the Apache 2.0 text)*

## Citation

If you use this software in your research, please cite it as follows:


> Ahmad M., Noori A., Homhuan P., Kour M. (2025). MetaAnalysisApp: An Interactive R Dashboard for Continuous Outcome Meta-Analysis. *Journal of Open Source Software*, [Volume]([Issue]), [ArticleNumber]. [https://doi.org/[JOSS_DOI]]()



Underlying R packages used for the analysis, particularly `meta` [@metaPackage], `metafor` [@metaforPackage], `dmetar` [@dmetarPackage], and `bayesmeta` [@bayesmetaPackage], `ggplot2` [@ggplot2], `ggbeeswarm` [@ggbeeswarm] as appropriate. Refer to the documentation of these packages for their preferred citation formats (e.g., using `citation("meta")` in R).
