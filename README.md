# ggsegLausanne
ggseg atlases for Lausanne scales used at FTDC
This Rda file can be cloned/downloaded and loaded into an R session to provide atlases compatible with ggseg for the cortical regions of the lausanne36, lausanne60, lausanne125, and lausanne250 scale parcellations. In particular, the regions considered in the FTDC-PICSL's QuANTs output. 

## Usage example:
```{r basicusage}
library(ggplot2)
library(ggseg)
load("/path/to/ggsegLausanne/lausannesggeg.Rda")

plot(lausanne36)
```

## more useful usage examples
If data frame 'df' has a column 'tstat' with t-statistics per ROI, indicated either with a column 'label' or columns 'hemi' and 'region' to plot
```{r tstat plot1}
ggseg(.data=df, atlas="lausanne60", mapping=aes(fill=tstat)) + labs(title="t-stat comparisons") + scale_fill_gradient(low="firebrick",high="goldenrod") + theme_custombrain(plot.background = "white") + theme(text=element_text(colour="black"))
```

If looking for both positive and negative values, only if significant based on column 'pval'

```{r tstat plot2way}
ggseg(.data=df[df$pval < 0.05,], atlas="lausanne125", mapping=aes(fill=tstat)) + labs(title=paste(group1, "&", group2, sep=" "), fill="t-stat (p<0.05 unc)") + scale_fill_gradient2(low="firebrick",high="blue") + theme_custombrain(plot.background = "white") + theme(text=element_text(colour="black"))
```

