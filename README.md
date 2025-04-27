# Promoter Sequence Extraction and Motif Scanning Galaxy Workflow

This Galaxy workflow extracts promoter sequences from gene annotations and scans them for transcription factor binding motifs. It takes gene annotations (GTF/GFF), a reference genome (FASTA), and a motif file (MEME format) as inputs, and produces promoter sequences and motif matches as outputs.

## Workflow Overview

This workflow performs the following steps:

1. Converts gene annotations from GTF/GFF to BED12 format
2. Extracts transcribed regions from the gene annotations
3. Extends the regions by 1 base pair
4. Computes region sizes and adjusts coordinates
5. Generates flanking regions (promoters)
6. Extracts promoter sequences from the reference genome
7. Scans promoter sequences for transcription factor binding motifs

## Inputs

- **Gene Annotation (GTF/GFF)**: Gene annotations containing genomic features
- **Reference Genome (FASTA)**: Genome sequence in FASTA format
- **Motif File (MEME)**: Transcription factor binding motifs in MEME format

## Outputs

- **Promoter Sequences (FASTA)**: Extracted promoter sequences
- **Motif Matches (Tabular)**: Motif scanning results showing binding site matches

## Usage

1. Import the workflow into your Galaxy instance
2. Upload your gene annotation file (GTF/GFF)
3. Upload your reference genome (FASTA)
4. Upload your motif file (MEME format)
5. Run the workflow with your inputs

## Requirements

This workflow requires a Galaxy instance with the following tools installed:

- Convert GTF to BED12 (iuc/gtftobed12)
- Gene BED To Exon/Intron/Codon BED (gene2exon1)
- bedtools SlopBed (iuc/bedtools/bedtools_slopbed)
- Compute (devteam/column_maker/Add_a_column1)
- bedtools FlankBed (iuc/bedtools/bedtools_flankbed)
- bedtools getfasta (iuc/bedtools/bedtools_getfastabed)
- FIMO (iuc/meme_fimo/meme_fimo)

## License

This workflow is released under the MIT License. See the [LICENSE](LICENSE) file for details.
