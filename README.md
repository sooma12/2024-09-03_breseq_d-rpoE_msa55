# 2024-09-03_breseq_d-rpoE_msa55
MWS created 2024-09-03

Analysis of WGS data from Seqcenter


## Methods from SeqCenter:
Illumina Sequencing Methods
Illumina sequencing libraries were prepared using the tagmentation-based and PCR-based
Illumina DNA Prep kit and custom IDT 10bp unique dual indices (UDI) with a target insert size of
280 bp. No additional DNA fragmentation or size selection steps were performed. Illumina
sequencing was performed on an Illumina NovaSeq X Plus sequencer in one or more multiplexed
shared-flow-cell runs, producing 2x151bp paired-end reads. Demultiplexing, quality control and
adapter trimming was performed with bcl-convert1 (v4.2.4). Sequencing statistics are included in
the ‘DNA Sequencing Stats.xlsx’ file.

Breseq setup if needed:
```bash
srun --partition=express --nodes=1 --cpus-per-task=2 --pty --time=00:60:00 /bin/bash
module load anaconda3/2021.05
conda create --prefix /work/geisingerlab/conda_env/breseq_env python=3.9
# Deal with CommandNotFoundError: Your shell has not been properly configured to use 'conda activate'.
conda init bash
source ~/.bashrc

conda activate /work/geisingerlab/conda_env/breseq_env

# Biopython tweaks
# Make .condarc file, then tell conda to check bioconda.
conda config 
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
conda config --set channel_priority strict

conda install -p /work/geisingerlab/conda_env/breseq_env breseq
```

## Get data
Downloaded data via Box to shared desktop (downloads "Illumina DNA Reads.zip")

Copy data to Discovery with `scp`

Request compute node before proceeding!

Unzip using `unzip <zipfile>`

`cd` to the fastq directory
Generated list of md5sums with `md5sum * > gz_md5sums.txt`
Ran `0_check_md5sums.py` to verify integrity.

Edit "config.cfg" file to ensure that file paths and any names are correct.

`mkdir ./logs` for slurm log files

Note, all files from Seqcenter were formatted like "MSA223_1_...", with an underscore separating the strain name and the clone number.
This borked part of the breseq code.  Dealt with this using `for file in ./*; do mv -v -- "$file" "${file/_/-}"; done` to change the first _ in each file to a -.
I then renamed the YDA94 and YDA99 samples to revert this change, as those were single clones.

## Fastqc

## Sample sheet preparation


## Breseq array


## Clean up and zip results


## Analysis

