# GenAI-Assisted Interpretation of Metagenomic Sequencing Data

AI Driven Clinical Interpretation of mNGS (Metagenomic Next-Generation Sequencing) Reports

This project demonstrates how GenAI + Python + LLM reasoning can assist in the clinical interpretation of metagenomic sequencing data, similar to workflows in labs

It integrates:

Microbial signal detection

Contaminant filtering

Pathogen ranking

Host response interpretation

Clinical reasoning using LLMs

Visualization & clustering (UMAP + embeddings)

End-to-end VS Code + Jupyter reproducible analysis

# Project Overview

Metagenomic sequencing (mNGS) produces large, complex datasets containing:

Bacterial, viral, fungal, and parasitic reads

Environmental contaminants

Background noise

Read mapping counts, identities, contigs, RPM, E-values

Manually interpreting these results is challenging.

This project builds a GenAI-assisted system to automatically:

Process the raw CZ ID mNGS report

Apply QC and filtering

Rank pathogens

Remove contaminants

Integrate host immune response

Generate a clinician-style report using an LLM

# Objective

To create a fully automated clinical-grade interpretation pipeline using:

Python

Jupyter Notebook

Ollama + DeepSeek LLM

Sentence-transformers

GPU acceleration

UMAP clustering

The final output is a clinician-ready infectious disease interpretation combining microbe evidence + host response.

# Dataset
1. Microbial mNGS Report

Downloaded from CZ ID (Illumina mNGS pipeline v8.3):
NGSRL2033_1_report.csv
(561 organisms: bacteria, viruses, fungi, environmental microbes).

Fields used:

RPM (nt/nr)

Read counts

Percent identity

Contig support

Known pathogen flag

E-values

Taxonomic categories

2. Host Response (Simulated for Demo)

NGSRL2033_1_host_response.csv
Contains 4 clinical immune markers:

Bacterial score

Viral score

Inflammation score

Sepsis likelihood

(Values chosen realistically based on typical mNGS host-response tools.)

# Methodology
1. Data Loading & QC
df = pd.read_csv("NGSRL2033_1_report.csv")
• RPM cleaning  
• Identity averaging  
• Contig extraction  
• E-value conversion  
• Missing value repair  

2. Filtering

High-signal organisms selected using:

RPM > 5

Reads > 10

Identity > 80%

Contigs > 0

3. Pathogen Ranking Model

Weighted pathogen score:

Feature	Weight
RPM	0.40
Identity	0.25
Count	0.20
Contigs	0.15

Produces a numerical threat score for each organism.

# Contaminant Removal

Rules remove:

Anelloviridae (known benign human background)

Unclassified buckets

Torque Teno Virus

Reagent contaminants

Environmental species

Then organisms are collapsed at genus level to reduce duplicates.

# What We Did Using LLM

Using Ollama + DeepSeek-R1 8B, we implemented:

✔️ Contaminant reasoning

✔️ Pathogen ranking explanation

✔️ Host response cross-checking

✔️ Clinical differential diagnosis

✔️ infectious diseases report

✔️ “What-if” simulation

✔️ JSON structured clinical output

The LLM receives a detailed prompt including:

Microbial candidates

Pathogen scores

Host markers

QC flags

Interpretation instructions

And generates:

A clinician summary

Full analysis

Recommendations

# Clinical Report (LLM Output Summary)

Primary pathogen: Escherichia coli

Secondary candidate: Klebsiella

Overall interpretation: Strong bacterial infection with moderate inflammatory response and very low sepsis risk.

Viral reads (monkeypox/varicellovirus) are false positives or contaminants — host response does not support viral infection.

Recommended actions:

Confirmatory targeted tests for E. coli

Begin empiric coverage for Gram-negative bacteria

Monitor sepsis indicators


# Results
Key Findings

E. coli had highest RPM, identity, pathogen score → true pathogen

Klebsiella detected but at lower evidence → possible secondary

Host immune response confirms bacterial infection

Viral detections (Varicellovirus, Monkeypox) were false positives / contaminants

Visualization:

We generated a UMAP + DBSCAN clustering map to show similarity between microbes using embeddings from sentence-transformers.

# Discussion

This project demonstrates:

How GenAI models can interpret complex mNGS data with clinical reasoning

How AI can reduce diagnostic turnaround time

How microbial signals + host immune activity create a dual-evidence interpretation system

How open-source tools (DeepSeek, Ollama) can replicate parts of clinical diagnostics

# Future Work

✔ Integrate actual host RNA-seq signature models
✔ Add antimicrobial resistance gene detection
✔ Improve contaminant models using statistical background correction
✔ Deploy as an interactive web dashboard
✔ Add a clinical decision support module


# Technologies Used

Python 3.12

VS Code

Jupyter

Ollama (local LLM)

DeepSeek-R1 8B

Pandas, NumPy

scikit-learn

UMAP-learn

Sentence Transformers

Matplotlib & Seaborn

CUDA GPU acceleration
