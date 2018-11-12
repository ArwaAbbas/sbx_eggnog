# Sunbeam Eggnog Mapper extension 

This is a template to use to extend the [Sunbeam pipeline](https://github.com/sunbeam-labs/sunbeam) with the [Eggnog Mapper](https://anaconda.org/bioconda/eggnog-mapper), a tool for functional annotation of large sets of sequences based on fast orthology assignments using precomputed eggNOG clusters and phylogenies. There are three major parts to a Sunbeam extension: 

 - `requirements.txt` specifies the extension's dependencies
 - `config.yml` contains configuration options that can be specified by the user when running an extension
 - `sbx_template.rules` contains the rules (logic/commands run) of the extension
 
## Creating an extension

The dependencies required for this extension are listed in the `requirements.txt` file in the [standard requirement format](https://pip.readthedocs.io/en/1.1/requirements.html). 

The `config.yml` contains parameters that the user might need to modify when running an extension. Default values should be specified for each bottom-level key.

Finally, `sbx_template.rules` contains the actual logic for the extension, including required input and output files. A detailed discussion of Snakemake rule creation is beyond the scope of this tutorial, but definitely check out [the Snakemake tutorial](http://snakemake.readthedocs.io/en/stable/tutorial/basics.html) and any of the [extensions by sunbeam-labs](https://github.com/sunbeam-labs) for inspiration.

## Installing an extension

Installing an extension is as simple as cloning (or moving) your extension directory into the sunbeam/extensions/ folder, installing requirements through Conda, and adding the new options to your existing configuration file: 
This extension has dependencies that conflict with those of  [sbx_rgi](https://github.com/louiejtaylor/sbx_rgi) so may need to create a separate conda environment (within the sunbeam environment) to run it.

    source activate sunbeam
    conda create -n eggnog
    source activate eggnog
    git clone https://github.com/ArwaAbbas/sbx_eggnog/ sunbeam/extensions/sbx_eggnog
    conda install --file requirements.txt -c bioconda
    cat sunbeam/extensions/sbx_eggnog/config.yml >> sunbeam_config.yml

## Running an extension

To run an extension, simply run Sunbeam as usual with your extension's target rule specified:

    sunbeam run --configfile=sunbeam_config.yml example_rule
    
# sbx_eggnog 
