# BLE-Based Indoor Localization: Reproducibility Code

Research code accompanying the manuscript **“A Comparative Evaluation of Machine Learning and Deep Learning Models for BLE-Based Indoor Localization: Generalization and RSSI Noise Robustness.”**

## Scope

The notebook compares seven regression models using 13 BLE-beacon RSSI features and two-dimensional grid-coordinate targets:

- k-Nearest Neighbors (kNN)
- Decision Tree
- Random Forest
- Support Vector Regression (SVR)
- Multilayer Perceptron (MLP)
- 1D-CNN with Global Average Pooling (CNN-GAP)
- 1D-CNN with Flattening (CNN-FLAT)

Four evaluation protocols are covered: (1) observation-level / seen-location testing, (2) held-out-location evaluation, (3) chronological future-time evaluation, and (4) controlled RSSI perturbations at ±2, ±5, and ±8 dBm.

**Unit clarification:** localization errors and coordinate differences are expressed in grid-coordinate units. The reference coordinates have not been calibrated to physical distances; values must not be interpreted as metres.

## Repository structure

```text
ble-indoor-localization/
├── notebooks/
│   └── ble_indoor_localization_experiments.ipynb
├── results/
│   ├── FINAL_MASTER_EXPERIMENTAL_RESULTS.csv
│   ├── FINAL_MASTER_PAPER_TABLE.csv
│   ├── STAGE4_MASTER_NOISE_ROBUSTNESS.csv
│   ├── STAGE4_STATISTICAL_VALIDATION.csv
│   └── stage4_robustness_summary.csv
├── README.md
├── requirements.txt
└── .gitignore
```

## Dataset access and preparation

The BLE-RSSI dataset used in the study is from Waldo Library, Western Michigan University. It contains 13 beacon RSSI features (`b3001`–`b3013`) and reference-location labels. The original dataset is **not redistributed** in this repository. Obtain it from its original provider and check the provider's terms before sharing or redistributing it.

For the complete experiment, open the notebook in Google Colab and provide the two source files when prompted:

- `iBeacon_RSSI_Labeled.csv`
- `iBeacon_RSSI_Unlabeled.csv`

The supervised experiments use the labelled file. The unlabelled file is loaded for dataset inspection only. The notebook expects uploaded files to be available in the Colab working directory (`/content`).

## Running the notebook

1. Open `notebooks/ble_indoor_localization_experiments.ipynb` in Google Colab or Jupyter.
2. Install dependencies from `requirements.txt` if required. The exact package versions used for a final archival run should be recorded.
3. Upload the two original dataset CSV files when prompted and execute the notebook sequentially from the beginning. Do not skip data preparation, split construction, training, or evaluation cells.
4. The final Stage 4 figure-generation section asks for `STAGE4_MASTER_NOISE_ROBUSTNESS.csv`. Upload the file from this repository's `results/` folder. It no longer requires a separate ZIP archive.
5. The figure-generation section exports Figures 4–6 as PNG and PDF files and packages the generated figures into a ZIP for convenience.

The CSV files in `results/` are the consolidated results accompanying the manuscript. They are provided for inspection and comparison; their presence does not mean that the notebook has been independently rerun in a fresh environment.

## Evaluation and interpretation notes

- Random seed: 42 where specified in the notebook.
- Feature scaling is fitted on the training partition within each evaluation protocol.
- In Stage 4, bounded perturbations are applied to detected raw RSSI values. The raw non-detection marker (`-200`) is preserved before scaling.
- Stage 4 reuses the Stage 1 scaler and does not retrain the models.
- The held-out-location and chronological protocols are distinct evaluations. Cross-stage differences should not be interpreted as the isolated effect of a single factor.
- Synthetic RSSI perturbations do not reproduce all real environmental effects, such as correlated multipath, body blockage, receiver variation, interference, or beacon displacement.
- Coordinate values have not been calibrated to physical distances. Do not report localization errors as metres.

## Software

See `requirements.txt`. The notebook was developed for a Google Colab-style environment. For archival reproducibility, record the exact Python and package versions from the final successful execution environment.

## Research use and citation

Please cite the associated manuscript once publication details are available, and cite the original BLE dataset at its official source. The manuscript and dataset have separate rights and licensing conditions.

## Release status

This repository contains the experiment notebook and consolidated result tables. The original dataset is not included. A fresh-runtime execution with the original dataset is required before claiming full independent reproduction of every reported result.
