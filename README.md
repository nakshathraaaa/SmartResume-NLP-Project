# SmartResume: NLP-Based Resume–Job Matching and Skill Gap Analysis

## 📌 Overview

SmartResume is a Natural Language Processing (NLP) based system that compares a resume with a job description and estimates how well the resume matches the requirements of the job.

The system combines traditional NLP using **TF-IDF and cosine similarity** with modern semantic understanding using **Sentence Transformers**. It also performs **skill gap analysis** to identify matching and missing skills.

### Research Question

> How do traditional TF-IDF similarity and modern semantic embeddings differ when matching resumes with job descriptions?

---

## 🎯 Objectives

- Compare resumes and job descriptions using NLP techniques.
- Establish TF-IDF with cosine similarity as a traditional lexical baseline.
- Use Sentence Transformers to capture semantic similarity.
- Combine both approaches using a hybrid matching score.
- Identify matching and missing technical skills.
- Provide simple recommendations based on skill gaps.
- Evaluate the approaches using similarity statistics and ROC-AUC.

---

## 📊 Dataset

The project uses the **Job Resume Fit** dataset from Hugging Face.

**Dataset:** `job_resume_fit.csv`

- **2,385** resume–job pairs
- **23** job categories
- English-language text
- Includes resume text, job description, category, required skills, resume skills, and auxiliary matching information.

Dataset source:

https://huggingface.co/datasets/batuhanmtl/job_resume_fit

> Note: The `ai_match_score` column is treated only as auxiliary/reference information and not as independently verified ground truth.

---

## 🧠 Methodology

The system follows this workflow:

**Resume + Job Description**  
↓  
**Text Preprocessing**  
↓  
**TF-IDF + Cosine Similarity**  
↓  
**Sentence Transformer Embeddings**  
↓  
**Semantic Similarity**  
↓  
**Hybrid Matching Score**  
↓  
**Skill Gap Analysis**  
↓  
**Match Category + Recommendations**

### 1. Text Preprocessing

Basic preprocessing is applied to make the text suitable for comparison while keeping the process simple and explainable.

### 2. TF-IDF Similarity

TF-IDF represents text based on the importance of words within the documents.

Cosine similarity is then used to calculate the similarity between the resume and job description.

This provides a traditional **lexical similarity baseline**.

### 3. Semantic Similarity

The project uses the Sentence Transformer model:

`all-MiniLM-L6-v2`

The model converts text into **384-dimensional embeddings**, allowing semantically similar text to have closer vector representations even when the exact words differ.

### 4. Hybrid Score

The final matching score combines both approaches:

**Hybrid Score = 0.4 × TF-IDF Score + 0.6 × Semantic Score**

The higher weight is given to semantic similarity because it can capture meaning beyond exact word overlap.

### 5. Match Categories

| Hybrid Score | Category |
|---|---|
| ≥ 70% | Strong Match |
| 45% – <70% | Moderate Match |
| <45% | Low Match |

These thresholds are heuristic and were selected for this project rather than learned from labeled data.

### 6. Skill Gap Analysis

A curated technical-skill vocabulary is used to identify:

- Matching skills
- Missing skills
- Skill match percentage
- Simple recommendations for improving the resume

Phrase-based matching is used to reduce incorrect substring matches.

---

## 📈 Results

The controlled evaluation consisted of:

- **2,385 genuine resume–job pairs**
- **2,385 controlled mismatched pairs**
- **4,770 total pairs**

### Similarity Statistics

| Metric | TF-IDF | Semantic |
|---|---:|---:|
| Average genuine-pair score | 16.03% | 51.93% |
| Average mismatched-pair score | 5.24% | 34.45% |
| ROC-AUC | 0.853 | 0.843 |

The correlation between TF-IDF and semantic similarity scores was approximately **0.667**, showing that the two methods capture related but different aspects of resume–job similarity.

### Interesting Case

For one aviation-related example:

- TF-IDF Score: **6.27%**
- Semantic Score: **73.99%**
- Difference: **67.72 percentage points**

This demonstrates how semantic embeddings can identify meaningful similarity even when exact word overlap is relatively low.

---

## 💻 Technologies Used

- Python
- Google Colab
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Sentence Transformers
- Natural Language Processing
- TF-IDF
- Cosine Similarity
- Semantic Embeddings

---

## 📁 Repository Structure

```text
SmartResume-NLP-Project/
│
├── README.md
├── SmartResume_NLP_Project_FINAL_CLEAN.ipynb
├── requirements.txt
│
├── dataset/
│   └── job_resume_fit.csv
│
├── screenshots/
│   └── final_output.png
│
└── report/
    └── SmartResume_NLP_Project_Report(1).pdf
