## GATK4_Zymoseptoria
This is a snakemake workflow that uses GATK4 to call SNPs against Australian Reference Z. tritici WAI332 or European Reference IPO323.
You must set the config.yml to choose which reference you would like to align against. You can do this by changing the config.yml file. Simply delete the "#" from infront of the reference you would like to use.


To use this Snake make workflow you must have Anaconda with the Bioconda channel installed.

#### Step 1 Install Anaconda, dowload the appropriate version for your operating system (Windows/Mac/Linux) and follow the prompts
Get the free version of anaconda from here: [https://www.anaconda.com/products/individual]

##### Check if this has worked by typing into your terminal
`conda help`

#### Step 2 Set up the Bioconda channel by running these three commands in your Terminal
`conda config --add channels defaults`

`conda config --add channels bioconda`

`conda config --add channels conda-forge`

##### Check if this has worked by typing into your terminal
`conda install bwa`

#### Step 3 Create a conda environment where you will run your analyses and use conda to install "snakemake"
You must use conda to install Snakemake and snakemake-wrapper-utils before running this pipeline.
We recommend creating a separate conda environment for running this analysis, we will call this environment "SNPcalling"

`conda create --name SNPcalling snakemake snakemake-wrapper-utils mamba`

##### Check if this has worked by typing in your terminal

`conda activate SNPcalling`

##### Note: you need to "activate" SNPcalling everytime you open a new terminal and want to run this analysis

#### Step 4 If you have not done so alread download or clone this repository on your local computer
This will create a folder called "GATK4_Zymoseptoria" on your computer.
This folder contains five folders:
  1. 00_reads: which contains some small example data
  2. config: which contains a config.yml text file which you will need to change your sample names and reference isolate name
  3. workflow: This folder contains the Snakefile which runs the whole analysis
  4. WAI332_reference: The referece genome, bowtie and GATK indexes needed if aligning reads to the Australian WAI332 reference genome
  5. IPO323_reference: The reference genome, bowtie and GATK indexes needed if aligning reads to the European IPO323 reference genome

##### Check if this has worked by typing into your terminal 
`cd /PATH/TO/GATK4_Zymoseptoria`

`conda activate SNPcalling`

#### Step 5 Modify the config.yml by opening this file in a text editor to to choose your reference (notepad, bbedit, vscode, sublime, DO NOT OPEN IN MS WORD!) 
In the config.yml file you will see these lines:

\# Choose which reference you want to use by removing the "#" in front of WAI332 or IPO323. The pipeline will not tolerate both references un-commented. You must choose one and only one!

Reference:

\# - WAI332

\# - IPO323

You must delete the "#" from in front of either WAI332 or IPO323 (but NOT BOTH!). Save your changes and close the config.yml file.

#### Step 6 Run! To run the snakemake pipeline make sure that you are in the GATK4_Zymoseptoria folder.

`snakemake --use-conda --cores`

The default analysis with example datafiles UV1short and UV2short will run and create output folder for each section of the analysis.
The output files are as follows:
  1. 01_trimmed: A folder containing the quality trimmed paired and unpaired fastq.gz files output by Trimmomatic
  2. 02_mapped: A folder containing the unsorted, sorted bam files of your samples aligned to the reference genome
  3. 03_dedup: A folder containing the de-duplicated sorted bam files which are required as input for GATK
  4. 04_calls: A folder containing the intermediate g.vcf files for each individual sample and a combinded .g.vcf file for all isolates. The FINAL important VCF file is called all.vcf  
  5. 05_filtered: A folder containing the filtered all.vcf file after removing low-quality SNPs with VCFtools. The intermediate file all.flagged.vcf includes LOW quality SNPs. The FINAL file all.filtered.vcf contains only High quality SNPs.


#### Step 7 Run the pipeline with your own samples by adding their names to the config.yml file
Modify the config.yml by opening this file in a text editor (notepad, bbedit, vscode, sublime, DO NOT OPEN IN MS WORD!) 
In the config.yml file you will see these lines:

\## List of paired end sample names

Samples:

\- UV1short

\- UV2short

##### You can add your own fastq.gz files to the 00_reads folder. NOTE, these files must be named as follows:

SampleX.1.fastq.gz  (forward reads)

SampleX.2.fastq.gz  (reverse reads)

##### Remove the example sample names and put your own samples in:

Samples:

 \- SampleX
 
 \- SampleY
 
 \- SampleZ
 
 ##### Save the config.yml file with your sample names and remove/delete all previous output folders.
 
 #### Step 8 Run the analysis with your own samples!
 
 `conda activate SNPcalling`
 
 `snakemake --use-conda --cores`
