# Usage Guide: Promoter Sequence Extraction and Motif Scanning

This guide provides detailed instructions on how to use the "Promoter Sequence Extraction and Motif Scanning" Galaxy workflow.

## Prerequisites

Before using this workflow, you need:

1. Access to a Galaxy instance with all required tools installed
2. Gene annotation file in GTF/GFF format
3. Reference genome in FASTA format
4. Transcription factor binding motifs in MEME format

## Step-by-Step Instructions

### 1. Import the Workflow

1. Download the workflow file (`Galaxy-Workflow-Promoter_Sequence_Extraction_and_Motif_Scanning.ga`) from this repository
2. Log in to your Galaxy instance
3. Go to "Workflow" in the top menu
4. Click on the "Import" button
5. Choose "Import from file" and select the downloaded workflow file
6. Click "Import workflow"

### 2. Prepare Input Data

1. Upload your gene annotation file (GTF/GFF format) to Galaxy
2. Upload your reference genome (FASTA format) to Galaxy
3. Upload your motif file (MEME format) to Galaxy

### 3. Run the Workflow

1. Go to "Workflow" in the top menu
2. Find the "Promoter Sequence Extraction and Motif Scanning" workflow and click on the run button (▶️)
3. In the workflow form:
   - Select your gene annotation file for "Gene Annotation (GTF/GFF)"
   - Select your reference genome file for "Reference Genome (FASTA)"
   - Select your motif file for "Motif File (MEME)"
4. Click "Run workflow"

### 4. Interpreting Results

The workflow produces two main outputs:

#### Promoter Sequences (FASTA)
This file contains the extracted promoter sequences from the gene annotations. Each sequence is named according to the gene identifier.

#### Motif Matches (Tabular)
This file contains the results of scanning the promoter sequences for transcription factor binding motifs. It includes:
- Pattern name (motif identifier)
- Sequence name (promoter identifier)
- Start position of the match
- End position of the match
- Strand (+/-)
- Score of the match
- p-value
- q-value (adjusted p-value)
- Matched sequence

### 5. Downstream Analysis

You can use the results for various downstream analyses:
- Identify enriched binding motifs in your gene set
- Correlate motif presence with gene expression data
- Analyze motif distribution relative to transcription start sites
- Compare motif occurrences across different gene sets

## Troubleshooting

If you encounter issues with the workflow:

1. Check that your input files are in the correct format
2. Ensure your Galaxy instance has all required tools installed
3. Verify that your reference genome matches your gene annotations
4. Check the MEME motif file format is correct
