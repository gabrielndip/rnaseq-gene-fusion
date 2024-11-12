### RNAseq Analysis Pipeline
This repository contains **`rna-seq-script-transcript-fusion-detection.txt`**, a comprehensive, high-throughput RNA sequencing (RNAseq) analysis pipeline designed for processing large-scale RNAseq data, from raw reads to normalized gene expression outputs. The pipeline is specifically configured to handle paired-end data from Illumina sequencers and includes steps for quality control, alignment, quantification, and normalization. This robust pipeline leverages SLURM for job scheduling and parallel processing, enabling efficient, scalable RNAseq analysis.

#### Key Features
- BCL to FASTQ Conversion: Converts Illumina .bcl files to .fastq.gz format using bcl2fastq with automatic demultiplexing based on SampleSheet information.
- Quality Control (QC): Integrates FastQC for read quality assessment and Qualimap for RNAseq-specific QC, ensuring data quality before analysis.
- Alignment: Utilizes STAR for aligning reads to the human genome (hg19), with parameters optimized for detecting splicing events.
- Read Counting: Counts reads at the gene level using featureCounts, focusing on exon-level quantification for RNAseq applications.
- Consolidated QC Reporting: Generates a MultiQC report for a unified view of quality metrics across all samples, providing insights into data integrity and consistency.
- Transcript Quantification with Cuffquant: Uses cuffquant for transcript-level quantification, generating CXB files for normalized expression.
- Normalization with Cuffnorm: Performs final normalization across samples with cuffnorm, allowing for comparative gene expression analysis.

#### Pipeline Workflow
1.	Data Preparation:
      - Convert .bcl files to .fastq.gz format.
      - Organize files by sample and ensure all data is in the correct directories for further processing.
2.	Quality Control:
    - Run FastQC and Qualimap to assess read quality and RNAseq-specific metrics.
    - Consolidate quality metrics with MultiQC.
3.	Alignment:
    - Align reads to the reference genome using STAR, with parameters set to optimize splicing junction detection and chimeric read handling.
4.	Gene Expression Quantification:
    - Count reads overlapping annotated exons with featureCounts.
    - Use cuffquant for transcript-level quantification, storing output for downstream normalization.
5.	Normalization and Output:
    - Normalize gene expression across samples using cuffnorm.
    - Format sample sheets and add headers for easy interpretation and compatibility with downstream tools.

#### Requirements
- SLURM for job scheduling
- Modules:
- bcl2fastq, FastQC, Qualimap, STAR, featureCounts, MultiQC, Cufflinks (with cuffquant and cuffnorm)

#### Getting Started
This pipeline is tailored for a cluster environment and requires access to SLURM and the listed bioinformatics modules. Adjustments may be needed if using other cluster management systems or alternative reference genomes.
1.	Configure Parameters: Adjust paths and parameters in the script for specific environment and data structure.
2.	Prepare Sample Sheets: Ensure `SampleSheet.csv` is correctly formatted for bcl2fastq and cuffnorm steps.
3.	Run the Pipeline: Submit each section or the full script to the SLURM scheduler.

#### License
This project is licensed under the MIT License. See the LICENSE file for details.
