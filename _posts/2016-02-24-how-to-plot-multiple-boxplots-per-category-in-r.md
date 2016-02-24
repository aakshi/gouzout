---
title: "How to plot multiple boxplots per category in R"
layout: post
---

Boxplots are a great way to explore data and when doing modelling I often want to see how all the variables interact with a single target variable.

This is the code I use to publish all the Boxplots to a PDF for perusual. 

{% marginfigure 'mf-id-1' 'assets/posts/how-to-plot-multiple-boxplots-per-category-in-r/boxplot.svg' 'Basic Boxplot.' %}

```r

# Plot all the boxplots :)
## Can only plot numeric data 
## Get the name of each numeric column
names <- colnames(data[sapply(data, is.numeric)])
## Save boxplots to PDF
pdf("boxplots.pdf")

## For each column in names create a boxplot
for (i in names){
  ## Create formula for boxplot
  ## Target is typically a category / factor variable
  f <- as.formula(paste(i, "Target", sep="~"))
  print(i)
  boxplot(f,data=data,ylab = i, xlab ='Target')
}
dev.off()
```

