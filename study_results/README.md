# Study Results: Data Files

This directory contains the CSV data outputs from our analysis of the drug database. Each file corresponds to a specific mini-study examining aspects of drug prohibition's effects.

## Files and Contents

### 1. publication_lag.csv
**Description:** Documents the delay between drug testing and publication of results.
**Columns:**
- `year`: Year of drug test date
- `sample_count`: Number of samples tested in that year
- `mean_lag_days`: Average days between testing and publication
- `min_lag_days`: Minimum delay in days (negative values represent rare cases of backdated publications)
- `max_lag_days`: Maximum delay in days

**Policy Relevance:** Long publication lags indicate failures in timely information sharing critical for harm reduction.

### 2. nps_emergence.csv
**Description:** Tracks the appearance of new psychoactive substances (NPS) over time.
**Columns:**
- `year`: Year of first appearance
- `new_substances`: Count of substances first observed that year

**Policy Relevance:** Accelerating new substance emergence demonstrates the "chemical whack-a-mole" effect of drug scheduling.

### 3. fentanyl_heroin.csv
**Description:** Tracks the presence of fentanyl in samples sold as heroin.
**Columns:**
- `year`: Year of sample testing
- `fentanyl_in_heroin_count`: Number of samples containing fentanyl that were sold as heroin

**Policy Relevance:** Demonstrates the shift toward more potent, concentrated substances (Iron Law of Prohibition).

### 4. adulterant_complexity.csv
**Description:** Measures the number of substances per sample over time.
**Columns:**
- `year`: Year of testing
- `samples`: Number of samples tested that year
- `avg_substances_per_sample`: Average number of distinct substances per sample
- `max_substances`: Maximum number of substances found in any single sample that year

**Policy Relevance:** Increasing complexity indicates deteriorating quality control and heightened unpredictability.

### 5. mislabeling.csv
**Description:** Documents how frequently drug samples don't contain what they're marketed as.
**Columns:**
- `year`: Year of testing
- `total_samples`: Number of samples with "sold as" data
- `mislabeled_count`: Number of samples that didn't contain what they were sold as
- `mislabeled_percentage`: Percentage of samples that were mislabeled

**Policy Relevance:** High mislabeling rates demonstrate collapse of consumer protection under prohibition.

### 6. cross_contamination.csv
**Description:** Tracks mixing of stimulants (cocaine, methamphetamine) in opioid samples (heroin, fentanyl).
**Columns:**
- `year`: Year of testing
- `contaminated_samples`: Count of samples with both substance types

**Policy Relevance:** Cross-class contamination presents particularly elevated overdose risks from unpredictable drug interactions.

## Usage Notes

These data files are designed to be imported into analysis and visualization tools (e.g., Python with pandas, R, Excel) for further exploration and chart generation.

For the source queries used to generate each file, see the `study_queries.md` file in the parent directory.