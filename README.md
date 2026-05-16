# When Evolution Gets It Wrong
### Characterizing Pathogenic Mutations Missed by HMMs Using Protein Language Models
CS 466 / BIOE 466 — Spring 2026 — UIUC

---

## Overview
This project implements core HMM algorithms from scratch, reproduces the FATHMM variant effect scoring framework, and compares it against ESM-1b to characterize where and why the HMM positional independence assumption fails.

---

## Repository Structure
setup.ipynb              # Run once: downloads data, parses ClinVar/Pfam, runs HMMER

HMM.ipynb                # HMM implementation (Forward, Backward, Viterbi) + unit tests

analysis.ipynb           # Main analysis: FATHMM vs ESM-1b comparison

clinvar_sample.csv       # Filtered ClinVar variants (top 500 genes, 20/gene)

pfam.pkl                 # Parsed Pfam emission probabilities

sequences.json           # UniProt protein sequences

uid_mapping.json         # Gene → UniProt ID mapping

gene_mapping.json        # Gene → Pfam domain mapping (from HMMER)

fathmm_input.txt         # Input file for FATHMM web server

Fathmm_output.rtf        # FATHMM web server results

esm1b_results.pkl        # Computed ESM-1b scores and difference vectors


---

## How to Run

**Step 1: Install dependencies**
```bash
pip install numpy pandas scipy scikit-learn requests fair-esm torch matplotlib
```

**Step 2: Run setup.ipynb**

Downloads ClinVar and Pfam, parses variants, runs HMMER, and generates `fathmm_input.txt`. Run once only.

**Step 3: Submit to FATHMM web server**

Go to http://fathmm.biocompute.org.uk/inherited.html, upload `fathmm_input.txt`, select Weighted, download result as `Fathmm_output.rtf`.

**Step 4: Run HMM.ipynb**

HMM implementation and unit tests.

**Step 5: Run analysis.ipynb**

Loads all saved files, computes ESM-1b scores, classifies variants into Type A/B/C/D, and generates all plots.

---

## Data Sources

| Dataset | Source |
|---------|--------|
| ClinVar (GRCh37) | https://ftp.ncbi.nlm.nih.gov/pub/clinvar/ |
| Pfam HMM | https://ftp.ebi.ac.uk/pub/databases/Pfam/ |
| ESM-1b | pip install fair-esm |
| FATHMM scores | http://fathmm.biocompute.org.uk |
