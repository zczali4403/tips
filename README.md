# tips
Some tips used during learning

1、去除含有缺失值的行
gwas <- na.omit(gwas)

2、在一列中添加字母X
gwas$chr <- paste("X",gwas$chr,,sep="")

3、R中通过tidyr将两列数据合成一列
gwas <- unite(gwas,"chr_pos",chr,pos,sep = "-" remove= FALSE)
将gwas中的列chr和列pos合并为一列，名为chr_pos，用-隔开，remove为TRUE表示将原来的两列删除，为FALSE表示将原来的两列保留

4、用coloc进行共定位分析
result <- coloc.abf(dataset1=list(pvalues=input$pval_nominal_gwas, type="cc", s=0.33, N=50000), dataset2=list(pvalues=input$pval_nominal_eqtl, type="quant", N=10000), MAF=input$maf)
修改s和N对结果的影响不大，因此就算s和N不准确影响也不大

5、使用R中merge()函数合并数据
input <- merge(eqtl,gwas,by = "rs_id",all = FALSE)
all为FALSE的含义是仅返回两数据框中匹配的数据行

6、给R中的列重命名
默认为dplyr中的rename
dplyr和plyr中的rename函数是不一样的
dplyr::rename(data,new=old)
plyr::rename(data,c(old=new))
dplyr::rename(d, two=old2, three=old3)
plyr::renmame(d,c("old2" = "two","old3" = "three"))
alp <- rename(alp,rs_id = snpid)

7、用CMplot画多track的曼哈顿图
CMplot(alp_a2_b2_c2, plot.type="m", LOG10=TRUE, ylim=c(0,80), threshold=c(1e-6,1e-4),multracks = TRUE
       threshold.lty=c(1,2),threshold.lwd=c(1,1),
       threshold.col=c("black","grey"), amplify=F,
       file="jpg",memo="",dpi=1200,
       file.output=TRUE,verbose=TRUE,cex = 0.1)

8、用subset函数提取数据
subset(data,pval <= 5e-8)   格式为subset(data,列名<数值)
注意这里需要用<=不能用<-

9、用separate函数将一列分解为多列，以某种字符为分隔标志
separate函数是dplyr包里的
gwas <- separate(gwas,col = "chr_position",into = c("chr","pos"),sep = "_",remove = FALSE)
remove为FALSE表示不去除原来的列
