# pguIMP: Visually Guided Preprocessing of Bioanalytical Laboratory Data

<!-- badges -->
[![CRAN status](https://www.r-pkg.org/badges/version/pguIMP)](https://cran.r-project.org/package=pguIMP)
[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

## Overview

**pguIMP** is an R package that provides a comprehensive, interactive pipeline for reproducible preprocessing and cleaning of bioanalytical laboratory data. Developed in collaboration between data scientists and bioanalytical diagnostics experts, pguIMP enables field experts and researchers to prepare high-dimensional bioanalytical data for machine learning and advanced statistical analysis without requiring programming expertise.

The package implements a fixed sequence of preprocessing steps within an intuitive Shiny-based graphical user interface, ensuring reproducible and traceable data preprocessing workflows.

## Purpose of pguIMP?

Data preprocessing is critical for the success of machine learning and statistical analyses of biomedical data. The evaluation of bioanalytical data by classical statistics, machine learning approaches, or pharmacokinetic-pharmacodynamic modeling depends heavily on data quality. However, most available preprocessing tools either:

- Require programming skills (limiting accessibility)
- Are limited to simple statistical methods (mean/median imputation)
- Lack interactive visualization for quality control
- Don't provide reproducible pipelines with full audit trails

**pguIMP solves these problems** by offering:

✓ **Interactive Graphical Interface** – No programming required  
✓ **Machine Learning Methods** – Advanced imputation and outlier detection  
✓ **Visual Validation** – Real-time visualization of preprocessing results  
✓ **Reproducibility** – Complete documentation of all preprocessing decisions  
✓ **Flexibility** – Choose from multiple algorithms for each preprocessing step  
✓ **Traceability** – Full audit trail with seed values and session reports  

## Key Features

### Data Visualization
- **Distribution Analysis**: Scatter plots, box plots, histograms, probability density function (PDF) plots
- **Normality Assessment**: Quantile-Quantile (Q-Q) plots, Shapiro-Wilk and Lilliefors' Kolmogorov-Smirnov tests
- **Specialized Methods**: Pareto density estimation for detecting subgroup structures

### Data Transformation
- **Tukey's Ladder of Powers** – Systematic power transformations (log, square root, etc.)
- **Box-Cox Transformation** – Optimal power transformation for normality
- **Standard Transformations**: Binary logarithm (log₂), natural logarithm (ln), common logarithm (log₁₀)
- **Automated Testing**: Statistical evaluation of transformation effectiveness

### Data Normalization
- Minimum-Maximum normalization
- Mean normalization
- Z-score normalization

### Outlier Detection
- **Statistical Methods**: Grubb's test for outliers
- **Machine Learning Methods**:
  - DBSCAN (Density-Based Spatial Clustering of Applications with Noise)
  - One-class Support Vector Machine (SVM)
  - k-Nearest Neighbors (kNN)

### Missing Value Imputation
- **Simple Substitution**: Mean or median replacement
- **Machine Learning-Based Imputation**:
  - k-Nearest Neighbors (kNN)
  - Predictive Mean Matching (PMM)
  - Classification and Regression Trees (CART)
  - M5P (Model Tree)
  - Random Forests
- **Missing Data Analysis**: Detection of Missing Completely At Random (MCAR) vs Not At Random (NMAR)

### Integration with Limits of Quantification (LOQ)
- Separate treatment of values below detection/quantification limits
- Distinction between different missing data mechanisms
- Preservation of analytical integrity

## Installation

### From CRAN (Recommended)

```r
install.packages("pguIMP")
```

### Development Version from GitHub

```r
# Install remotes package if needed
if (!requireNamespace("remotes", quietly = TRUE))
  install.packages("remotes")

# Install development version
remotes::install_github("JornLotsch/pguIMP")
```

## Quick Start

### Launch the Interactive Application

```r
library(pguIMP)

# Launch the Shiny-based web interface
pguIMP::pguIMP()
```

This opens an interactive graphical interface where you can:
1. **Upload** your bioanalytical data (CSV, Excel, or other formats)
2. **Explore** the data structure and distributions
3. **Transform** skewed variables to normality
4. **Detect and Handle** outliers using statistical or ML methods
5. **Impute** missing values using advanced techniques
6. **Normalize** your preprocessed data
7. **Validate** results with comprehensive visualizations
8. **Export** preprocessed data and detailed preprocessing reports

### Using the API in R Scripts

```r
library(pguIMP)

# Load your data
data <- read.csv("your_data.csv")

# Create a data object
pgu_data <- pgu.data(data)

# Transform variables (example: log transformation)
transformed <- pgu.transformator(pgu_data, method = "log")

# Impute missing values using kNN
imputed <- pgu.imputation(transformed, method = "knn")

# Normalize the data (example: z-score)
normalized <- pgu.normalizer(imputed, method = "zscore")

# Export results
pgu.exporter(normalized, file = "preprocessed_data.csv")
```

## Main Functions

| Function | Purpose |
|----------|---------|
| `pguIMP()` | Launch interactive Shiny application |
| `pgu.data()` | Create and initialize data object |
| `pgu.explorer()` | Explore data distributions and structure |
| `pgu.transformator()` | Apply data transformations |
| `pgu.normalizer()` | Normalize/scale data |
| `pgu.outliers()` | Detect outliers using various methods |
| `pgu.imputation()` | Impute missing values |
| `pgu.limitsOfQuantification()` | Handle values below LOQ separately |
| `pgu.validator()` | Validate preprocessing results |
| `pgu.exporter()` | Export preprocessed data and reports |
| `pgu.reporter()` | Generate comprehensive preprocessing reports |

## Evaluation & Scientific Validation

pguIMP has been rigorously evaluated on real bioanalytical datasets from:

- **Lipidomics**: Plasma lipid mediators and endogenous metabolites
- **Pharmacogenetics**: Drug metabolite measurements in urine
- **Mass Spectrometry**: High-dimensional LC-MS lipidomic data

Results demonstrate that:

✓ Machine learning-based imputation methods (kNN, Random Forests) significantly outperform simple mean/median substitution, especially for Not-At-Random missing data  
✓ Proper preprocessing improves downstream clustering accuracy and biomarker identification  
✓ The pguIMP pipeline preserves data structure better than alternative approaches  
✓ Integration into machine learning workflows enhances model performance  

## Citation

If you use pguIMP in your research, please cite the following publication:

> Malkusch, S., Hahnefeld, L., Gurke, R., & Lötsch, J. (2021).
> Visually guided preprocessing of bioanalytical laboratory data using an interactive R notebook (pguIMP).
> *Clinical and Translational Science*, 14(6), 2213-2224.
> https://doi.org/10.1111/cts.13089

**Full Paper**: [PDF available on PubMed Central](https://pmc.ncbi.nlm.nih.gov/articles/PMC8592507/pdf/PSP4-10-1371.pdf)

```bibtex
@article{Malkusch2021,
  title={Visually guided preprocessing of bioanalytical laboratory data using an interactive {R} notebook ({pguIMP})},
  author={Malkusch, Sebastian and Hahnefeld, Lisa and Gurke, Robert and L{\"o}tsch, J{\"o}rn},
  journal={Clinical and Translational Science},
  volume={14},
  number={6},
  pages={2213--2224},
  year={2021},
  doi={10.1111/cts.13089}
}
```

## System Requirements

- **R**: Version 3.6.0 or higher
- **Operating System**: Windows, macOS, or Linux
- **Memory**: 4 GB RAM recommended for large datasets
- **Dependencies**: Automatically installed with the package (see DESCRIPTION file)

## Documentation

- **CRAN Documentation**: [https://cran.r-project.org/package=pguIMP](https://cran.r-project.org/package=pguIMP)
- **Package Manual**: Available via `help(pguIMP)` after installation
- **Function Help**: Access specific function documentation with `?function_name()`

## Authors

**Core Development Team:**
- **Sebastian Malkusch** – Primary programming and implementation (https://orcid.org/0000-0001-6766-140X)
- **Jörn Lötsch** – Project supervision and current maintainer (https://orcid.org/0000-0002-5818-6958)

**Contributing Authors:**
- Lisa Hahnefeld
- Robert Gurke

For questions or issues, please contact the maintainer

## License

This project is licensed under the **GNU General Public License v3.0 or later (GPL ≥ 3)**.

See the [LICENSE](LICENSE) file for details.

## Bug Reports & Contributing

- **Report Bugs**: [GitHub Issues](https://github.com/JornLotsch/pguIMP/issues)
- **Source Code**: [GitHub Repository](https://github.com/JornLotsch/pguIMP)
- **CRAN Page**: [https://cran.r-project.org/package=pguIMP](https://cran.r-project.org/package=pguIMP)

## Funding

This work was funded by the **Landesoffensive zur Entwicklung wissenschaftlich-ökonomischer Exzellenz (LOEWE)**, specifically the **LOEWE-Zentrum für Translationale Medizin und Pharmakologie** (J.L.), through the project "Reproducible Cleaning of Biomedical Laboratory Data Using Methods of Visualization, Error Correction and Transformation Implemented as Interactive R-Notebooks."

The funders had no role in method design, data selection and analysis, decision to publish, or preparation of the manuscript.

## Acknowledgments

pguIMP was developed in close collaboration between:
- Data scientists
- Experts in bioanalytical diagnostics
- The R/Bioconductor community

The package implements contemporary data processing and machine learning methods while maintaining a focus on usability for domain experts without programming expertise.

## References

Key references for methods implemented in pguIMP:

1. Tukey's Ladder of Powers for data transformation
2. Box-Cox power transformation
3. Grubb's test for outlier detection
4. DBSCAN for density-based clustering
5. k-Nearest Neighbors (kNN) imputation
6. Predictive Mean Matching (PMM) for missing data
7. Classification and Regression Trees (CART)
8. Random Forest algorithms

---

**Last Updated**: February 2026  
**Package Version**: Check DESCRIPTION file for current version
