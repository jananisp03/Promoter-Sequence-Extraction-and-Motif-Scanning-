# Galaxy Tools Requirements

This document lists all the Galaxy tools required for the "Promoter Sequence Extraction and Motif Scanning" workflow and provides installation instructions for Galaxy administrators.

## Required Tools

| Tool Name | Tool ID | Version | Repository |
|-----------|---------|---------|------------|
| Convert GTF to BED12 | toolshed.g2.bx.psu.edu/repos/iuc/gtftobed12/gtftobed12 | 357 | iuc/gtftobed12 |
| Gene BED To Exon/Intron/Codon BED | gene2exon1 | 1.0.0 | Built-in Galaxy tool |
| bedtools SlopBed | toolshed.g2.bx.psu.edu/repos/iuc/bedtools/bedtools_slopbed | 2.31.1+galaxy0 | iuc/bedtools |
| Compute | toolshed.g2.bx.psu.edu/repos/devteam/column_maker/Add_a_column1 | 2.1 | devteam/column_maker |
| bedtools FlankBed | toolshed.g2.bx.psu.edu/repos/iuc/bedtools/bedtools_flankbed | 2.31.1+galaxy0 | iuc/bedtools |
| bedtools getfasta | toolshed.g2.bx.psu.edu/repos/iuc/bedtools/bedtools_getfastabed | 2.31.1+galaxy0 | iuc/bedtools |
| FIMO | toolshed.g2.bx.psu.edu/repos/iuc/meme_fimo/meme_fimo | 5.5.6+galaxy0 | iuc/meme_fimo |

## Installation Instructions

### For Galaxy Administrators

1. Access your Galaxy Admin interface
2. Go to "Admin" → "Tool Management" → "Install and Uninstall"
3. Search for each tool by ID or name
4. Select the correct version and install

### Manual Installation via Command Line

You can also install tools using the Galaxy API or `ephemeris` tool:

```bash
# Install ephemeris if not already installed
pip install ephemeris

# Create a tool list YAML file
cat > tool_list.yaml << EOF
tools:
- name: gtftobed12
  owner: iuc
  tool_panel_section_label: "Convert Formats"
  revisions:
  - b026dae67fba

- name: bedtools
  owner: iuc
  tool_panel_section_label: "BEDTools"
  revisions:
  - 2892111d91f8

- name: column_maker
  owner: devteam
  tool_panel_section_label: "Text Manipulation"
  revisions:
  - aff5135563c6

- name: meme_fimo
  owner: iuc
  tool_panel_section_label: "MEME Suite"
  revisions:
  - 01f5d04846c4
EOF

# Install tools
shed-tools install -g <galaxy_url> -a <api_key> -t tool_list.yaml
```

## Genome Requirements

This workflow requires a reference genome to be available in your Galaxy instance. The workflow is configured to use CHM13_T2T_v2.0 as the default genome, but you can modify this to use any genome available in your Galaxy instance.

### Adding New Genomes

If the required genome is not available in your Galaxy instance:

1. Go to "Admin" → "Local Data" → "Create Genome"
2. Upload your FASTA file
3. Provide required details and save

## MEME Suite Requirements

The FIMO tool requires the MEME Suite to be properly installed. This includes licensing agreements for non-commercial use. When installing the MEME Suite tools:

1. Ensure you accept the non-commercial use license
2. Verify that all dependencies are correctly installed
3. Test the tools with sample data

## Troubleshooting Tool Installation

If you encounter issues during tool installation:

1. Check Galaxy logs for error messages
2. Verify that all dependencies are properly installed
3. Ensure your Galaxy instance has sufficient resources
4. Check that your tool shed connection is working
5. Consult the Galaxy community forums or documentation
