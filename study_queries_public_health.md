# Public Health Impact Analysis Queries

This document contains the Cypher queries used for analyzing public health impacts in the drug database.

## 1. High-Risk Substance Prevalence

```cypher
// Track emergence of high-risk substances over time
MATCH (d:Drug)-[:HAS_SUBSTANCE]->(s:Substance)
WHERE 
    toLower(s.name) CONTAINS 'fentanyl' OR
    toLower(s.name) CONTAINS 'heroin' OR
    toLower(s.name) CONTAINS 'xylazine'
WITH d.test_date.year AS year, 
     CASE 
         WHEN toLower(s.name) CONTAINS 'fentanyl' THEN 'Fentanyl Analogs'
         WHEN toLower(s.name) CONTAINS 'heroin' THEN 'Heroin'
         WHEN toLower(s.name) CONTAINS 'xylazine' THEN 'Xylazine'
         ELSE 'Other'
     END AS substance_category,
     COUNT(DISTINCT d) AS sample_count
RETURN 
    year, 
    substance_category,
    sample_count
ORDER BY year, substance_category;
```

## 2. Dangerous Combinations Analysis

```cypher
// Analyze co-occurrence of high-risk substances
MATCH (d:Drug)-[:HAS_SUBSTANCE]->(s1:Substance), (d)-[:HAS_SUBSTANCE]->(s2:Substance)
WHERE 
    (toLower(s1.name) CONTAINS 'fentanyl' AND toLower(s2.name) CONTAINS 'xylazine') OR
    (toLower(s1.name) CONTAINS 'fentanyl' AND toLower(s2.name) CONTAINS 'heroin') OR
    (toLower(s1.name) CONTAINS 'fentanyl' AND toLower(s2.name) CONTAINS 'benzo') OR
    (toLower(s1.name) CONTAINS 'heroin' AND toLower(s2.name) CONTAINS 'xylazine')
WITH 
    d.test_date.year AS year,
    CASE
        WHEN toLower(s1.name) CONTAINS 'fentanyl' AND toLower(s2.name) CONTAINS 'xylazine' THEN 'Fentanyl + Xylazine'
        WHEN toLower(s1.name) CONTAINS 'fentanyl' AND toLower(s2.name) CONTAINS 'heroin' THEN 'Fentanyl + Heroin'
        WHEN toLower(s1.name) CONTAINS 'fentanyl' AND toLower(s2.name) CONTAINS 'benzo' THEN 'Fentanyl + Benzodiazepine'
        WHEN toLower(s1.name) CONTAINS 'heroin' AND toLower(s2.name) CONTAINS 'xylazine' THEN 'Heroin + Xylazine'
        ELSE 'Other Combination'
    END AS combination,
    COUNT(DISTINCT d) AS sample_count
RETURN 
    year, 
    combination,
    sample_count
ORDER BY year, combination;
```

## 3. Fentanyl Analog Timeline

```cypher
// Emergence of fentanyl analogs over time
MATCH (d:Drug)-[:HAS_SUBSTANCE]->(s:Substance)
WHERE toLower(s.name) CONTAINS 'fentanyl'
WITH s.name AS analog, MIN(d.test_date) AS first_detected
RETURN 
    analog,
    first_detected.year AS year_first_detected,
    first_detected.month AS month_first_detected
ORDER BY first_detected;
```

## 4. Early Warning System Analysis

```cypher
// Analyze detection patterns for key substances
WITH [
    'Xylazine', 
    '4-Fluorofentanyl',
    'Despropionyl-4-fluorofentanyl',
    'Acetylfentanyl'
] AS substances_to_analyze

MATCH (d:Drug)-[:HAS_SUBSTANCE]->(s:Substance)
WHERE s.name IN substances_to_analyze
WITH 
    s.name AS substance, 
    d.test_date.year AS year, 
    d.test_date.month AS month,
    COUNT(*) AS detections
RETURN 
    substance,
    year,
    month,
    detections
ORDER BY substance, year, month;
```