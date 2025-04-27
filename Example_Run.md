# Example Run: Promoter Sequence Extraction and Motif Scanning

This document demonstrates an example run of the workflow with sample data and expected results.

## Sample Input Data

### 1. Gene Annotation (GTF)
```
chr1	HAVANA	gene	11869	14409	.	+	.	gene_id "ENSG00000223972"; gene_name "DDX11L1"; gene_source "HAVANA"; gene_biotype "transcribed_unprocessed_pseudogene";
chr1	HAVANA	transcript	11869	14409	.	+	.	gene_id "ENSG00000223972"; transcript_id "ENST00000456328"; gene_name "DDX11L1"; gene_source "HAVANA"; gene_biotype "transcribed_unprocessed_pseudogene"; transcript_name "DDX11L1-202"; transcript_source "HAVANA"; transcript_biotype "processed_transcript";
chr1	HAVANA	exon	11869	12227	.	+	.	gene_id "ENSG00000223972"; transcript_id "ENST00000456328"; gene_name "DDX11L1"; gene_source "HAVANA"; gene_biotype "transcribed_unprocessed_pseudogene"; transcript_name "DDX11L1-202"; transcript_source "HAVANA"; transcript_biotype "processed_transcript"; exon_number 1; exon_id "ENSE00002234944";
chr1	HAVANA	exon	12613	12721	.	+	.	gene_id "ENSG00000223972"; transcript_id "ENST00000456328"; gene_name "DDX11L1"; gene_source "HAVANA"; gene_biotype "transcribed_unprocessed_pseudogene"; transcript_name "DDX11L1-202"; transcript_source "HAVANA"; transcript_biotype "processed_transcript"; exon_number 2; exon_id "ENSE00003582793";
chr1	HAVANA	exon	13221	14409	.	+	.	gene_id "ENSG00000223972"; transcript_id "ENST00000456328"; gene_name "DDX11L1"; gene_source "HAVANA"; gene_biotype "transcribed_unprocessed_pseudogene"; transcript_name "DDX11L1-202"; transcript_source "HAVANA"; transcript_biotype "processed_transcript"; exon_number 3; exon_id "ENSE00002312635";
```

### 2. Reference Genome (FASTA)
```
>chr1
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
...
TAACCCTAACCCTAACCCTAACCCTAACCCTAACCCTAACCCTAACCCT
AACCCTAACCCTATCGTCAAAGTTCCTATCGATCCCTTAATCCTAGCGC
...
```

### 3. Motif File (MEME) - Example with CTCF motif
```
MEME version 4.11.3

ALPHABET= ACGT

strands: + -

Background letter frequencies
A 0.25 C 0.25 G 0.25 T 0.25

MOTIF CTCF CTCF

letter-probability matrix: alength= 4 w= 19 nsites= 20 E= 0
  0.095  0.000  0.905  0.000
  0.003  0.000  0.997  0.000
  0.000  0.004  0.000  0.996
  0.421  0.358  0.004  0.217
  0.047  0.003  0.948  0.002
  0.960  0.006  0.030  0.004
  0.992  0.002  0.004  0.002
  0.003  0.004  0.991  0.002
  0.000  0.000  1.000  0.000
  0.001  0.001  0.001  0.997
  0.002  0.000  0.997  0.001
  0.987  0.005  0.004  0.004
  0.005  0.009  0.010  0.976
  0.009  0.959  0.024  0.008
  0.003  0.000  0.001  0.996
  0.985  0.003  0.000  0.012
  0.000  0.996  0.002  0.002
  0.015  0.007  0.975  0.003
  0.000  0.999  0.000  0.001
```

## Expected Outputs

### 1. Promoter Sequences (Extract from output FASTA)
```
>ENSG00000223972_DDX11L1(+)
ACTCCTAGCCCTAACCCTAACCCTAACCCTAACCCTAACCCT
>ENSG00000227232_WASH7P(-)
AGCGCGTCCCGGTGTGAGGGTCGGGGGCGAGTGCACCCGGAG
>ENSG00000278267_MIR6859-1(-)
AGAAAGAGCCAACGCGGTGAGTGAGGAGGTGGGGCGGGGCCT
```

### 2. Motif Matches (Extract from FIMO output)
```
#pattern name	sequence name	start	stop	strand	score	p-value	q-value	matched sequence
CTCF	ENSG00000227232_WASH7P(-)	18	36	+	15.2793	7.31e-06	0.0291	CGGTGTGAGGGTCGGGGGC
CTCF	ENSG00000278267_MIR6859-1(-)	23	41	-	14.9217	9.31e-06	0.0291	GGAGGTGGGGCGGGGCCTG
```

## Workflow Visualization

Workflow steps for the example run:

1. Input files uploaded to Galaxy
2. GTF converted to BED12 format
3. Transcribed regions extracted (11869-14409 for DDX11L1)
4. Regions extended by 1bp
5. Coordinates adjusted based on strand
6. Flanking regions (promoters) generated
7. Promoter sequences extracted from reference genome
8. FIMO scan identified CTCF binding sites in two promoters

## Interpretation of Results

In this example run:
- We identified promoter regions for three genes (DDX11L1, WASH7P, MIR6859-1)
- CTCF binding motifs were found in the promoters of WASH7P and MIR6859-1
- The binding sites had p-values < 1e-5, suggesting high confidence matches
- No CTCF binding site was found in the DDX11L1 promoter

This demonstrates the workflow's ability to extract promoter sequences and identify transcription factor binding sites, which can provide insights into gene regulation mechanisms.
