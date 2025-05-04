# Public Health Impact Analysis: Data Files

This directory contains the CSV data outputs from our analysis of the drug database from a public health perspective. Each file provides data on a specific aspect of how drug prohibition impacts public health outcomes.

## Files and Contents

### 1. high_risk_substances.csv
**Description:** Documents the yearly prevalence of particularly dangerous substances.
**Columns:**
- `year`: Year of drug test date
- `substance_category`: Category of substance (Fentanyl Analogs, Heroin, Xylazine)
- `sample_count`: Number of samples containing each substance category per year

**Public Health Relevance:** Shows the shift in the drug supply toward more potent and dangerous substances, aligning with the "Iron Law of Prohibition."

### 2. dangerous_combinations.csv
**Description:** Tracks the co-occurrence of high-risk substance combinations.
**Columns:**
- `year`: Year of test date
- `combination`: Specific substance combination detected (e.g., "Fentanyl + Xylazine")
- `sample_count`: Number of samples containing each combination per year

**Public Health Relevance:** These combinations present significantly elevated overdose risks, as they can produce synergistic respiratory depression and complicate overdose reversal efforts.

### 3. fentanyl_analogs_emergence.csv
**Description:** Chronological record of when each fentanyl analog first appeared in the database.
**Columns:**
- `analog`: Name of the specific fentanyl analog
- `year_first_detected`: Year of first detection
- `month_first_detected`: Month of first detection

**Public Health Relevance:** Demonstrates the accelerating "chemical arms race" that prohibition creates, with each new analog representing an information gap for harm reduction efforts.

### 4. detection_patterns.csv
**Description:** Monthly detection counts for key substances of concern.
**Columns:**
- `substance`: Name of substance
- `year`: Year of detection
- `month`: Month of detection
- `detections`: Number of samples containing the substance in that month

**Public Health Relevance:** Shows how rapidly new substances spread once established, highlighting the critical need for early warning systems.

## Usage Notes

These data files can be used to:

1. **Track Dangerous Trends:** Identify significant shifts in the drug supply that correlate with increased overdose risk
2. **Evaluate Early Warning Systems:** Assess how quickly emerging threats are recognized and communicated
3. **Analyze Policy Impact:** Correlate changes in supply with enforcement actions or scheduling decisions
4. **Model Public Health Risk:** Develop risk indices based on the presence of high-risk substances and combinations

For visualization, consider:
- Timeline plots showing the emergence of new substances
- Stacked area charts displaying the changing composition of the drug supply
- Heat maps showing the intensity of detections by month/year
- Comparative analysis with local/regional overdose statistics (where available)

For the source queries used to generate each file, see the `study_queries_public_health.md` file in the parent directory.