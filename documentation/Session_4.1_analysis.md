# Analysis of mOTUs Output in R

### R Studio

To work in R, we are going to use the R Studio interface:

![rstudio](/images/rstudio.png)

The panels are:

* top-left: script editor
* top-right: variable list
* bottom-left: console
* bottom-right: file browser / plots / package list / help

### First, set the correct working directory
```
setwd("S:/biolcourse-34")
```

### What is the effect of running mOTUs with different parameters?

#### Sort mOTUs from most to least abundant and remove those that never appear
```
data <- read.table("M04.5-V3-stool-metaG.merged.motus",sep="\t",stringsAsFactors = F,quote="\"",row.names=1,comment="",skip=2,header=T)
data.sorted <- data[order(rowSums(data),decreasing=T),]
data.filtered <- data.sorted[rowSums(data.sorted)>0,]
```

#### Plot the data from the three different sets of parameters
```
matplot(100*data.filtered,log="y",type="l",lty=1,ylim=c(1e-4,1e2),ylab="Relative Abundance (%)")
legend("topright",legend=c("Default","High Precision","High Sensitivity"),fill=1:3)
grid()
```

#### Compare the default and high sensitivity data sets
```
plot(100*data.filtered[,1]+1e-4,100*data.filtered[,2]+1e-4,log="xy",xlim=c(1e-4,1e2),ylim=c(1e-4,1e2),xlab="Default",ylab="High Sensitivity",pch=20,col=rgb(1,0,0,0.25))
grid()
abline(0,1)
```
___

### How does metagenomic data compare with metatranscriptomic data?

#### Import the data, remove rows with no abundance
```
all.data <- read.table("default.merge.motus",sep="\t",stringsAsFactors = F,quote="\"",row.names=1,comment="",skip=2,header=T)
valid.data <- all.data[rowSums(all.data)>0,]
```

#### Shortcuts for different sample types
```
metaG <- seq(1,ncol(valid.data),2)
metaT <- seq(2,ncol(valid.data),2)
```

#### Plot G against T
```
plot(1e-5+unlist(valid.data[,metaG]),1e-5+unlist(valid.data[,metaT]),log="xy",xlab="metaG",ylab="metaT",pch=20,col=rgb(1,0,0,0.1))
abline(0,1)
grid()
```
___

### Calculate a distance matrix between samples, perform ordination and hierarchically cluster

#### Load libraries
```
library(vegan)
library(dendextend)
```

#### Import sample metadata
```
metadata <- read.table("../data/motus_metadata.tsv",sep="\t",row.names=1,header=T)
```

#### Color samples by individual
```
palette(c('#e6194b', '#3cb44b', '#ffe119', '#4363d8', '#f58231', '#911eb4', '#46f0f0', '#f032e6', '#bcf60c', '#fabebe', '#008080', '#e6beff', '#9a6324', '#fffac8', '#800000', '#aaffc3', '#808000', '#ffd8b1', '#000075', '#808080', '#ffffff', '#000000'))
sample.individuals <- substr(colnames(valid.data),1,5)
sample.colors <- as.numeric(as.factor(sample.individuals))
```

#### Calculate distance matrix
```
dm <- vegdist(t(log(valid.data+1e-6)),method="euclidean")
```

#### Perform MDS
```
mds <- monoMDS(dm,pc=T,k=4)
```

### Will individuals cluster, will families?

#### Create ordination plot
```
plot(mds$points,pch=20,col=sample.colors)
legend("topleft",legend=unique(sample.individuals),fill=unique(sample.colors),cex=0.5)
```

#### Repeat, but consider family
```
sample.family <- metadata[sample.individuals,"FAMNO"]
plot(mds$points,pch=20,col=sample.family)
legend("topleft",legend=unique(sample.family),fill=unique(sample.family))
```

#### Repeat with the metadata of your choice
```
sample.diabetes <- metadata[sample.individuals,"DIABETESTY1"]
plot(mds$points,pch=20,col=sample.diabetes)
legend("topleft",legend=unique(sample.diabetes),fill=unique(sample.diabetes))
```

#### Hierarchically cluster samples
```
hc <- as.dendrogram(hclust(dm))
```
### Will samples cluster by individual, by diabetes status?

#### Plot with individual information
```
sample.colors
labels_colors(hc) <- sample.colors
par(mar=0.1+c(12,4,4,1))
plot(hc)
```

#### Plot diabetes status
```
diabetes.colors <- as.numeric(as.factor(metadata[sample.individuals,"DIABETESTY1"]))
labels_colors(hc) <- diabetes.colors
plot(hc)
```

#### Plot some metadata of your choice
```
meta.colors <- as.numeric(as.factor(metadata[sample.individuals,"SEX"]))
labels_colors(hc) <- meta.colors
plot(hc)
```
