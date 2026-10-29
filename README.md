# Patterns, Persistence and Prediction

Analysis of early help-seeking behaviors and later struggle in ASSISTments data.

## Dataset

Download the ASSISTments dataset here:
[2011 Goldstein, Baker, and Heffernan dataset](https://sites.google.com/site/assistmentsdata/datasets/2011-goldstein-baker-heffernan)

The notebooks use **`PJ Data (Actions).csv`**. The raw dataset is not included in this repository.

## Setup

Use Python 3.12. From the project directory, create and activate a virtual environment.

**Windows (PowerShell)**
```powershell
py -3.12 -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**macOS/Linux**
```bash
python3.12 -m venv .venv
source .venv/bin/activate
```

Install dependencies:
```bash
python -m pip install --upgrade pip
python -m pip install numpy pandas scipy matplotlib networkx statsmodels scikit-learn jupyter nbconvert threadpoolctl
```

## Run the analyses

Run notebooks from their respective folders and execute cells from top to bottom.

1. **RQ1 — Patterns and transitions**  
   Open `RQ1 and Hand-Offs/RQ1_final_clean_revised_with_RQ2_RQ3_handoff_TNA_ARROWS.ipynb`. Place the downloaded ASSISTments ZIP where the notebook expects it. RQ1 generates `rq1_merged_spm_quade_outputs/rq1_objects_for_rq2_rq3.pkl`.

2. **RQ2 — Change in help reliance**  
   Open `RQ2 and Hand-Offs/RQ2_reliance_on_help.ipynb`. Run RQ1 first; RQ2 needs the hand-off pickle generated above. Update `HANDOFF_PATH` if necessary.

3. **RQ3 — Prediction**  
   Open `RQ3 and Consolidation/RQ3_complete_explained.ipynb`. Set `DATA_PATH` to the location of `PJ Data (Actions).csv`. RQ3 can run independently of RQ1 and RQ2.

Start Jupyter with:
```bash
jupyter notebook
```

Check each notebook's setup cell if a data path differs from the defaults. RQ3's HTML export is available at `RQ3 and Consolidation/RQ3_complete_explained.html` for reading without running the notebook.

## Outputs

- **RQ1:** pattern/transition results and the hand-off file for RQ2.
- **RQ2:** help-reliance comparisons and figures.
- **RQ3:** prediction results, diagnostics, figures, and run manifest in `RQ3 and Consolidation/rq3_complete_results/`.

## Main findings

- **RQ1:** repeated bottom-out hints were more common among students who later struggled; repeated first-attempt success was more common among students who did not.
- **RQ2:** bottom-out reliance declined more among students without later struggle, including when comparing students with the same early score.
- **RQ3:** help-use and behavioral-state features improved prediction over the early-correctness baseline; transition counts added no further predictive benefit in the reported evaluations.

These are observational findings and should not be interpreted as causal effects.
# LA_Project_Investigating_Help_Seeking_Behavior
