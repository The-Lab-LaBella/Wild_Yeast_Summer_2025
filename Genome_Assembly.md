# Genome Assembly

This tutorial will walk you through how to assemble the Nanopore genomes sequenced by Plasmidsaurus 

If you want to learn more about how Nanopore sequencing works there are lots of informative videos here: https://nanoporetech.com/platform/technology 

This tutorial will only cover the bioinformatics parts of the analysis. We will discuss the background information in person. 

Along the way you will report results in this spreadsheet: https://docs.google.com/spreadsheets/d/17ScIAdl7iKe4SDxmFpJEvZmdBlQJUDD8eWTuUf0sbvA/edit?usp=sharing 

&nbsp;
&nbsp;

## Step 1 - Set up your folder

&nbsp;

### Step 1a - create a new folder to work in 

In either your home or scratch directory create a new folder with your genomeID. I will use ABB_052825_01_A as an example throughout 

```mkdir ABB_052825_01_A```

Then move into that directory using `cd`

&nbsp;

### Step 1b - copy the fastq files into your directory 

If you have access to the `labella_lab` directory you can copy them from there.

If you do not, let Dr. LaBella know and she will get you the files. 

```
cp /projects/labella_lab/wild_yeast/summer_25_results/RKTLP_1_AB-01.fastq.gz .
```

&nbsp;

## Step 2 - Filter the sequencing reads

Not all sequencing reads will be of the same quality. We want to trim or remove sequences that are low quality. To do this we will use https://github.com/OpenGene/fastplong 

&nbsp;

### Step 2a - Install fastplong 

We need to install and activate fastplong before running it. 

```
#activate anaconda
module load anaconda3

#create a new conda environment named fastplong
conda create --name fastplong

#activate the conda environment - after doing this you should see (fastplong) before your username in the command line
conda activate fastplong

#install fastplong in your environment
conda install -c bioconda fastplong

#when it asks you if you want to proceed type y and hit enter
```

&nbsp;

### Step 2b - Filter your sequencing reads

To filter the reads use this command

```
fastplong -i RKTL8P_10_ABB-01.fastq.gz -o RKTL8P_10_ABB-01.filtered.fastq.gz
```

Once this is done, you will have a new file and a report on the filtering saved to `fastplong.html`

Download the html file and take a look at it. Report on the spreadsheet your
- Perecent of Reads passed Filters
- Total Reads
- Median Lenght (in Kilo bases (K))

&nbsp;

### Step 2c - Deactivate your environment

We don't need to use fastplong anymore so deactivate the environment using the command

```
conda deactivate fastplong
```

&nbsp;
&nbsp;

## Step 3 - Assemble reads into the genome

We will use the assembler flye to assemble the nanopore genome https://github.com/mikolmogorov/Flye 

&nbsp;

### Step 3a - Load Flye on the cluster

Flye is available on the HPC so we will load it first

```
module load flye
```

&nbsp;

### Step 3b - Uncompress the fastq files

Flye expects uncompressed files so you will need to uncompress the gz file generated above

```
gunzip RKTL8P_10_ABB-01.fastq.filtered.gz
```

&nbsp;

### Step 3c - Run Flye using the high quality nanopore settings

The genome assembly will take more resources than we should use on the head node of the cluster.

Therefore we are going to submit a slurm job to the cluster. This should take less than an hour to complete

You will copy the slurm file `flye_assembly.slurm` from the project space. 

```
cp /projects/labella_lab/wild_yeast/flye_assembly.slurm
```

You will then need to change the name of the sequence in the file. You can see the text of the file below. 

```
#!/bin/bash
#SBATCH --job-name=flye_assembly
#SBATCH --output=flye_assembly_%j.out
#SBATCH --error=flye_assembly_%j.err
#SBATCH --partition=Orion
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=16
#SBATCH --mem=64G
#SBATCH --time=2:00:00

module load flye

# Replace the following with your Flye command and input files
flye --nano-hq RKTL8P_10_ABB-01.filtered.fastq -o RKTL8P_10_ABB-01/ --threads 16


```

&nbsp;

### Step 3d - Refine assembly with Medaka

We will further refine our assembly using Medaka: https://github.com/nanoporetech/medaka

Again we will run this using a slurm script - this should take less than 30 minutes

```
#!/bin/bash
#SBATCH --job-name=medaka_assembly
#SBATCH --output=medaka_assembly_%j.out
#SBATCH --error=medaka_assembly_%j.err
#SBATCH --partition=Orion
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=16
#SBATCH --mem=32G
#SBATCH --time=4:00:00

module load artic

# Replace the following with your medaka command and input files
medaka_consensus -i RKTL8P_10_ABB-01.filtered.fastq -d RKTL8P_10_ABB-01/assembly.fasta -o RKTL8P_10_ABB-01 -t 16

```

&nbsp;

## Step 4 - Analyze your final genome

Your final genome is now held in your new folder under the name `consensus.fasta`

### Step 4a - Copy your genome

We want to rename the genome to it's proper name

```cp RKTL8P_10_ABB-01/consensus.fasta ABB_052825_01_A.fasta```

### Step 4b - Analyze your genome quality 

```
#remove any active modules
module purge

#load QUAST
module load quast
```



# Set up Funannotate

```
module load anaconda
conda create -n funannotate "python>=3.6,<3.9" funannotate
conda activate funannotate
conda install chardet
export FUNANNOTATE_DB=/projects/labella_lab/funannotate_db
```

