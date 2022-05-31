# File Formats

### [back to home](index.md)

## Formatting Gene Counts File
(Most manipulation can be done in Excel, by saving as a CSV file.)
Gene counts will be formatted in comma separated columns, as below.
```
Geneid,PP15,PP16,PP17,PP18,PP19,PP20,PP21,PP22,PP23,PP24,PP25,PP26
ENSMUSG00000102693,0,0,0,0,0,0,0,0,0,0,0,0
ENSMUSG00000064842,0,0,0,0,0,0,0,0,0,0,0,0
ENSMUSG00000051951,0,0,0,1,0,0,1,1,0,1,0,0
ENSMUSG00000102851,0,2,0,0,0,0,0,0,0,0,0,0
```

## Formatting Gene Annotations File
Gene annotations will be formatted in tab separated columns, as below. "nkx" is used throughout the code as the name of the variable used to store the difference between data sets (whether or not a particular gene count is from a sample where nkx is expected to be upregulated or not).
```
file	nkx
PP15	yes
PP16	yes
PP19	no
PP20	no
...
```
