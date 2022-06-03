# GSEA Information
### [back to home](index.md)

### What is GSEA?

GSEA desktop app can be downloaded here: [http://www.gsea-msigdb.org/gsea/login.jsp](http://www.gsea-msigdb.org/gsea/login.jsp)

## Step 1 - Load data
(Note - for more formatting questions, see [File Formats](file_formats.md) page.

Dataset will be in file format .gct - this is a version of the output from DESeq2.

Phenotype labels will be in the file format .cls;

Gene sets will be in the file format .gmt, and can be downloaded from [this link](https://data.broadinstitute.org/gsea-msigdb/msigdb/release/7.1/) on the Broad Institute website.

## Step 2 - Run GSEA

### "Expression dataset"

### "Gene sets database"

### "Number of Permutations"
This can be left at the default value of 1000, unless otherwise directed.

### "Phenotype labels"

### "Collapse/Remap to gene symbols"
Choose "No_Collapse" option, which is the only option that will work without specifying a chip platform.  These settings work because of the data that will be fed into the program, which comes from counts files that already have much of the raw data processed.

### "Permutation type"

### "Chip platform"
This can be left alone, unless otherwise directed.
