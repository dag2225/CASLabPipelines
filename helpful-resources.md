## Welcome to CAS Lab Pipelines!

# Helpful External Resources
### [back to home](index.md)

## Helpful resources for DESeq2 Pipeline
- Bioconductor: includes a bunch of helpful [vignettes](https://www.bioconductor.org/help/package-vignettes/) that explain how to use different libraries hosted on their site.
- A quick start guide for using the DESeq2 package can be found on the [Bioconductor website here](http://bioconductor.org/packages/devel/bioc/vignettes/DESeq2/inst/doc/DESeq2.html#quick-start).  A more step-by-step walkthrough of DESeq2 can be found in the Bioconductor site's course materials [here](https://www.bioconductor.org/help/course-materials/2016/CSAMA/lab-3-rnaseq/rnaseq_gene_CSAMA2016.html) (which was incredibly helpful to me).  This is slightly different than the R code used for this analysis, since it generates the counts from BAM files (which, if you are interested, are discussed [here](https://www.ncbi.nlm.nih.gov/tools/gbench/tutorial6/#:~:text=BAM%20files%20can%20be%20opened,to%20the%20BAM%20file%20name); if no BAM files are present, they can be generated from FASTQ files.
- An undergraduate student in the CAS Lab, Alex Chui, also has a site with important information on how DESeq2 can be used: [Alex's Github Site](https://alexchui252.github.io/BioinformaticsWorkflows/RNA-seq/deseq2.html)
- If you run into issues with R, the R project maintains a site that includes a [code "cheat sheet"](https://cran.r-project.org/doc/contrib/Short-refcard.pdf) for reference.
- Here is [another site explaining DESeq2](https://hbctraining.github.io/DGE_workshop/lessons/05_DGE_DESeq2_analysis2.html), maintained by a bioinformatics group at Harvard.
- Additional description and background for RNA Seq can be found here, in [a lecture from Rockefeller University/Weill Cornell Medical Center](https://physiology.med.cornell.edu/faculty/mason/lab/clinicalgenomics/lectures/2015/Lecture20_Sboner.pdf).
- Some more [background to the lfcShrink function](https://support.bioconductor.org/p/95695/) used in the pipeline.
- Some more information about how to output data from your DESeq2 R code ready to be run in GSEA: [here](https://www.biostars.org/p/9475520/)

## Helpful resources for GSEA
- Gene names can be extracted from gene ID's using Ensembl's [Biomart](https://useast.ensembl.org/info/data/biomart/index.html) tool.
- Information about count normalization from GSEA can be found [here](https://software.broadinstitute.org/cancer/software/gsea/wiki/index.php/Using_RNA-seq_Datasets_with_GSEA), on the Broad Institute GSEA website.
- Information on how to use GSEA gene sets: [here](https://www.gsea-msigdb.org/gsea/doc/GSEAUserGuideTEXT.htm#Gene_Sets)
- ### File formats for GSEA: [here](https://software.broadinstitute.org/cancer/software/gsea/wiki/index.php/Data_formats)
- Information on [what to do with the "chip platforms" option](https://software.broadinstitute.org/cancer/software/gsea/wiki/index.php/1002)
- In case additional help or debugging is necessary, a GSEA help group can be found here: [GSEA Google Group](https://groups.google.com/g/gsea-help)
