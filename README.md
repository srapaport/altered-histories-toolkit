# History Alterations - Replication Package

This repository contains the complete replication package for the research article *Altered Histories in Version Control System Repositories: Evidence from the Trenches*. The package provides tools to detect, analyze, and categorize Git history alterations across software repositories, along with Jupyter notebooks to reproduce the analysis presented in the paper.

## 📋 Table of Contents

- [Overview](#overview)
- [Repository Structure](#repository-structure)
- [Quick Start](#quick-start)
- [Reproducing the Analysis](#reproducing-the-analysis)
- [Data](#data)
- [Tools Description](#tools-description)
- [Requirements](#requirements)
- [Citation](#citation)

## 🔍 Overview

This replication package enables researchers to reproduce the analysis of altered Git histories in software repositories archived by [Software Heritage](https://www.softwareheritage.org/). The study investigates how and why Git histories are modified over time, providing insights into developer practices and repository maintenance patterns.

**Main Research Questions:**

- How prevalent are Git history alterations in open-source repositories?
- What types of changes are most commonly made to Git histories?
- What are the root causes of these alterations?
- How do these practices vary across different types of repositories?

## 📁 Repository Structure

```
├── README.md                    # This file
├── data/                        # Pre-computed datasets
│   ├── ...
├── altered-history/             # Main analysis tool
│   ├── src/                     # Rust source code
│   ├── notebooks/               # Analysis notebooks
│   │   ├── analysis.ipynb       # Main analysis notebook
│   │   ├── build_analysis_dataset.ipynb
│   │   └── utils_analysis.py    # Analysis utilities
│   └── README.md
├── git-historian/               # History checking tool
│   ├── src/                     # Rust source code
│   └── README.md
├── modified-files/              # File modification analysis tool
│   ├── src/                     # Rust source code
│   ├── notebooks/               # Additional analysis notebooks
│   │   ├── license_analysis.ipynb
│   │   ├── license_categorization.py
│   │   ├── secret-analysis.ipynb
│   │   └── swh_license_files.py
│   └── README.md
```

## 🚀 Quick Start

### Prerequisites

- **Rust** (latest stable version)
- **Python 3.8+** with Jupyter
- **PostgreSQL** (for database operations)
- **Git** (for repository analysis)

### Installation

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd altered-histories-tool-replication-pkg
   ```

2. **Unzip all directories**

3. **Install Python dependencies:**
   ```bash
   pip install pandas matplotlib seaborn jupyter plotly numpy
   ```

4. **Build the Rust tools (optional, for dataset generation):**
   ```bash
   cd altered-history && cargo build --release && cd ..
   cd git-historian && cargo build --release && cd ..
   cd modified-files && cargo build --release && cd ..
   ```

## 📊 Reproducing the Analysis

### Option 1: Using Pre-computed Data (Recommended)

The `data/` directory contains pre-computed datasets that allow you to reproduce all analyses without running the computationally intensive data collection process. It can be found on Zenodo: https://doi.org/10.5281/zenodo.15558282

1. **Open the main analysis notebook:**
   ```bash
   cd altered-history/notebooks
   jupyter notebook analysis.ipynb
   ```

2. **Run all cells** to reproduce the complete analysis.

3. **Explore additional analyses:**

    Modify notebooks at will to explore the dataframe.
   ```bash
   # Build analysis dataset (shows data preparation)
   jupyter notebook build_analysis_dataset.ipynb
   
   # License-related analysis
   cd ../../modified-files/notebooks
   jupyter notebook license_analysis.ipynb
   
   # Security and secrets analysis
   jupyter notebook secret-analysis.ipynb
   ```

### Option 2: Regenerating the Dataset

To reproduce the complete data collection and analysis pipeline:

1. **Download Software Heritage datasets** (see individual tool READMEs)
2. **Configure database connections** in each tool
3. **Run the analysis pipeline** following the step-by-step instructions in each tool's README
4. **Process results** using the provided notebooks

**Note:** Complete dataset regeneration requires significant computational resources and time (potentially weeks for large datasets).

## 📋 Data

The `data/` directory contains several key datasets including:

- **`res.pkl`**: Main analysis results containing categorized alterations
- **`stars_without_dup.pkl`**: Repository popularity metrics (GitHub stars)
- **`visit_type.pkl`**: Classification of repository visit patterns
- **`altered_histories_2024_08_23.dump`**: PostgreSQL database dump for git-historian tool

## 🛠️ Tools Description

### 1. altered-history

**Purpose:** Detects and categorizes Git history alterations in Software Heritage archives.

**Key Features:**

- Three-step analysis pipeline (detection → root cause → categorization)
- Parallel processing for large datasets
- Comprehensive alteration taxonomy

**Usage:** See `altered-history/README.md` for detailed instructions.

### 2. git-historian

**Purpose:** Checks individual repositories against the database of known alterations.

**Key Features:**

- PostgreSQL integration
- Git hook integration for automated checking
- Caching system for performance

**Usage:** See `git-historian/README.md` for detailed instructions.

### 3. modified-files

**Purpose:** Analyzes file-level modifications and their patterns.

**Key Features:**

- File modification tracking
- License and security analysis
- Integration with Software Heritage graph

**Usage:** See `modified-files/README.md` for detailed instructions.

## 📋 Requirements

### System Requirements

- **Memory:** Minimum 16GB RAM (1.5TB+ recommended for full dataset processing)
- **Storage:** 600GB+ free space for complete datasets
- **CPU:** Multi-core processor recommended for parallel processing

## 🔄 Reproducibility Notes

1. **Deterministic Results:** The analysis notebooks will produce identical results when run with the provided datasets.

2. **Versioning:** All tools are pinned to specific versions to ensure reproducibility.

3. **Random Seeds:** Where applicable, random seeds are fixed in the analysis code.
