# TCGA

使用R包cgdsr来下载TCGA的数据

参考使用教程http://firebrowse.org/tutorial/FireBrowse-Tutorial.pdf


接下来我们要讲的就是cbioportal网站提供的一个R接口，非常好用，只需记住4个函数即可！！！

只需熟记getCancerStudies，getCaseLists，getGeneticProfiles，getProfileData需要什么参数以及它们返回了什么对象即可！

install.packages("cgdsr",repos="http://cran.us.r-project.org")
library(cgdsr)
mycgds <- CGDS("http://www.cbioportal.org/public-portal/")
test(mycgds)
# Get list of cancer studies at server
## 获取有哪些数据集
all_TCGA_studies <- getCancerStudies(mycgds)

第一个函数就是获取我们的cbioportal网站里面存储的关于TCGA的研究项目列表（每个study都是一篇文章），至今有126个(2016年7月12日21:37:40)

具体的文章可以见：https://tcga-data.nci.nih.gov/docs/publications/

前面我下载过胃癌的RNA表达数据，我们这里可以验证一下：

我这里用R来下载一次看看

stad2014 <- "stad_tcga_pub"   ##这篇文章里面的数据

## 获取在stad2014数据集中有哪些样本列表，

all_tables <- getCaseLists(mycgds, stad2014)

dim(all_tables)

## 我们需要验证一下下载的mRNA表达量数据，所以我们选择下面这个样本列表

my_table <- "stad_tcga_pub_rna_seq_v2_mrna"

## 而后获取有哪些数据可以下载

all_dataset <- getGeneticProfiles(mycgds, stad2014)

my_dataset <- 'stad_tcga_pub_rna_seq_v2_mrna'  ##然后我们选择下载mRNA数据

BRCA1 <- getProfileData(mycgds, "BRCA1", my_dataset, my_table)  ## 根据my_table这个样本列表来下载my_dataset这种数据

##还可以下载临床数据来对比

getClinicalData(mycgds, my_table) ##临床数据经常下载失败，不知道为什么

拿到的数据，就可以与之前在TCGA官网里面下载的数据比较啦！！

但是下面的链接已经失效啦！

临床数据：https://tcga-data.nci.nih.gov/docs/publications/stad_2014/20140110_STAD_Clinical_Data_Blacklisted_Cases_Removed.xlsx

RPKM值表达数据：https://tcga-data.nci.nih.gov/docs/publications/stad_2014/RPKM_Expression_Matrix.291Samples_GAF3genes.BCGSC.20131127.tsv
