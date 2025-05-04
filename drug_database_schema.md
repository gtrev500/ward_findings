# Drug Database Schema and Sample Data

## Database Schema

### Nodes
1. **Drug** (19,032 nodes)
   - Properties: id (Integer), name (String), test_date (LocalDateTime), publication_date (LocalDateTime)

2. **Substance** (5,395 nodes)
   - Properties: name (String), quanity (String) [Note: "quanity" appears to be misspelled in the schema]

3. **DrugSoldAs** (1,235 nodes)
   - Properties: drug (String)

4. **SourceLocation** (1,226 nodes)
   - Properties: location (String)

### Relationships
1. **HAS_SUBSTANCE** (38,935 edges)
   - Connects: Drug → Substance

2. **SOLD_AS** (15,428 edges)
   - Connects: Drug → DrugSoldAs

3. **SOURCE_LOCATION** (19,032 edges)
   - Connects: Drug → SourceLocation

## Sample Data

### Sample Drugs
```
{'id': 1, 'name': 'Euro', 'publication_date': '2001-04-01', 'test_date': '2001-04-01'}
{'id': 2, 'name': 'Butterfly', 'publication_date': '2001-04-01', 'test_date': '2001-04-01'}
{'id': 3, 'name': 'Happy Campers', 'publication_date': '2001-04-01', 'test_date': '2001-04-01'}
{'id': 4, 'name': 'Wannabe', 'publication_date': '2001-04-01', 'test_date': '2001-04-01'}
{'id': 5, 'name': 'Mitsubishi', 'publication_date': '2001-04-01', 'test_date': '2001-04-01'}
```

### Sample Substances
```
{"name": "MDMA", "quanity": "1"}
{"name": "Methamphetamine", "quanity": "1"}
{"name": "DXM", "quanity": "10"}
{"name": "Caffeine", "quanity": "3"}
{"name": "Ephedrine/Pseudoephedrine", "quanity": "1"}
```

### Sample DrugSoldAs
```
{"drug": "Cocaine"}
{"drug": "MDMA"}
{"drug": "MDAI, 5-MeO-DALT, 2C-I"}
{"drug": "Ketamine"}
{"drug": "Molly"}
```

### Sample SourceLocations
```
{"location": "AL"}
{"location": "Orlando, FL"}
{"location": "New Orleans, LA"}
{"location": "Eau Claire, WI"}
{"location": "Ann Arbor, MI"}
```

### Sample Relationships

#### Drug-HAS_SUBSTANCE-Substance
```
{"d.name": "Euro", "s.name": "MDMA", "s.quanity": "1"}
{"d.name": "Butterfly", "s.name": "Methamphetamine", "s.quanity": "1"}
{"d.name": "Happy Campers", "s.name": "DXM", "s.quanity": "10"}
{"d.name": "Happy Campers", "s.name": "Caffeine", "s.quanity": "3"}
{"d.name": "Happy Campers", "s.name": "Ephedrine/Pseudoephedrine", "s.quanity": "1"}
```

#### Drug-SOLD_AS-DrugSoldAs
```
{"d.name": "Cocaine", "ds.drug": "Cocaine"}
{"d.name": "Blue Star", "ds.drug": "MDMA"}
{"d.name": "Apple Pokeball", "ds.drug": "MDMA"}
{"d.name": "Capsule", "ds.drug": "Cocaine"}
{"d.name": "Broken Capsule 27016", "ds.drug": "MDAI, 5-MeO-DALT, 2C-I"}
```

#### Drug-SOURCE_LOCATION-SourceLocation
```
{"d.name": "Euro", "l.location": "AL"}
{"d.name": "Butterfly", "l.location": "Orlando, FL"}
{"d.name": "Happy Campers", "l.location": "New Orleans, LA"}
{"d.name": "Wannabe", "l.location": "Eau Claire, WI"}
{"d.name": "Mitsubishi", "l.location": "Ann Arbor, MI"}
```

## Database Overview
This graph database tracks information about drugs, their composition (substances), how they're marketed/sold, and their geographic origins. Each drug has a test date and publication date, potentially indicating when it was analyzed and when that information was published.