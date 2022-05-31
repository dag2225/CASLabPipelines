# R Code

In R Studio, start a new R script.  It may be helpful to change the Renviron file directly, in case the program has difficulty accessing the packages you have downloaded:
```
write('PATH="${RTOOLS40_HOME}\\usr\\bin;${PATH}"', file = "~/.Renviron", append = TRUE)
```

First, you will have to load in your gene counts file (more information on how to format that [here]).  Keep in mind that the file path may differ slightly for Mac (this code was written on a PC):
```
mouse_counts <- file.path("C:", "Users", "Devin", "Desktop", "caslab_stuff", "tissue_recombs", "mouse_counts.csv", fsep="/")
file.exists(mouse_counts) # Helpful for debugging to check to see if you are in the right location
cts <- as.matrix(read.csv(mouse_counts,sep=",",row.names=1)) # Convert to matrix
cts # This just prints the matrix
```
