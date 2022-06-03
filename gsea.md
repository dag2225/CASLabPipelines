# GSEA Information
### [back to home](index.md)

### What is GSEA?

GSEA desktop app can be downloaded here: [http://www.gsea-msigdb.org/gsea/login.jsp](http://www.gsea-msigdb.org/gsea/login.jsp)

## Step 1 - Load data
(Note - for more formatting questions, see [File Formats](file_formats.md) page, or additionally, this link [here](https://software.broadinstitute.org/cancer/software/gsea/wiki/index.php/Data_formats#:~:text=file%20format%20(*.-,cls),tabs%20to%20separate%20the%20fields.&text=The%20first%20line%20contains%20the%20text%20%22%23numeric%22%20which%20indicates,the%20file%20defines%20continuous%20labels.): 

Dataset will be in file format .gct - this is a version of the output from DESeq2.  Additional columns and labels may need to be added as this file is processed - this can be done in Excel, by splitting text into columns.
```
#1.2
38160 10
NAME Description sam1 sam2 sam3 sam4 sam5 sam6 sam7 sam8 sam9 sam10
gene1             1 0 0 0 0 23 24 35 65 24
...
```
Note that here, 38160 is the number of rows (genes) in the file, and 10 is the number of classes, which are each listed as their own columns.
Also note that if a geneset file ending in ".symbols.gmt" is used for this analysis, and the DESeq2 output lists genes by their numeric gene ID, a conversion needs to take place before analysis can occur - a list of gene names from gene IDs can be obtained using the Ensembl Biomart tool, [here](https://www.ensembl.org/biomart/martview/f72f154b2e4ce299357c02ca7f720a5a).  

Biomart instructions:
- Click "New" in the top left corner, then select the correct organism
- Input your list of gene ID's in the text box under "Filters" tab, then "GENE" heading.  Also, check this checkbox.
- Under "Attributes" tab, "GENE" heading, ensure that "Gene stable ID" and "Gene name" are checked.
- Click "Results" in the top left corner.
Also note that if any repeat gene names exist in the file, the program will give an error.

Phenotype labels will be in the file format .cls; and will look like
```
10 2 1
# no_nkx nkx
no_nkx no_nkx no_nkx no_nkx no_nkx nkx nkx nkx nkx nkx
```
where "10" here refers to the number of samples analyzed in the normalized counts, "2" refers to the number of classes (which are listed on the comment line; in this case they are "no_nkx" and "nkx"), and "1" is always there.  

Gene sets will be in the file format .gmt, and can be downloaded from [this link](https://data.broadinstitute.org/gsea-msigdb/msigdb/release/7.1/) on the Broad Institute website.

## Step 2 - Run GSEA

### "Expression dataset"
Select the correctly formatted .gct file from your loaded data.

### "Gene sets database"
Select geneset file that was downloaded from file, or select geneset file from those provided.

### "Number of Permutations"
This can be left at the default value of 1000, unless otherwise directed.

### "Phenotype labels"
Select .cls file from your loaded data.

### "Collapse/Remap to gene symbols"
Choose "No_Collapse" option, which is the only option that will work without specifying a chip platform.  These settings work because of the data that will be fed into the program, which comes from counts files that already have much of the raw data processed.

### "Permutation type"
Leave the default option, "phenotype".

### "Chip platform"
This can be left alone, unless otherwise directed.
