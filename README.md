# Fuzzy Logic — Similar Name Matching

An intelligent matching module based on **fuzzy sets**: decide whether two person-name strings refer to the same entity despite typos, nicknames, shortenings, or spelling variants.

## Dataset

`corner_cases_new.csv` — pairs of names (`Name1`, `Name2`) with challenging “corner case” variations for similarity testing.

## What was done

### String similarity features

For each pair, three complementary scores were computed:

- **Jaro–Winkler / token-sort ratio** — character similarity with preference for shared prefixes
- **Soundex** — phonetic match (do the names *sound* alike?)
- **Damerau–Levenshtein** — edit distance turned into a normalized similarity

### Fuzzy system design

- Defined fuzzy sets and **membership functions** over the continuous similarity scores (e.g. low / medium / high similarity)
- Implemented **fuzzification** of crisp metric values into membership degrees
- Built an **if–then rule base** for fuzzy inference (how combinations of metrics imply “same person” vs “different”)
- Ran inference on the dataset and summarized match decisions / scores

### Analysis

- Cleaned encoding artifacts and duplicated-fragment cells in the CSV
- Tabulated and visualized membership behavior and final decisions on hard pairs

## Outcome

A complete mini expert system for name matching: classical string metrics feed a fuzzy controller instead of a single hard threshold, which is more robust on ambiguous real-world name pairs.

## Stack

`pandas` · `rapidfuzz` · `python-Levenshtein` · `Fuzzy` (Soundex) · `scikit-fuzzy` · `matplotlib`