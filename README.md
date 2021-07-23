## GATK4_Zymoseptoria
This is a snakemake workflow that uses GATK4 to call SNPs against Australian Reference Z. tritici WAI332 or European Reference IPO323.
You must set the config.yml to choose which reference you would like to align against


To use this Snake make workflow you must have Anaconda with Bioconda channels set up.

You must use conda to install Snakemake and snakemake-wrapper-utils before running.
We recommend creating a separate conda environment for running this analysis.

`conda-env create -n SNPcalling snakemake snakemake-wrapper-utils`

`conda activate SNPcalling`

`cd /PATH/TO/GATK4_Zymoseptoria`

To run the analysis your terminal must be in the GATK4_Zymoseptoria folder.

`snakemake --use-conda --cores`
