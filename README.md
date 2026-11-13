# Reproducible ATAC-seq & Transcription Factor Footprinting Pipeline

End-to-end **Snakemake** workflow for bulk ATAC-seq quality control, alignment, open-chromatin peak calling, differential accessibility, and genome-wide transcription factor (TF) footprinting (`TOBIAS`). Designed for seamless execution on local workstations (Conda) or HPC clusters (`Slurm` + `Singularity/Apptainer`).

> **Scientific Context:** Architecture adapted from regulatory element footprinting and postmitotic chromatin accessibility analyses published in *PNAS* (2025) and *eLife* (2022) using publicly available GEO datasets.

---

### Pipeline Architecture

```text
Raw FASTQs ─► FastQC ─► BWA-MEM ─► SAMtools (Filter/Dedup) ─► MACS3 (Peaks)
                                          │                        │
                                          ▼                        ▼
                                   TOBIAS ATACorrect ◄─────────────┘
                                          │
                                          ▼
                                   TOBIAS ScoreBigwig ─► TOBIAS BINDetect (TF Footprints)
                                          │
                                          ▼
                                   MultiQC Summary Report (HTML)
