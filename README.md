# Machine Learning Analysis of RNA Characteristics

This repository contains a statistical and machine learning study of RNA characteristics using the **Stanford COVID-19 RNA Vaccine** dataset.

The project investigates how classical machine learning, sequential deep learning, and graph neural network methods can be applied to RNA sequence data and experimentally measured RNA characteristics.

## Project Overview

RNA molecules can be represented in several ways, including:

* nucleotide sequences;
* statistical sequence features;
* GC-content features;
* sequential representations;
* RNA secondary-structure graphs.

This project compares several approaches for predicting RNA-related target variables and analyzes their performance using the **Mean Absolute Error (MAE)** metric.

The main objective is to examine whether combining statistical analysis with machine learning and deep learning can provide useful predictive information about RNA characteristics.

## Research Questions

The project focuses on the following questions:

1. What statistical properties characterize the RNA sequences in the dataset?
2. How are nucleotide distributions related to the target variables?
3. Can classical machine learning models predict RNA characteristics from sequence-derived features?
4. Can convolutional and recurrent neural networks improve prediction performance?
5. Does adding GC-content information improve the performance of sequence-based models?
6. Can RNA secondary structures be represented as graphs and processed using graph neural networks?
7. How do sequential and graph-based approaches compare?

## Dataset

The project uses the **Stanford COVID-19 RNA Vaccine** dataset available through Kaggle.

The dataset contains RNA sequences and experimentally measured target variables related to RNA characteristics.

The original dataset is not included in this repository. Please download it from the original Kaggle source and place the required files in the appropriate data directory.

## Methods

### Exploratory Data Analysis

The exploratory analysis includes:

* inspection of the dataset structure;
* analysis of missing values;
* examination of RNA sequence lengths;
* nucleotide frequency analysis;
* visualization of target-variable distributions;
* analysis of sequence-derived characteristics.

The four standard RNA nucleotides are considered:

* Adenine — `A`;
* Cytosine — `C`;
* Guanine — `G`;
* Uracil — `U`.

### Statistical Analysis

The project includes statistical analysis of the dataset and target variables.

The **Mann–Whitney U test** is used to investigate differences between distributions without assuming normality.

The analysis also considers nucleotide frequencies and GC-content:

$$
GC\text{-}content =
\frac{N_G + N_C}{N_A + N_C + N_G + N_U}
$$

where \(N_A\), \(N_C\), \(N_G\), and \(N_U\) represent the numbers of the corresponding nucleotides in an RNA sequence.

### Classical Machine Learning

The following classical machine learning approach is implemented:

* LightGBM.

LightGBM is trained using sequence-derived features and evaluated on the target variables.

### Deep Learning

The project implements a neural network combining convolutional and recurrent components:

* Convolutional Neural Network;
* Bidirectional Long Short-Term Memory network;
* CNN + BiLSTM architecture.

The CNN component extracts local patterns from RNA sequences, while the BiLSTM component models dependencies between sequence positions.

### GC-Content Features

Additional experiments investigate the use of GC-content-related features.

These experiments evaluate whether simple biological sequence characteristics can provide useful information for predicting RNA target variables.

### Graph Neural Network

RNA secondary structures are represented as graphs.

The graph representation is processed using a Graph Neural Network based on the **EdgeConv** operation.

The graph-based approach is designed to incorporate structural relationships between elements of the RNA representation rather than relying only on the original sequence order.

The graph-based experiment uses:

* RNA secondary-structure information;
* graph construction;
* PyTorch Geometric;
* EdgeConv layers;
* regression-based prediction;
* MAE evaluation.

## Experimental Pipeline

```text
RNA sequences
      |
      v
Data preprocessing
      |
      +----------------------+
      |                      |
      v                      v
Statistical analysis    Feature extraction
      |                      |
      |                      +--------------------+
      |                      |                    |
      |                      v                    v
      |                 LightGBM             Sequence models
      |                                           |
      |                                           +--------+
      |                                           |        |
      |                                           v        v
      |                                          CNN     BiLSTM
      |                                           |
      |                                           v
      |                                         CNN + BiLSTM
      |
      v
RNA secondary-structure representation
      |
      v
Graph construction
      |
      v
GNN with EdgeConv
      |
      v
Model evaluation
      |
      v
MAE comparison
```

## Results

The models are evaluated using **Mean Absolute Error**:

$$
MAE =
\frac{1}{n}
\sum_{i=1}^{n}
|y_i-\hat{y}_i|
$$

where:

* \(y_i\) is the true target value;
* \(\hat{y}_i\) is the predicted value;
* \(n\) is the number of observations.

The implemented graph neural network obtained the following MAE values for the five target variables:

| Target   |    MAE |
| -------- | -----: |
| Target 1 | 0.2533 |
| Target 2 | 0.2922 |
| Target 3 | 0.2822 |
| Target 4 | 0.3120 |
| Target 5 | 0.3020 |

The results show that the graph-based model can be used for RNA-related regression tasks. However, its performance should be compared with the sequential CNN+BiLSTM and classical LightGBM approaches under the same data split and evaluation protocol.

## Technologies

The project uses the following technologies and libraries:

* Python;
* NumPy;
* Pandas;
* SciPy;
* scikit-learn;
* LightGBM;
* PyTorch;
* PyTorch Geometric;
* Matplotlib;
* Seaborn;
* Jupyter Notebook;
* ViennaRNA-related tools for RNA secondary-structure analysis.

## Repository Structure

```text
.
├── README.md
├── covid-19-rna(2).ipynb
├── requirements.txt
├── .gitignore
├── data/
│   └── README.md
└── results/
    ├── figures/
    └── tables/
```

## Running the Project

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/covid-19-rna-analysis.git
cd covid-19-rna-analysis
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate the environment on Windows:

```bash
.venv\Scripts\activate
```

Activate the environment on Linux or macOS:

```bash
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Prepare the dataset

Download the Stanford COVID-19 RNA Vaccine dataset from Kaggle.

Place the dataset files in the directory specified in the notebook.

### 5. Run the notebook

Start Jupyter Notebook:

```bash
jupyter notebook
```

Open:

```text
covid19_rna_analysis.ipynb
```

Run the notebook cells in order.

## Reproducibility Notes

The results may depend on:

* the selected train-test split;
* random seeds;
* preprocessing settings;
* sequence length;
* model hyperparameters;
* hardware;
* the installed versions of PyTorch and PyTorch Geometric;
* the availability of RNA secondary-structure software.

For reproducible experiments, random seeds should be fixed and the versions of the main dependencies should be recorded in `requirements.txt`.

## Limitations

This project has several limitations:

* The dataset contains a limited number of experimentally measured RNA characteristics.
* The performance of the models depends on the selected features and preprocessing pipeline.
* The graph representation depends on the quality of RNA secondary-structure prediction.
* The implemented GNN architecture may require additional hyperparameter tuning.
* The experiments do not establish a biological or clinical conclusion about COVID-19 vaccines.
* The results describe the performance of the implemented models on the selected dataset and evaluation procedure.

## Future Work

Possible directions for further development inc
