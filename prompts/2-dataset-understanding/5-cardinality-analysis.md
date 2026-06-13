TASK: Cardinality Analysis

Read:

- docs/2-dataset-understanding/dataset_schema.md

Analyze all categorical features.

For every categorical feature calculate:

- Unique Count
- Cardinality Level

Classify as:

- Low Cardinality (<10)
- Medium Cardinality (10-50)
- High Cardinality (>50)

Create:

docs/2-dataset-understanding/cardinality_analysis.md

Include:

# Cardinality Analysis

| Feature | Unique Values | Classification |

Identify:

- Potential One-Hot Encoding candidates
- Potential Target Encoding candidates
- Potential Frequency Encoding candidates

Do NOT perform encoding.

Save the file and display contents.