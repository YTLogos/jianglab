## LDheatmap

LDheatmap, as a heat map, is to display measures of pairwise linkage disequilibria betweens SNPs.

{{<figure src="/img/LDheatmap.png" width="1000" hegiht="1200" align=center >}}

Here we developed the shiny app LDheatmap to extract SNPs from our lab's 1000 Brassica napus database and get the LDheatmap, you just need to select the chromosome and enter genome region (start, end) you want to extract and visualize! You can run the analysis in [LDheatmap-app](http://rapeseed.zju.edu.cn:3838/LDheatmap). The app will extract the SNPs from the 1000 B.napus database,if you want to use your own samples you need to prepare your sample file (.txt) like this (just need the first column):

```
R4155
R4156
R4157
...
```

Then you just need to select the chromosome, upload your sample file (if you need), enter genome region (start, end) and click the button Run Analysis. It will return a vcf file contains the SNPs information and a pdf file of LDheatmap. 


You can click [**Here**](http://rapeseed.zju.edu.cn:3838/LDheatmap) to access the app.