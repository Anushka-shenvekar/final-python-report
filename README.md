# Commenticius Mutation Screening Analysis

This repository contains the complete Python-based analysis, graphs, and final report for identifying gene mutations that affect mRNA expression, protein expression, and cell viability. The analysis is based on 49 mutation data files provided by Commenticius.

## 📂 Contents

- `commenticius_analysis_script.py` — Python script for data loading, mutation classification, analysis, and plotting.
- `Commenticius_Conclusion_Report.docx` — Word document containing final conclusions and all Python-generated graphs.
- PNG Graphs:
  - `viability_by_mutation_type.png`
  - `mrna_vs_protein_change.png`
  - `viability_distribution.png`

---

## 🧪 Full Python Workflow

### 1. Load Libraries
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import os
import glob
```

### 2. Load and Merge Data
```python
file_paths = sorted(glob.glob("file *.txt"))
all_data = [pd.read_csv(f, sep="\t") for f in file_paths]
df_combined = pd.concat(all_data, ignore_index=True)
```

### 3. Classify Mutation Type and Location
```python
def classify_mutation(wt, mut):
    if len(wt) < len(mut): return "Insertion"
    elif len(wt) > len(mut): return "Deletion"
    return "Substitution"

def classify_location(wt, mut):
    for i in range(min(len(wt), len(mut))):
        if wt[i] != mut[i]: return "Promoter" if i < 1000 else "Coding"
    return "Unknown"

df_combined["Mutation.Type"] = ...
df_combined["Mutation.Location"] = ...
```

### 4. Calculate Expression & Viability Change
```python
def calc_change(wt_cols, mut_cols):
    return df_combined[mut_cols].mean(axis=1) - df_combined[wt_cols].mean(axis=1)

df_combined["mRNA_Change"] = ...
df_combined["Protein_Change"] = ...
df_combined["Viability_Change"] = ...
```

### 5. Plot Graphs Using Seaborn
```python
sns.boxplot(...)
plt.savefig("viability_by_mutation_type.png")

sns.scatterplot(...)
plt.savefig("mrna_vs_protein_change.png")

sns.histplot(...)
plt.savefig("viability_distribution.png")
```

### 6. Identify Top 5 Genes
```python
top_genes = df_combined.sort_values(
    by=["Viability_Change", "Protein_Change", "mRNA_Change"],
    ascending=False
).head(5)
```

### 7. Generate Word Report
```python
from docx import Document
doc = Document()
doc.add_heading(...)
doc.add_picture(...)
doc.save("Commenticius_Conclusion_Report.docx")
```

### 8. Create ZIP for Submission
```python
import zipfile
with zipfile.ZipFile("commenticius_project_submission.zip", "w") as zipf:
    zipf.write(...)
```

---

## 🔗 GitHub Setup Instructions

1. Create a new GitHub repository: [https://github.com/new](https://github.com/new)
2. Clone and move into the folder:
```bash
git clone https://github.com/your-username/commenticius-mutation-analysis.git
cd commenticius-mutation-analysis
```
3. Add and commit all files:
```bash
git add .
git commit -m "Initial commit with code, report, and plots"
git push -u origin main
```

---

## ✅ GitHub Repo Link to Include in Report
```
https://github.com/your-username/commenticius-mutation-analysis
```
