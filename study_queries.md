# Drug Analysis Queries

This document contains all the Cypher queries used in our analysis of the drug database, organized by study topic.

## 1. Publication Lag Analysis

```cypher
// Publication Lag Analysis - calculating days manually
MATCH (d:Drug)
WHERE d.test_date IS NOT NULL AND d.publication_date IS NOT NULL
WITH 
     d.test_date.year AS test_year,
     d.test_date.month AS test_month,
     d.test_date.day AS test_day,
     d.publication_date.year AS pub_year,
     d.publication_date.month AS pub_month,
     d.publication_date.day AS pub_day,
     d.test_date.year AS year
WITH 
     year,
     (pub_year * 365 + pub_month * 30 + pub_day) - (test_year * 365 + test_month * 30 + test_day) AS lag_days
RETURN 
     year, 
     COUNT(*) AS sample_count,
     AVG(lag_days) AS mean_lag_days,
     MIN(lag_days) AS min_lag_days,
     MAX(lag_days) AS max_lag_days
ORDER BY year;
```

## 2. Novel Psychoactive Substances (NPS) Emergence

```cypher
// NPS Emergence - First appearance of substances
MATCH (d:Drug)-[:HAS_SUBSTANCE]->(s:Substance)
WITH s.name AS substance, MIN(d.test_date) AS first_seen
RETURN 
    first_seen.year AS year, 
    COUNT(*) AS new_substances
ORDER BY year;
```

## 3. Potency Escalation - Fentanyl in Heroin

```cypher
// Potency Escalation - Fentanyl in heroin samples (simplified regex)
MATCH (d:Drug)-[:SOLD_AS]->(ds:DrugSoldAs)
WHERE toLower(ds.drug) CONTAINS 'heroin'
WITH d
MATCH (d)-[:HAS_SUBSTANCE]->(s:Substance)
WHERE toLower(s.name) CONTAINS 'fentanyl'
RETURN 
    d.test_date.year AS year, 
    COUNT(DISTINCT d) AS fentanyl_in_heroin_count
ORDER BY year;
```

## 4. Adulterant Complexity Study

```cypher
// Adulterant Complexity - Substances per sample over time
MATCH (d:Drug)-[:HAS_SUBSTANCE]->(s:Substance)
WITH d, d.test_date.year AS year, COUNT(DISTINCT s) AS substance_count
RETURN 
    year, 
    COUNT(d) AS samples,
    AVG(substance_count) AS avg_substances_per_sample,
    MAX(substance_count) AS max_substances
ORDER BY year;
```

## 5. Mislabeling Analysis

```cypher
// Mislabeling Analysis - What drugs are sold as vs. what they contain
MATCH (d:Drug)-[:SOLD_AS]->(ds:DrugSoldAs), (d)-[:HAS_SUBSTANCE]->(s:Substance)
WITH 
    d.test_date.year AS year,
    ds.drug AS sold_as,
    COLLECT(DISTINCT s.name) AS substances,
    d
WITH
    year,
    d,
    sold_as,
    substances,
    CASE WHEN ANY(substance IN substances WHERE toLower(substance) CONTAINS toLower(sold_as)) THEN 'Matched' ELSE 'Mislabeled' END AS match_status
RETURN
    year,
    COUNT(d) AS total_samples,
    SUM(CASE WHEN match_status = 'Mislabeled' THEN 1 ELSE 0 END) AS mislabeled_count,
    ROUND(100.0 * SUM(CASE WHEN match_status = 'Mislabeled' THEN 1 ELSE 0 END) / COUNT(d)) AS mislabeled_percentage
ORDER BY year;
```

## 6. Geographic Source Displacement

```cypher
// Geographic Source Displacement - Focus on methamphetamine
MATCH (d:Drug)-[:SOURCE_LOCATION]->(loc:SourceLocation)
WHERE toLower(d.name) CONTAINS 'meth'
WITH loc.location AS place, d.test_date.year AS year, COUNT(*) AS count
WHERE count > 4  // Filter for statistical significance
RETURN place, year, count
ORDER BY year, count DESC
LIMIT 20;
```

## 7. Cross-Contamination of Drug Classes

```cypher
// Cross-Contamination Study - Stimulants in Opioids
MATCH (d:Drug)-[:HAS_SUBSTANCE]->(s1:Substance), (d)-[:HAS_SUBSTANCE]->(s2:Substance)
WHERE 
    (toLower(s1.name) CONTAINS 'heroin' OR toLower(s1.name) CONTAINS 'fentanyl') AND
    (toLower(s2.name) CONTAINS 'meth' OR toLower(s2.name) CONTAINS 'cocaine')
RETURN 
    d.test_date.year AS year,
    COUNT(DISTINCT d) AS contaminated_samples
ORDER BY year;
```