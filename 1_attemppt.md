# 1_attempt.md — Diagnostic attempt and planned decisions

> **Timing note:** This is a reconstructed attempt-before-AI. 

## File diagnosis

* 97 rows and 6 columns.

* Expected panel: 12 dates × 4 items × 2 cities = 96 date-item-city combinations.

* `price` is stored as text because the file contains a comma-formatted value (`1,250`) and a blank.

* One exact duplicate exists.

* One price is missing.

* Two extreme price entries (1,250 and 9,999) need investigation.

* `oil b` has inconsistent capitalization.

* One record labelled `oil b` has a price that appears to belong to the Staple A series.

## Planned decisions

| Issue | Planned decision | Reason | 
| ----- | ----- | ----- | 
| Price stored as text | Convert to numeric after removing commas | Enables numerical checks while preserving original strings. | 
| Missing price | Retain as missing and flag | No source value supports imputation. | 
| 1,250 | Investigate; correct only if internal pattern supports it | Paired city and surrounding weeks can reveal a likely entry error. | 
| 9,999 | Investigate; correct only if internal pattern supports it | Paired city and surrounding weeks can reveal a likely entry error. | 
| `oil b` | Standardize to `Oil B` | Formatting consistency only. | 
| Mislabelled item | Investigate and document any correction | The price series may identify a product-label error. | 
| Exact duplicate | Remove one copy; preserve it separately | Avoids double-counting without losing the audit record. | 

## Source integrity

The original CSV is kept unchanged. All operations are performed on a copy. The source identifies the data as illustrative teaching data, not actual PBS observations.