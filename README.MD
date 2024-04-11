# PII Data Detection using LLM

A reliable automated LLM based ML Model for detecting Personally Identifiable Information (PII) in student writing.

## Problem Statement
The presence of personally identifiable information (PII) poses a barrier to the analysis and release of open educational datasets due to privacy concerns for students. While manual review remains the most reliable method for PII detection, it is costly and limits the scalability of educational datasets. Existing automatic PII detection techniques, primarily relying on named entity recognition (NER), struggle with accurately identifying and distinguishing sensitive PII, such as student names, from non-sensitive information.

## Folder Structure

    .
    ├── data/
    │
    ├── notebooks/
    │   ├── parse_ai4privacy_dataset_10k.ipynb  : used to parse dataset into required json format
    │   ├── parse_ai4privacy_dataset_10k.ipynb  : used to parse dataset into required json format
    │   └── PII.ipynb
    │
    ├── src/
    │   └── dict.py :   pythin dictionary file used for mapping
    │
    ├── .gitignore
    │
    └── README.md



## Source
The project is based on a Kaggle Competition hosted by The Learning Agency Lab:
[Competition Link](https://www.kaggle.com/competitions/pii-detection-removal-from-educational-data/overview)

## Overview
The model would detect 7 types of PII given below in student-written essays:
- NAME_STUDENT - The full or partial name of a student that is not necessarily the author of the essay. This excludes instructors, authors, and other person names.
- EMAIL - A student’s email address.
- USERNAME - A student's username on any platform.
- ID_NUM - A number or sequence of characters that could be used to identify a student, such as a student ID or a social security number.
- PHONE_NUM - A phone number associated with a student.
- URL_PERSONAL - A URL that might be used to identify a student.
- STREET_ADDRESS - A full or partial street address that is associated with the student, such as their home address.

The tokens would be labeled in BIO (Beginning, Inner, Outer) format:
- PII type prefixed with B or I
- "B-" for the beginning of an entity, e.g., First Name
- "I-" for continuation of the entity, e.g., Middle Name and last name.
- “O” for tokens that are not PII and these will not be included in the final output.

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

## Sample Output
A sample output would be an aggregation of findings from all essays in test data in a CSV file in the below format:

| row_id | document | token | label         |
|--------|----------|-------|---------------|
| 0      | 1        | 9     | B-NAME_STUDENT|
| 1      | 1        | 10    | I-NAME_STUDENT|
| 2      |  2       | 482   | B-NAME_STUDENT|

