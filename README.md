# tips
Some tips used during learning

1、去除含有缺失值的行
gwas <- na.omit(gwas)

2、在一列中添加字母X
gwas$chr <- paste("X",gwas$chr,"")

3、R中通过tidyr将两列数据合成一列
gwas <- unite(gwas,"chr_pos",chr,pos,sep = "-" remove= FALSE)
将gwas中的列chr和列pos合并为一列，名为chr_pos，用-隔开，remove为TRUE表示将原来的两列删除，为FALSE表示将原来的两列保留

4、用coloc进行共定位分析
result <- coloc.abf(dataset1=list(pvalues=input$pval_nominal_gwas, type="cc", s=0.33, N=50000), dataset2=list(pvalues=input$pval_nominal_eqtl, type="quant", N=10000), MAF=input$maf)
修改s和N对结果的影响不大，因此就算s和N不准确影响也不大

5、使用R中merge()函数合并数据
input <- merge(eqtl,gwas,by = "rs_id",all = FALSE)
all为FALSE的含义是仅返回两数据框中匹配的数据行
