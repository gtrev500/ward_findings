# Drug Database Analysis: The War on Drugs Failure Evidence

This repository contains analysis of a drug database to examine patterns that validate critiques of drug prohibition policies, particularly the War on Drugs in the United States.

## Project Structure

```
.
├── README.md                      # This file - project overview
├── drug_database_schema.md        # Documentation of database structure
├── analysis_context.md            # Contextual information about the analysis
├── analysis_plan.md               # Methodology and structured approach
├── analysis_findings.md           # Key findings and policy implications
├── study_queries.md               # Cypher queries used for each study
└── study_results/                 # CSV data output from each study
    ├── publication_lag.csv        # Data on delays between testing and publication
    ├── nps_emergence.csv          # Data on new psychoactive substances over time
    ├── fentanyl_heroin.csv        # Data on fentanyl in heroin samples
    ├── adulterant_complexity.csv  # Data on multiple substances per sample
    ├── mislabeling.csv            # Data on drug mislabeling percentages
    └── cross_contamination.csv    # Data on mixing of drug classes
```

## Studies Overview

1. **Publication Lag Study**: Examines delays between drug testing and information publication, revealing how criminalization hinders timely public health responses and early warning systems.

2. **Novel Psychoactive Substances (NPS) Study**: Tracks the emergence of new substances over time, demonstrating how scheduling specific drugs leads to rapid innovation in untested alternatives.

3. **Potency Escalation Study**: Documents the rise of fentanyl in samples sold as heroin, validating the "Iron Law of Prohibition" where enforcement drives suppliers toward more potent products.

4. **Adulterant Complexity Study**: Analyzes the increasing number of substances per sample over time, showing how prohibition creates unpredictable, complex mixtures with elevated risk.

5. **Mislabeling Analysis**: Quantifies how often drugs don't contain what they're sold as, demonstrating how prohibition eliminates consumer protections and quality control.

6. **Geographic Source Displacement**: Examines shifts in drug source locations, showing how enforcement actions move rather than eliminate production.

7. **Cross-Contamination Study**: Documents the mixing of drug classes (stimulants in opioids), highlighting a particularly dangerous consequence of unregulated markets.

## Key Findings Summary

Our analysis provides strong evidence for multiple failure modes of prohibition:

1. **Information Failures**: Significant delays in publishing drug test results, culminating in the complete information blackout since April 2024.

2. **Market Distortion Effects**: Dramatic shift toward more potent substances, with fentanyl increasingly replacing heroin.

3. **Quality Control Collapse**: Majority of samples (55-74%) don't contain what they're sold as, with complexity increasing over time.

4. **Chemical Arms Race**: Acceleration of novel substance emergence from ~7/year (pre-2010) to ~91/year (2020-2023).

These findings validate key critiques of prohibition - that it not only fails to prevent drug use but actively makes it more dangerous by incentivizing potency, eliminating quality control, generating novel substances, and blocking harm reduction information.

## Methodology

Each study was conducted using Cypher queries against a Memgraph database of drug samples collected in the United States. The database contains information about:
- 19,032 drug samples
- 5,395 unique substances
- 1,235 types of drugs sold
- 1,226 source locations

The full queries used for each analysis are documented in `study_queries.md`.