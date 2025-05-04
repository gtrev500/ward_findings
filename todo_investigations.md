# EDA Investigation TODO List

This document outlines the planned exploratory data analysis tasks for the drug database, focusing on validating critiques of drug prohibition policies.

## Completed Investigations

- [x] **Publication Lag Analysis**: Examine delays between testing and publication
- [x] **Novel Psychoactive Substances (NPS) Analysis**: Track emergence of new substances over time
- [x] **Potency Escalation Analysis**: Monitor fentanyl presence in heroin samples
- [x] **Adulterant Complexity Analysis**: Measure increase in substances per sample
- [x] **Mislabeling Analysis**: Quantify discrepancies between sold-as and actual content
- [x] **Cross-Contamination Analysis**: Track mixing of stimulants in opioid samples

## Planned Investigations

### 1. Deeper Substance-Level Analyses

- [ ] **Common Adulterants Tracking**: Identify the most common adulterants by drug type
  - Identify top 10 most common adulterants for each major drug category
  - Track changes in adulterant preferences over time
  - Analyze geographical patterns in adulterant use

- [ ] **Dangerous Combinations Analysis**: Focus on particularly risky substance combinations
  - Identify co-presence of benzodiazepines and opioids
  - Track xylazine emergence in the opioid supply
  - Analyze multiple synthetic opioid combinations

### 2. Geographical Analyses

- [ ] **Regional Comparison Study**: Compare drug composition across different US regions
  - Compare East Coast vs. West Coast drug composition
  - Analyze rural vs. urban differences in drug adulteration
  - Track border state vs. interior state differences

- [ ] **Enforcement Impact Analysis**: Correlate major enforcement actions with geographical shifts
  - Identify major DEA operations during the dataset timeframe
  - Analyze changes in source locations following operations
  - Track "balloon effect" patterns of displacement

### 3. Temporal Pattern Analyses

- [ ] **Seasonality Analysis**: Examine seasonal patterns in drug composition
  - Analyze monthly/quarterly variations in drug purity
  - Identify seasonal patterns in specific adulterants
  - Correlate with known supply chain disruptions

- [ ] **Policy Impact Timeline**: Correlate composition changes with policy changes
  - Identify major scheduling decisions during dataset timeframe
  - Create before/after comparisons for specific substance bans
  - Analyze lag between policy implementation and market response

### 4. Market Dynamics Analyses

- [ ] **Brand Reliability Analysis**: Examine consistency within specific "branded" drugs
  - Analyze consistency of samples with the same street name
  - Track how brand reliability changes over time
  - Compare branded vs. unbranded sample consistency

- [ ] **Price-Purity Relationship**: Analyze economic factors if price data is available
  - Correlate price data with purity levels (if available)
  - Track inflation-adjusted price trends by substance
  - Analyze geographical price variations

### 5. Public Health Impact Analyses

- [ ] **Overdose Correlation Study**: Connect composition changes with overdose trends
  - Gather public overdose data for the same timeframe
  - Correlate emergence of specific substances with overdose spikes
  - Create risk index based on sample composition

- [ ] **Warning System Evaluation**: Assess how effectively the testing system serves as an early warning
  - Calculate detection-to-alert timeframes for novel substances
  - Analyze how publication lag affects warning system efficacy
  - Compare with other international early warning systems

### 6. Specialized Studies

- [ ] **Synthetic Cannabinoids Analysis**: Focus on this rapidly evolving class
  - Track novel synthetic cannabinoid emergence timeline
  - Analyze mislabeling patterns in cannabis products
  - Examine potency increases over time

- [ ] **Counterfeit Pharmaceutical Analysis**: Examine fake prescription drugs
  - Analyze content of samples sold as prescription medications
  - Track changes in counterfeit pill composition over time
  - Identify percentage containing dangerous substances

## Implementation Notes

Each investigation should follow our standardized EDA structure:
1. Create analysis plan with specific queries
2. Execute queries and save results to CSV files
3. Document methodology and findings
4. Connect results to broader policy implications

Investigations should be prioritized based on:
- Data availability within our dataset
- Relevance to current drug policy debates
- Potential impact on harm reduction strategies
- Complexity and time requirements