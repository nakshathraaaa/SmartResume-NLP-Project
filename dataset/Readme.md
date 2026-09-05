# Dataset

This folder contains information about the dataset used in the SmartResume NLP project.

## Dataset Used

**Job Resume Fit Dataset**

- Source: Hugging Face
- Dataset: `batuhanmtl/job_resume_fit`
- Number of resume–job pairs: 2,385
- Number of job categories: 23
- Language: English

## Dataset Source

The dataset is publicly available on Hugging Face:

https://huggingface.co/datasets/batuhanmtl/job_resume_fit

The main file used in the project is:

`job_resume_fit.csv`

## Dataset Description

The dataset contains resume and job-description pairs along with job categories and skill-related information. It is used to evaluate resume–job matching using TF-IDF similarity and Sentence Transformer semantic similarity.

## Note

The full CSV file is not stored directly in this GitHub repository because its size exceeds GitHub's browser upload limit.

The dataset can be downloaded from the Hugging Face source above and placed in this folder when running the project locally.
