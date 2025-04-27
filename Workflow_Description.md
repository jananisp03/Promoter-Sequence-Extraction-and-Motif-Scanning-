# Detailed Workflow Description

This document provides a technical description of each step in the "Promoter Sequence Extraction and Motif Scanning" Galaxy workflow.

## Workflow Steps

### 1. Input: Gene Annotation (GTF/GFF)
- **Description**: Gene annotation file containing genomic features
- **Format**: GTF or GFF
- **Purpose**: Provides gene coordinates and structures

### 2. Input: Reference Genome (FASTA)
- **Description**: Genome sequence file
- **Format**: FASTA
- **Purpose**: Provides the DNA sequence for extracting promoters

### 3. Input: Motif File (MEME)
- **Description**: Transcription factor binding motifs
- **Format**: MEME
- **Purpose**: Defines motif patterns to search for in promoter sequences

### 4. Convert GTF to BED12
- **Tool**: Convert GTF to BED12 (iuc/gtftobed12)
- **Description**: Converts gene annotations from GTF to BED12 format
- **Parameters**: Default settings
- **Output**: BED12 file containing gene coordinates

### 5. Gene BED To Exon/Intron/Codon BED
- **Tool**: Gene BED To Exon/Intron/Codon BED (gene2exon1)
- **Description**: Extracts transcribed regions from gene annotations
- **Parameters**: Region = "transcribed"
- **Output**: BED file containing transcribed regions

### 6. bedtools SlopBed
- **Tool**: bedtools SlopBed (iuc/bedtools/bedtools_slopbed)
- **Description**: Extends regions by adding bases to each end
- **Parameters**: 
  - Base pairs to add: 1
  - Genome reference: CHM13_T2T_v2.0
- **Output**: Extended BED regions

### 7. Compute
- **Tool**: Compute (devteam/column_maker/Add_a_column1)
- **Description**: Calculates region sizes and adjusts coordinates based on strand
- **Parameters**: 
  - Expression 1: `c3-c2` (calculates region size)
  - Expression 2: Conditional expression to adjust coordinates based on strand
- **Output**: BED file with adjusted coordinates

### 8. bedtools FlankBed
- **Tool**: bedtools FlankBed (iuc/bedtools/bedtools_flankbed)
- **Description**: Generates flanking regions (promoters) for each gene
- **Parameters**: Base pairs to add: 1
- **Output**: BED file containing promoter regions

### 9. bedtools getfasta
- **Tool**: bedtools getfasta (iuc/bedtools/bedtools_getfastabed)
- **Description**: Extracts promoter sequences from the reference genome
- **Parameters**:
  - Name: true
  - nameOnly: true
  - Strand: true
- **Output**: FASTA file containing promoter sequences

### 10. FIMO
- **Tool**: FIMO (iuc/meme_fimo/meme_fimo)
- **Description**: Scans promoter sequences for transcription factor binding motifs
- **Parameters**:
  - Basic options
  - Output format: Text
  - Change output datatype to tabular
- **Output**: Tabular file containing motif matches

## Data Flow

1. Gene annotations → Convert to BED12 → Extract transcribed regions
2. Transcribed regions → Extend regions → Adjust coordinates → Generate flanking regions
3. Flanking regions + Reference genome → Extract promoter sequences
4. Promoter sequences + Motif file → Scan for motifs → Output motif matches

## Note on Coordinate Systems

This workflow uses 0-based coordinate system (BED format) for genomic features. When converting between coordinate systems, special care is taken to properly account for the strand orientation of genes.
