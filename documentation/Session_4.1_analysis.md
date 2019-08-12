# Analysis of mOTUs Output in R

### R Studio

To work in R, we are going to use the R Studio interface:

![rstudio](/images/rstudio.png)

The panels are:

* top-left: script editor
* top-right: variable list
* bottom-left: console
* bottom-right: file browser / plots / package list / help

### Comparing the data from running mOTUs with different parameters
#### Sort mOTUs from most to least abundant and remove those that never appear
```R
data <- read.table("combined.motu",sep="\t",stringsAsFactors = F,quote="\"",row.names=1,comment="",skip=2,header=T)
data.sorted <- data[order(rowSums(data),decreasing=T),]
data.filtered <- data.sorted[rowSums(data.sorted)>0,]
```
#### Plot the data from the three different sets of parameters
```R
matplot(100\*data.filtered,log="y",type="l",lty=1,ylim=c(1e-2,1e6),ylab="Relative Abundance (%)")
legend("topright",legend=c("Default","High Precision","High Sensitivity"),fill=1:3)
```
#### Compare the default and high sensitivity data sets
```R
plot(100*data.filtered[,1]+1e-2,100*data.filtered[,3]+1e-2,log="xy",xlim=c(1e-2,1e6),ylim=c(1e-2,1e6),xlab="Default",ylab="High Sensitivity",pch=20,col=rgb(1,0,0,0.25))
abline(0,1)
```
___

### Comparing the metagenomic with the metatranscriptomic data

#### Import the data, remove rows with no abundance and keep samples with matching G/T data
```R
all.data <- read.table("all.motu",sep="\t",stringsAsFactors = F,quote="\"",row.names=1,comment="",skip=2,header=T)
sample.names <- substr(colnames(all.data),1,8)
valid.names <- names(which(table(sample.names)==2))
valid.samples <- which(sample.names%in%valid.names)

valid.data <- data.filtered[,valid.samples]
valid.data <- valid.data[rowSums(valid.data)>0,]
```
#### Shortcuts for different sample types
```R
metaG <- seq(1,ncol(valid.data),2)
metaT <- seq(2,ncol(valid.data),2)
```
### Plot G against T
```R
plot(1e-5+unlist(valid.data[,metaG]),1e-5+unlist(valid.data[,metaT]),log="xy",xlab="metaG",ylab="metaT",pch=20,col=rgb(1,0,0,0.1))
abline(0,1)
```
___

### Clustering the data

#### Calculate a distance matrix between samples and hierarchically cluster
```R
library(vegan)
library(dendextend)
dm <- vegdist(t(valid.data))
hc <- as.dendrogram(hclust(dm,method="ward.D"))
```
#### Plot with individual information
```R
palette(c('#e6194b', '#3cb44b', '#ffe119', '#4363d8', '#f58231', '#911eb4', '#46f0f0', '#f032e6', '#bcf60c', '#fabebe', '#008080', '#e6beff', '#9a6324', '#fffac8', '#800000', '#aaffc3', '#808000', '#ffd8b1', '#000075', '#808080', '#ffffff', '#000000'))
sample.colors <- as.numeric(as.factor(substr(labels(hc),3,5)))
labels_colors(hc) <- sample.colors
par(mar=0.1+c(10,4,4,1))
plot(hc)
```
#### Import sample metadata
```R
metadata <- read.table("motus_metadata.tsv",sep="\t",row.names=1,header=T)
individual.names = substr(labels(hc),1,5)
```
#### Plot diabetes status
```R
diabetes.colors <- as.numeric(as.factor(metadata[individual.names,"DIABETESTY1"]))
labels_colors(hc) <- diabetes.colors
plot(hc)
```
#### Plot some metadata of your choice
```R
meta.colors <- as.numeric(as.factor(metadata[individual.names,"SMOKING"]))
labels_colors(hc) <- meta.colors
plot(hc)
```
