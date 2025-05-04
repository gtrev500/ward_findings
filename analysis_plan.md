# Drug Database Analysis Plan

## Overview
This analysis aims to examine patterns in our drug database that could validate criticisms of the War on Drugs. We'll conduct seven mini-studies, each focusing on a specific aspect of drug prohibition failure.

## Analysis Structure

1. **Setup & Data Collection**
   - Define and execute specific Cypher queries for each mini-study
   - Save results to local files for analysis

2. **Analysis & Visualization**
   - Process query results
   - Generate visualizations for key metrics
   - Identify trends that support or refute our hypotheses

3. **Documentation**
   - Document findings for each mini-study
   - Compile overall conclusions
   - Note limitations and potential further research

## Mini-Studies Implementation Plan

### 1. Potency Escalation Study
**Question:** Has prohibition pushed suppliers toward stronger, more compact drugs?

**Implementation:**
- Identify opioids/fentanyl analogs in our database
- Track yearly prevalence of fentanyl analogs in samples sold as heroin
- Analyze potency changes over time

**Adapted Query:**
```cypher
// Find fentanyl-containing samples
MATCH (d:Drug)-[:HAS_SUBSTANCE]->(s:Substance) 
WHERE s.name =~ '(?i).*fentanyl.*' 
RETURN d.name, s.name, d.test_date
ORDER BY d.test_date;

// Track fentanyl in heroin samples over time
MATCH (d:Drug)-[:SOLD_AS]->(ds:DrugSoldAs)
WHERE ds.drug =~ '(?i).*heroin.*'
MATCH (d)-[:HAS_SUBSTANCE]->(s:Substance)
WHERE s.name =~ '(?i).*fentanyl.*'
RETURN d.test_date.year AS year, count(DISTINCT d) AS count
ORDER BY year;
```

### 2. Adulterant Complexity Study
**Question:** Has prohibition led to increased chemical "noise" and consumer risk?

**Implementation:**
- Calculate number of substances per sample over time
- Track mean and median substance count by year

**Adapted Query:**
```cypher
MATCH (d:Drug)-[:HAS_SUBSTANCE]->(s:Substance)
WITH d, d.test_date.year AS year, count(DISTINCT s) AS substance_count
RETURN year, avg(substance_count) AS mean_substances, 
       percentileCont(substance_count, 0.5) AS median_substances
ORDER BY year;
```

### 3. Mislabeling Analysis
**Question:** How often does what's sold not match what's actually in the substance?

**Implementation:**
- Compare what drugs were sold as versus their actual content
- Calculate mislabeling percentage by year and drug type

**Adapted Query:**
```cypher
MATCH (d:Drug)-[:SOLD_AS]->(ds:DrugSoldAs)
MATCH (d)-[:HAS_SUBSTANCE]->(s:Substance)
WITH d, ds.drug AS sold_as, collect(s.name) AS contains
RETURN d.name, sold_as, contains, 
       CASE WHEN sold_as IN contains THEN false ELSE true END AS mislabeled;
```

### 4. Geographic Source Displacement
**Question:** Do enforcement actions move rather than eliminate production?

**Implementation:**
- Select key drugs (e.g., methamphetamine, cocaine)
- Track source locations over time
- Identify shifts in production geography

**Adapted Query:**
```cypher
MATCH (d:Drug)-[:SOURCE_LOCATION]->(loc:SourceLocation)
WHERE d.name =~ '(?i).*(meth|amphetamine).*'
WITH loc.location AS place, d.test_date.year AS year, count(*) AS count
RETURN place, year, count
ORDER BY place, year;
```

### 5. Publication Lag Analysis
**Question:** Do slow data pipelines hinder timely public health responses?

**Implementation:**
- Calculate time between test and publication dates
- Track median lag by quarter/year

**Adapted Query:**
```cypher
MATCH (d:Drug)
WHERE d.test_date IS NOT NULL AND d.publication_date IS NOT NULL
WITH d, duration.inDays(d.test_date, d.publication_date) AS lag_days, 
     d.test_date.year AS year
RETURN year, 
       avg(lag_days) AS mean_days,
       percentileCont(lag_days, 0.5) AS median_days,
       max(lag_days) AS max_days
ORDER BY year;
```

### 6. Cross-Contamination Study
**Question:** Does prohibition lead to unpredictable mixing of drug classes?

**Implementation:**
- Identify samples containing substances from multiple drug classes
- Track cross-contamination over time

**Adapted Query:**
```cypher
// Example: Opioids containing stimulants
MATCH (d:Drug)-[:HAS_SUBSTANCE]->(s1:Substance),
      (d)-[:HAS_SUBSTANCE]->(s2:Substance)
WHERE s1.name =~ '(?i).*(heroin|fentanyl|morphine).*'
  AND s2.name =~ '(?i).*(cocaine|amphetamine|methamphetamine).*'
RETURN d.name, d.test_date, s1.name AS opioid, s2.name AS stimulant
ORDER BY d.test_date;
```

### 7. Novel Psychoactive Substances (NPS) Emergence
**Question:** Does scheduling lead to a cycle of new synthetic drugs?

**Implementation:**
- Identify first appearance of each substance in the database
- Count new substances per year/quarter

**Adapted Query:**
```cypher
MATCH (d:Drug)-[:HAS_SUBSTANCE]->(s:Substance)
WITH s.name AS substance, min(d.test_date) AS first_seen
RETURN first_seen.year AS year, count(*) AS new_substances
ORDER BY year;
```

## Output and Documentation
For each study, we'll generate:
1. Raw data files with query results
2. Analysis notes with key findings
3. Visualizations of critical trends
4. A summary document connecting findings to War on Drugs criticism

## Limitations
- Our analysis is bounded by the time period covered in the database
- We can identify correlations but not definitively prove causation
- Some policy events may fall outside our dataset's timeline