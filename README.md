# FewShotSoftwareTestingProject
This project processes a dataset of Java code mutants, generates labeled pairs for equivalence testing, and evaluates GPT-4’s ability to classify whether two Java mutants are semantically equivalent.


## Dataset Overview

- The input is a .rar archive (partitioned_results_TFTPWMN1Complete.rar) containing multiple folders of Java mutant files.
- Each folder represents a mutation set, with mutants that are functionally equivalent.
- Java files are named M<ID>.java.


## Project Steps

1. Dataset Extraction and File Discovery

- The .rar file is extracted using patoolib.
- All .java files are located and grouped by mutation sets.

2. Generating CSV Files

- code_db.csv: Contains all Java mutant files with a unique ID and source code.
- pairwise.csv: Contains labeled pairs:
  - Label 1 for mutants in the same folder (functionally equivalent).
  - Label 0 for mutants from different folders (not equivalent).
- generated_mutant_pairs.csv: Merges the above files to prepare for GPT-4 input.

3. GPT-4 Based Evaluation

- A sample of 25 mutant pairs is selected.
- Few-shot prompting is used with GPT-4 to classify each pair as Equivalent or Not Equivalent.
- Evaluation metrics include:
	- Accuracy
	- Precision
	- Recall
	- F1 Score
- Confusion matrix (optional visualization)


## Requirements

- Install required packages:

	```pip install patool pandas openai scikit-learn matplotlib seaborn```

## OpenAI API Key

- Add your GPT-4 API key:

	```openai.api_key = 'your-api-key-here'```


## Output Files

- code_db.csv: ID-to-code mappings.
- pairwise.csv: Labeled mutant pairs.
- generated_mutant_pairs.csv: Full records for GPT-4 input.
- Terminal output: GPT-4 predictions and evaluation scores.


## Evaluation Example

After prediction:

GPT-4 Evaluation Metrics:
Accuracy:  0.7200
Precision: 0.7500
Recall:    0.7000
F1 Score:  0.7241


## Notes
The dataset is imbalanced, so prompts ask GPT-4 to avoid classifying everything as one class.
Code snippets are truncated to a maximum of 30 lines for context management.
Random sampling ensures variety in testing and few-shot examples.
