# ![nf-core/viralrecon](docs/images/nf-core-viralrecon_logo_light.png#gh-light-mode-only) ![nf-core/viralrecon](docs/images/nf-core-viralrecon_logo_dark.png#gh-dark-mode-only)

[![GitHub Actions CI Status](https://github.com/nf-core/viralrecon/workflows/nf-core%20CI/badge.svg)](https://github.com/nf-core/viralrecon/actions?query=workflow%3A%22nf-core+CI%22)
[![GitHub Actions Linting Status](https://github.com/nf-core/viralrecon/workflows/nf-core%20linting/badge.svg)](https://github.com/nf-core/viralrecon/actions?query=workflow%3A%22nf-core+linting%22)
[![AWS CI](https://img.shields.io/badge/CI%20tests-full%20size-FF9900?logo=Amazon%20AWS)](https://nf-co.re/viralrecon/results)
[![Cite with Zenodo](http://img.shields.io/badge/DOI-10.5281/zenodo.3901628-1073c8)](https://doi.org/10.5281/zenodo.3901628)

[![Nextflow](https://img.shields.io/badge/nextflow%20DSL2-%E2%89%A521.10.3-23aa62.svg)](https://www.nextflow.io/)
[![run with conda](http://img.shields.io/badge/run%20with-conda-3EB049?logo=anaconda)](https://docs.conda.io/en/latest/)
[![run with docker](https://img.shields.io/badge/run%20with-docker-0db7ed?logo=docker)](https://www.docker.com/)
[![run with singularity](https://img.shields.io/badge/run%20with-singularity-1d355c.svg)](https://sylabs.io/docs/)
[![Launch on Nextflow Tower](https://img.shields.io/badge/Launch%20%F0%9F%9A%80-Nextflow%20Tower-%234256e7)](https://tower.nf/launch?pipeline=https://github.com/nf-core/viralrecon)

[![Get help on Slack](http://img.shields.io/badge/slack-nf--core%20%23viralrecon-4A154B?logo=slack)](https://nfcore.slack.com/channels/viralrecon)
[![Follow on Twitter](http://img.shields.io/badge/twitter-%40nf__core-1DA1F2?logo=twitter)](https://twitter.com/nf_core)
[![Watch on YouTube](http://img.shields.io/badge/youtube-nf--core-FF0000?logo=youtube)](https://www.youtube.com/c/nf-core)

## Introduction
This is the Greninger Lab fork of the **nf-core/viralrecon** pipeline. Visit the official [nf-core/viralrecon github](https://github.com/nf-core/viralrecon) and [nf-core/viralrecon project](https://nf-co.re/viralrecon) for more detailed instructions on how to use this pipeline.

## Added/Modified Features
- use `--trim_len` to specify the minimum read length for fastp to retain
- Mosdepth whole genome coverage graph log10 transformation disabled

## Usage
1. Install [`Nextflow`](https://www.nextflow.io/docs/latest/getstarted.html#installation) (`>=21.10.3`)

2. Install any of [`Docker`](https://docs.docker.com/engine/installation/)

3. Download the pipeline and test it on a minimal dataset with a single command:

   ```console
   nextflow run greninger-lab/viralrecon -latest -profile test,docker --outdir <OUTDIR>
   ```

4. Running your own analysis

	- A samplesheet needs to be created first in order to run viralrecon. You can automate samplesheet creation with a bundled python script. Download the repository locally and run:

	```console
	python <VIRALRECON_REPO_DIR/bin/fastq_dir_to_samplesheet.py> <FASTQ_DIR> viralrecon_samplesheet.csv
	```

	- Modify the `conf/base.config` to make sure computing resource allocation is appropriate for your usage

	- Example command for Illumina shotgun sequencing QC:

	```bash
	nextflow run <VIRALRECON_REPO_DIR/main.nf> \
		--input viralrecon_samplesheet.csv \
		--outdir <VIRALRECON_OUTDIR> \
		--platform illumina \
		--protocol metagenomic \
		--fasta <REFERENCE_FASTA_PATH> \
		--trim_len 120 \
		--skip_markduplicates false \
		--filter_duplicates true \
		--skip_nextclade \
		--skip_pangolin \
		--skip_assembly \
		--skip_asciigenome \
		--skip_consensus \
		-profile docker
	```

	- Example command for Illumina amplicon sequencing QC:
	
	```bash
	nextflow run <VIRALRECON_REPO_DIR/main.nf> \
		--input viralrecon_samplesheet.csv \
		--outdir <VIRALRECON_OUTDIR> \
		--platform illumina \
		--protocol amplicon \
		--fasta <REFERENCE_FASTA_PATH> \
		--primer_bed <AMPLICON_PRIMER_BED_FILE_PATH> \
		--trim_len 120 \
		--skip_nextclade \
		--skip_pangolin \
		--skip_assembly \
		--skip_asciigenome \
		--skip_consensus \
		-profile docker
	```
