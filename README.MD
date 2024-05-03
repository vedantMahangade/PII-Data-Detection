# PII Data Detection using Transformers

A reliable automated LLM based ML Model for detecting Personally Identifiable Information (PII) in student writing.

## Problem Statement
The presence of personally identifiable information (PII) poses a barrier to the analysis and release of open educational datasets due to privacy concerns for students. While manual review remains the most reliable method for PII detection, it is costly and limits the scalability of educational datasets. Existing automatic PII detection techniques, primarily relying on named entity recognition (NER), struggle with accurately identifying and distinguishing sensitive PII, such as student names, from non-sensitive information.

## Folder Structure

    .
    ├── data/ 
    │   ├── Most data files are not uploaded due to size constraints
    │   ├──test-essay*.txt : Sample Input Test essays for model inference
    │   └──test.json : Test data from kaggle competetion 
    │
    ├── notebooks/
    │   ├── Data Preprocessing and EDA.ipynb  : used to mearge original dataset and external dataset
    │   ├── Inference.ipynb.ipynb  : compares output of different fine tuned models
    │   ├── ModelPush.ipynb : pushes model to hugging face
    │   ├── PII_Train_BigBird.ipynb : training script for BigBird
    │   ├── PII_Train_DistilBERT.ipynb : training script for DistilBERT
    │   └── PII_Train_RoBERTa.ipynb : training script for RoBERTa
    │   
    ├── src/
    │   └── dict.py :   pythin dictionary file used for mapping
    │
    ├── .gitignore
    │
    ├── README.md
    │
    └── requirements.yaml



## Overview
The model would detect 7 types of PII given below in student-written essays:
- NAME_STUDENT - The full or partial name of a student that is not necessarily the author of the essay. This excludes instructors, authors, and other person names.
- EMAIL - A student’s email address.
- USERNAME - A student's username on any platform.
- ID_NUM - A number or sequence of characters that could be used to identify a student, such as a student ID or a social security number.
- PHONE_NUM - A phone number associated with a student.
- URL_PERSONAL - A URL that might be used to identify a student.
- STREET_ADDRESS - A full or partial street address that is associated with the student, such as their home address.


## Dataset Description
The dataset contains around 22,000 student-written essays in a JSON file.
The format of the dataset is as below:

```json
{
"document": 1,
"full_text": "Design Thinking for innovation reflexion-Avril 2021-Nathalie Sylla.",
"tokens": ["Design", "Thinking", "for", "innovation", "reflexion", "-", "Avril", "2021", "-", "Nathalie", "Sylla", "."],
"trailing_whitespace": [true, true, true, true, false, false, true, false, false, true, false, true],
"label": ["O","O","O","O","O","O","O","O","O","B-NAME_STUDENT","I-NAME_STUDENT","O"]
},
{...}
```

- document (int): an integer ID of the essay
- full_text (string): a UTF-8 representation of the essay
- tokens (list of string) (string): a string representation of each token
- trailing_whitespace (list of bool): a boolean value indicating whether each token is followed by whitespace.
- labels (list of string): a token label in BIO format - training data only


