# EDA Pipeline Structure Directive

This document establishes the standard organizational structure for all Exploratory Data Analysis (EDA) pipelines in this project. Following this structure ensures consistency, reproducibility, and clarity in our analyses.

## Directory Structure

```
/project_name/
├── README.md                      # Project overview & navigation
├── database_schema.md             # Documentation of data source structure
├── analysis_context.md            # Background and contextual information
├── analysis_plan.md               # Methodology and structured approach
├── analysis_findings.md           # Key findings and implications
├── study_queries.md               # Queries used for each analysis component
├── eda_structure_directive.md     # This file - organizational standard
└── study_results/                 # Data output directory
    ├── README.md                  # Detailed description of each data file
    └── [topic]_[metric].csv       # CSV data files with consistent naming
```

## Required Documentation Files

### 1. README.md
- Project title and high-level summary
- Directory structure explanation
- Brief overview of each analysis component
- Key findings summary
- Methodology overview
- Cross-references to other documents

### 2. database_schema.md
- Complete documentation of data source structure
- Tables/collections/nodes and their relationships
- Field descriptions and data types
- Sample records for each entity type
- Notes on data limitations or peculiarities

### 3. analysis_context.md
- Background information relevant to the analysis
- Scope and limitations of the dataset
- Relevant external factors affecting interpretation
- Prior research or knowledge that informs the analysis

### 4. analysis_plan.md
- Clear statement of analysis objectives
- Step-by-step methodology for each component
- Query/code approach for each analysis question
- Expected outputs and their formats
- Measurement definitions and calculation methods

### 5. analysis_findings.md
- Detailed results for each analysis component
- Interpretation of patterns and trends identified
- Connection to broader context or hypotheses
- Implications of findings
- Limitations and areas for further investigation

### 6. study_queries.md
- All queries used in the analysis, organized by topic
- Comments explaining query logic and purpose
- Parameters or variations used
- Performance notes where relevant

## Data Output Standards

### Directory Organization
- All data outputs stored in `/study_results/` directory
- One CSV file per distinct analysis metric
- README.md file explaining all outputs

### File Naming Convention
- Format: `[topic]_[metric].csv`
- Example: `publication_lag.csv`, `cross_contamination.csv`
- Use lowercase with underscores for consistency

### CSV File Requirements
- Include header row with clear column names
- Document all columns in the README.md
- Use consistent date formats (YYYY-MM-DD)
- Include raw counts alongside percentages where applicable

### README.md Within Results Directory
For each data file, document:
- File description and purpose
- Each column's meaning and units
- Calculation method for derived metrics
- Relevance to overall analysis questions
- Usage notes for visualization or further analysis

## Implementation Process

1. **Initialize Structure**: Create the directory structure and empty files at project start
2. **Document As You Go**: Update documentation files during analysis, not just at the end
3. **Cross-Reference**: Ensure files reference each other where appropriate
4. **Review Completeness**: Verify all components are documented before finalizing
5. **Maintain Consistency**: Follow naming and organizational patterns throughout

## Benefits of Standardization

This structured approach ensures:
- Easy navigation across different analyses
- Clear documentation of methodologies
- Reproducibility of results
- Consistent data output formats
- Simplified handoff between team members
- Efficient creation of reports and visualizations

All EDA pipelines in this project must follow this structure unless explicitly exempted with documented justification.