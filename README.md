# Named Entity Identification 
## Project Overview

This project implements Named Entity Recognition (NER) using Support Vector Machine (SVM) classifier with comprehensive feature engineering. The system performs binary classification to identify whether words in a sentence are named entities or not, utilizing the CoNLL-2003 dataset for training and evaluation.

## Team Members

- **Shruti Patel** (24M0825, CSE)
- **Kaustubh Shivshankar Shejole** (24M2109, CSE)  
- **Tushar Katakiya** (24M2110, CSE)
- **Kush Mangukiya** (24M0769, CSE)

  
**Course**: CS626 - Speech, Natural Language Processing, and the Web  


## Problem Statement

Perform Named Entity Identification using SVM classifier with appropriate feature engineering to classify each word in a sentence as either a named entity (1) or non-entity (0).

**Example:**
- **Input**: "Washington DC is the capital of United States of America"
- **Output**: "Washington_1 DC_1 is_0 the_0 capital_0 of_0 United_1 States_1 of_1 America_1"

## Dataset

- **Primary Dataset**: CoNLL-2003 NER Data
- **Sources**: 
  - [Papers with Code](https://paperswithcode.com/dataset/conll-2003)
  - [Hugging Face](https://huggingface.co/datasets/conll2003)
- **Format**: Pre-tokenized sentences with entity annotations
- **Task**: Binary classification (Named Entity vs Non-Entity)

## Features

### Data Preprocessing

1. **Tokenization**: Utilized pre-tokenized format from CoNLL-2003 dataset
2. **Binary NER Labeling**: Converted multi-class entity tags (`PER`, `ORG`, `LOC`, `MISC`) to binary labels:
   - `1` for named entities
   - `0` for non-entities (O tag)
3. **Case Preservation**: Maintained original casing for capitalization pattern analysis
4. **POS Tag Mapping**: Converted POS tags to numerical identifiers for feature representation
5. **Possessive Suffix Removal**: Implemented `get_root_word` function to standardize words by removing `'s` and `'` endings

### Feature Engineering

#### Capitalization Features
- **`is_title`**: Detects title case words (common in proper nouns)
- **`is_upper`**: Identifies uppercase words (acronyms, abbreviations)
- **`is_lower`**: Flags lowercase words (helps distinguish from proper nouns)
- **`word.lower()`**: Lowercase representation for standardization

#### Character-Based Features
- **`suffix-1`**: Last character analysis (plurals, name patterns)
- **`prefix-1`**: First character analysis (entity type patterns)
- **`root_word`**: Base form extraction for variation reduction

#### Semantic Features
- **`is_currency`**: Currency term detection
- **`date_time_check`**: Temporal expression identification
- **`pos`**: Part-of-speech tags for grammatical context

### SVM Implementation

- **Library**: scikit-learn SVM implementation
- **Approach**: Binary classification with engineered features
- **Feature Processing**: Multi-dimensional feature vectors combining linguistic and semantic information
- **Supporting Libraries**: NLTK for tokenization, POS tagging, and feature extraction

## Performance Results

### Overall Performance
| Metric    | Non-Entity (0) | Named Entity (1) | Overall |
|-----------|----------------|------------------|---------|
| Precision | 0.99           | 0.94             | 0.98    |
| Recall    | 0.99           | 0.97             | 0.98    |
| F1-Score  | 0.99           | 0.95             | 0.98    |
| Support   | 38,554         | 8,112            | 46,666  |

**Overall Accuracy**: 98%

### Confusion Matrix Analysis

The system demonstrates excellent performance with:
- **High precision for non-entities** (99%): Minimal false positive rate
- **Strong recall for named entities** (97%): Effective entity detection
- **Balanced F1-scores**: Robust performance across both classes

## Error Analysis

### Common Misclassification Patterns

1. **Ambiguous Names**:
   - **"May"**: Context-dependent interpretation (month vs. verb)
   - **"Apple"**: Misclassified as common noun without clear business context

2. **Capitalization Issues**:
   - **Uncapitalized Entities**: Named entities in informal text lacking proper capitalization
   - **Overcapitalized Text**: Regular words capitalized inappropriately leading to false positives

3. **Context Dependency**:
   - Words requiring broader sentence context for accurate classification
   - Domain-specific terminology without clear linguistic markers


