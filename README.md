# CSE Student Question Intent Dataset (v0.1)

**Last updated:** 2026-03-10  
**Dataset type:** Student-written short questions for *intent detection* (single-label, multiclass text classification).  
**Collection method:** Structured Google Form (self-submitted by undergraduate CSE students).  
**Current size (after cleaning and exact deduplication):** **3,706** question instances .

---

## Dataset summary

This dataset contains questions written by undergraduate CSE students. Each question is associated with one **intent label** (20 intents) and one **language tag** (`English`, `Bangla`, or `Mixed`). The dataset is intended to support research on **question intent detection** in an academic/student-help context.

**Important note on coverage:** the current v0.1 release contains responses from **1st-, 2nd-, and 3rd-year** students only. **No 4th-year responses** are present in the released file.

---

## Supported tasks

- **Intent Detection / Intent Classification** (single-label, 20 classes)
- Optional analyses:
  - Performance by **academic year**
  - Performance by **language type** (`English`, `Bangla`, `Mixed`)

---

## Label provenance

The intent labels in v0.1 come from the **structured form design itself**. Participants were asked to submit each question under one of the predefined intent categories. After collection, the data were cleaned, standardized, and deduplicated, but the current release should be interpreted as a **participant-labeled dataset with curated preprocessing**, not as a fully expert-annotated corpus.

---

## Languages

The `language` field in the released CSV uses the following values:

- `English`
- `Bangla`
- `Mixed` (Bangla-English mixed / code-mixed)

Current distribution (cleaned):
- **English:** **1,421**
- **Mixed:** **1,532**
- **Bangla:** **753**

---

## Label set (20 intents)

1. Debugging / Error Fixing  
2. How-to Implementation  
3. Concept Explanation / Clarification  
4. Algorithm Choice / Strategy  
5. Data Structures  
6. Time & Space Complexity  
7. Programming Language Syntax / Features  
8. Object-Oriented Programming (OOP)  
9. Database / SQL  
10. Operating Systems (OS)  
11. Computer Networks  
12. Web Development  
13. Software Engineering / SDLC  
14. Machine Learning / AI  
15. Cybersecurity  
16. Competitive Programming / Problem Solving  
17. Project Guidance / System Architecture  
18. Tooling / Environment Setup  
19. Career / Internship / Interview Prep  
20. Exam / Assignment / Course Admin

---

## Data fields (CSV schema)

The released CSV file is in **long format** (1 row = 1 question):

| Column | Type | Description |
|---|---|---|
| `question_id` | string | Unique question ID (e.g., `Q000123`) |
| `respondent_id` | int | Anonymous respondent index |
| `timestamp` | string / datetime-like | Form submission timestamp as exported from the source sheet |
| `year` | int | Student year (`1`, `2`, or `3` in v0.1; `4` currently absent) |
| `intent_id` | int | Intent ID (`1..20`) |
| `intent` | string | Intent name |
| `language` | string | `English` / `Bangla` / `Mixed` |
| `text` | string | Question text |

---

## Cleaning and quality control

**Performed in v0.1:**
- Converted the wide Google Form export into a **long-format** intent dataset.
- Removed empty entries and obvious non-answers (e.g., `yes`, `no`, `null`, extremely short fragments).
- Applied light text normalization (e.g., trimming and whitespace cleanup).
- Applied basic PII redaction where detected:
  - Emails -> `[REDACTED_EMAIL]`
  - Phone-like patterns -> `[REDACTED_PHONE]`
- Performed **exact deduplication within the same intent context**.

**Not yet fully handled (future versions):**
- Near-duplicate detection (paraphrases)
- Manual relabeling / spot-check verification of participant-selected intent labels
- Formal inter-annotator agreement analysis
- Advanced PII review for names or embedded identifiers inside free text

---

## Current dataset composition


- **Questions (cleaned):** 3,706
- **Intent classes:** 20
- **Language categories:** 3

### Academic year distribution
- **Year 1:** 2,030
- **Year 2:** 639
- **Year 3:** 1,037
- **Year 4:** 0 *(currently absent in v0.1)*

### Recommended experimental split
The release package includes a fixed stratified split file:
- **Train:** 2,964
- **Validation:** 371
- **Test:** 371

Use the provided split file for reproducible experiments.

---

## Recommended use for modeling

- Use the provided `splits_v0_1_stratified.csv` file rather than generating a new random split.
- Treat the task as **single-label multiclass classification**.
- Report at least:
  - **Accuracy**
  - **Macro Precision**
  - **Macro Recall**
  - **Macro F1**
- Optional subgroup analysis:
  - by `language`
  - by `year`

---

## Intended use

This dataset is intended for:
- intent detection / intent classification research
- student Q\&A assistants
- academic helpdesk or chatbot research
- educational NLP in multilingual or code-mixed settings

---

## Limitations and bias notes

- **Selection bias:** Responses were collected through voluntary Google Form submissions and may not represent all students.
- **Label noise:** Students selected intent categories themselves, so some questions may be mislabeled.
- **Year imbalance:** Fourth-year data are absent in v0.1.
- **Domain bias:** The dataset is CSE-focused and may not generalize directly to other academic disciplines.
- **Language variation:** Mixed-language and informal phrasing may increase modeling difficulty.

---

## Label distribution (v0.1)

| intent_id | intent | total | English | Mixed | Bangla |
|---:|:---|---:|---:|---:|---:|
| 1 | Debugging / Error Fixing | 202 | 78 | 83 | 41 |
| 2 | How-to Implementation | 207 | 84 | 82 | 41 |
| 3 | Concept Explanation / Clarification | 194 | 74 | 81 | 39 |
| 4 | Algorithm Choice / Strategy | 199 | 77 | 82 | 40 |
| 5 | Data Structures | 186 | 68 | 79 | 39 |
| 6 | Time & Space Complexity | 188 | 69 | 81 | 38 |
| 7 | Programming Language Syntax / Features | 190 | 73 | 79 | 38 |
| 8 | Object-Oriented Programming (OOP) | 191 | 75 | 78 | 38 |
| 9 | Database / SQL | 183 | 68 | 78 | 37 |
| 10 | Operating Systems (OS) | 197 | 75 | 82 | 40 |
| 11 | Computer Networks | 192 | 73 | 79 | 40 |
| 12 | Web Development | 191 | 73 | 78 | 40 |
| 13 | Software Engineering / SDLC | 183 | 69 | 76 | 38 |
| 14 | Machine Learning / AI | 182 | 66 | 78 | 38 |
| 15 | Cybersecurity | 177 | 68 | 72 | 37 |
| 16 | Competitive Programming / Problem Solving | 187 | 75 | 75 | 37 |
| 17 | Project Guidance / System Architecture | 176 | 66 | 75 | 35 |
| 18 | Tooling / Environment Setup | 163 | 65 | 64 | 34 |
| 19 | Career / Internship / Interview Prep | 165 | 64 | 68 | 33 |
| 20 | Exam / Assignment / Course Admin | 153 | 61 | 62 | 30 |

---

## Release package

The v0.1 release package is expected to include:
- `intent_questions_v0_1.csv`
- `splits_v0_1_stratified.csv`
- `label_definitions_v0_1.csv`
- `label_distribution_per_intent_v0_1.csv`
- `dataset_statistics_v0_1.md`
- `LICENSE`
- `CHANGELOG.md`

---

## Citation (placeholder)

If you use this dataset, please cite the accompanying paper and/or dataset release once publicly available.

**Placeholder citation:**  
> Author(s). *CSEQIntent: A Benchmark Dataset for Intent Detection in Undergraduate CSE Student Questions.* 2026.

---

## License

See the included `LICENSE` file for the dataset license.

---

## Contact

Project team: *[add lab / institution / email here]*
