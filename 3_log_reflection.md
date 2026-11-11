# 3_log_reflection.md — Cleaning log and reflection

## Cleaning log

| Step | Action | Evidence / result | Decision |
|---|---|---|---|
| 1 | Loaded source as text and inspected shape/types | 97 rows, 6 columns; price stored as object/text | Keep raw file unchanged; work on a copy |
| 2 | Checked missing values | One missing price at 2026-01-01, Pulse C, City 2 | Retain as missing; do not invent a value |
| 3 | Checked exact duplicates | One exact duplicate, the 2026-01-08 Staple A / City 1 / 99.5 record | Remove the extra copy; export it separately |
| 4 | Parsed price values | Comma-formatted `1,250` and blank prevent direct numeric conversion | Remove commas and convert; blank becomes NaN |
| 5 | Investigated 1,250 | Paired City 1 value is 103.0; usual City 2 premium is 6.0; adjacent weeks support 109.0 | Correct to 109.0, preserve original, document inference |
| 6 | Investigated 9,999 | Paired City 2 value is 163.5; usual City 2 premium is 6.0; adjacent weeks support 157.5 | Correct to 157.5, preserve original, document inference |
| 7 | Standardized item label | `oil b` differs only in capitalization from `Oil B` | Normalize capitalization |
| 8 | Investigated 2026-02-05 `oil b`, City 1, 108.5 | 108.5 fits Staple A series; Oil B observations are around 318 | Relabel as Staple A and document inference |
| 9 | Checked panel after cleaning | 96 rows and 96 unique date-item-city keys; one price remains missing | Panel structure retained; missing value remains visible |

## AI-use log

AI assistance was used to help draft and review the cleaning code and to structure the audit. The code was not accepted blindly. Each suggested operation was checked against the raw rows and the before/after evidence.

| AI-suggested operation | Verdict | Reason |
|---|---|---|
| Strip whitespace and normalize `oil b` capitalization | KEEP | Formatting-only change |
| Convert price strings to numeric | KEEP | Required for numerical checks; preserve original values |
| Replace 1,250 with 109.0 | MODIFY | Accept only with paired-city and time-series evidence, plus an audit note |
| Replace 9,999 with 157.5 | MODIFY | Accept only with paired-city and time-series evidence, plus an audit note |
| Relabel suspicious `oil b` row to Staple A | MODIFY | Pattern supports it, but source does not independently verify the label |
| Drop exact duplicate | KEEP | Exact duplicate would double-count the observation |
| Fill missing price | REJECT | No source evidence supports a replacement value |
| Automatically delete every outlier | REJECT | Outliers require investigation rather than automatic deletion |

## Reflection

My decisions differed from a fully automatic cleaning approach in three ways. First, I did not fill the missing price because the file contains no source value for it. Second, I did not simply delete the two extreme prices; I checked their paired-city values and surrounding weeks, then corrected them while preserving the original strings and explaining the inference. Third, I treated the suspicious product label as a possible data-entry error rather than assuming capitalization alone solved it.

The strongest evidence was the repeated six-unit difference between the two cities for the same product and date, alongside the weekly price patterns. Without checking the panel structure, I could have missed the duplicate and the mislabeled product. I could also have made the dataset look complete by inventing the missing value, which would have been less defensible than retaining a visible gap.

The cleaned data is more consistent, but it is not equivalent to verified official data. The file itself states that these are illustrative teaching observations, and the two price corrections plus the product relabeling remain documented inferences.
