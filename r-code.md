# R Code

Credit to Alex Chui, Alex Papachristodoulou, Devin Golla, and others

### [back to home](index.md)

In R Studio, start a new R script.  It may be helpful to change the Renviron file directly, in case the program has difficulty accessing the packages you have downloaded:
```
write('PATH="${RTOOLS40_HOME}\\usr\\bin;${PATH}"', file = "~/.Renviron", append = TRUE)
```

First, you will have to load in your gene counts file (more information on how to format that [here](file_formats.md).  Keep in mind that the file path may differ slightly for Mac (this code was written on a PC):
```
mouse_counts <- file.path("C:", "Users", "Devin", "Desktop", "mouse_counts.csv", fsep="/")
file.exists(mouse_counts) # Helpful for debugging to check if you are in the right location
cts <- as.matrix(read.csv(mouse_counts,sep=",",row.names=1)) # Convert to matrix
cts # This just prints the matrix
```

Then, you will have to load in your annotations file (more information on how to format that [here](file_formats.md).
```
mouse_anno <- file.path("C:", "Users", "steel", "Desktop", "mouse_anno.txt", fsep="/")
coldata <- read.csv(mouse_anno, sep="\t") # Read as CSV file
coldata$nkx <- factor(coldata$nkx) # Converts to factor data type, for comparison
```

To download a library in R using Bioconductor, use the following code.  You do not have to do this every time you call the library, only when you are first downloading it:
```
BiocManager::install("DESeq2") # or whatever the name of your library is
```

Now, we will call a library that we have downloaded, DESeq2, and create a new data type that will allow our data to be processed, a DESeqDataSet.
```
library("DESeq2")
dds <- DESeqDataSetFromMatrix(countData = cts,
                              colData = coldata,
                              design = ~ nkx)
dds
```

A variance stabilizing transform will then be performed on the data.
```
vsd <- vst(dds) 
class(vsd) # Check type - object should be of type DESeqTransform
```

In order to view the data in clusters, a PCA plot can be generated.  More info on PCA plots can be found [here].
```
data <- plotPCA(vsd, intgroup="nkx", returnData = TRUE)
data
percentVar <- round(100 * attr(data, "percentVar"))
library("ggplot2")
ggplot(data, aes(PC1, PC2, color=nkx)) + geom_point(size=3) +
  xlab(paste0("PC1: ",percentVar[1],"% variance")) +
  ylab(paste0("PC2: ",percentVar[2],"% variance"))
```

DESeq analysis can then be performed.  However, in order to limit our output to data that is statistically significant, we can lower the false discovery rate threshold of the analysis pipeline to p = 0.05, and we can raise the log fold change threshold so that only genes with more substantial changes will be recognized by the analysis.  These can be changed with whatever cutoff is necessary for data analysis.
```
# lower false discovery rate threshold
res.05 <- results(dds, alpha=.05)
table(res.05$padj < .05)

#raise log2 fold change threshold (genes w/ more substantial changes)
resLFC1 <- results(dds, lfcThreshold=1)
table(resLFC1$padj < 1)

dds <- DESeq(dds)
```

A program called "lfcShrink" can also be called to account for the shrunken log fold changes present in the data.  After this, the output can be visualized.
```
res <- results(dds, alpha = 0.05)
mcols(res, use.names=TRUE)
resLFC <- lfcShrink(dds, coef="nkx_yes_vs_no", type="apeglm")
summary(res)
```

A plot of individual gene counts by annotation designation (ex. "nkx" vs. "no-nkx") can be visualized using plotCounts, and the name of the gene in question:
```
plotCounts(dds, "ENSMUSG00000022061", "nkx")
```

An MA plot, which shows the genome and the genes that are expressed differentially within the statistical significance threshold, can also be generated:
```
DESeq2::plotMA(res, ylim=c(-10,10))
```

Once "interesting" genes have been identified, these genes can be selectively plotted into a heat map, where their differences in expression can be visualized:
```
interesting <- c("ENSMUSG00000015619", "ENSMUSG00000068457")
library("pheatmap")
mat <- assay(vsd)[interesting,]
mat <- mat - rowMeans(mat)
df <- as.data.frame(colData(vsd))
pheatmap(mat, cluster_rows=FALSE, cluster_cols=TRUE, show_rownames=TRUE, annotation_col=df)
```

If you are viewing an RNA Seq data set for the first time and are simply looking for genes that are differentially expressed, the pheatmap can be generated as follows:
```
library("pheatmap")
mat <- assay(vsd)[ head(order(res$padj),200), ]
mat <- mat - rowMeans(mat)
df <- as.data.frame(colData(vsd)[,c("SampleName","nkx")])
pheatmap(mat, show_rownames=FALSE, annotation_col=df)
```

After the analysis has been performed, the normalized counts can be saved to a file for further analysis in GSEA (after some file manipulation has taken place):
```
norm_counts <- counts(dds, normalized = T)
norm_counts <- as.data.frame(norm_counts)
gct_path <- file.path("C:", "Users", "Devin", "Desktop", "norm.gct", fsep="/")
write.table(norm_counts, gct_path, sep = "\t", quote = F, row.names = F)
```

Otherwise, if you would like to save your results to a file including the gene names:
```
library("AnnotationDbi")
library(Homo.sapiens)
columns(Homo.sapiens)

library("edgeR")
genetable <- data.frame(gene.id=rownames(se))
y <- DGEList(counts=countdata, 
             samples=coldata, 
             genes=genetable)
names(y)

# provide row names of results table as key
res$symbol <- mapIds(Homo.sapiens,
                     keys=row.names(res),
                     column="SYMBOL",
                     keytype="ENSEMBL",
                     multiVals="first")

y$genes$symbol <- res$symbol

res$entrez <- mapIds(Homo.sapiens,
                     keys=row.names(res),
                     column="ENTREZID",
                     keytype="ENSEMBL",
                     multiVals="first")

y$genes$entrez <- res$entrez

res$symbol <- mapIds(Homo.sapiens,
                     keys=row.names(res),
                     column="GENENAME",
                     keytype="ENSEMBL",
                     multiVals="first")

y$genes$symbol <- res$symbol
resOrdered <- res[order(res$padj),]
head(resOrdered)

# save results to a csv file
resOrderedDF <- as.data.frame(resOrdered)[seq_len(100),]
write.csv(resOrderedDF, file="results_all.csv")
```
