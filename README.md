# 数据的双录入比对DT
## 读入数据
library(compareDF)
library(readxl)
nx <- read_excel("Desktop/~.xls")
QW <- read_excel("Desktop/~.xls")
## 去除不比对的变量
nx$investigator <- NULL
nx$T3<- NULL
nx$ADT05_5<- NULL
QW$investigator <- NULL
QW$T3<- NULL
QW$ADT05_5 <- NULL
## 进行比对
QW_nx <- compare_df(nx,QW,c("PID","C01") ,limit_html = 900)
QW_nx$html_output
