# data-analysis
library(RODBC)
mydata <- function(m,n){
  path<- paste0("C:/Users/Administrator/Desktop/",m)
  setwd(path)
  channel<-odbcConnectAccess("dongtai6.mdb")
  data1<-sqlFetch(channel, "dongtai6")
  data2<-sqlFetch(channel, "dongtai61")
  data3<-sqlFetch(channel, "dongtai63")
  data4<-sqlFetch(channel, "dongtai64")
  data5<-sqlFetch(channel, "dongtai65")
  data_1 <- cbind(data2,data3,data4,data5)
  data_1$GlobalRecordId <- NULL
  data_1$GlobalRecordId <- NULL
  data_1$GlobalRecordId <- NULL
  data_1$GlobalRecordId <- NULL
  clerkcdc <- rep(n,length(data1$UniqueKey))
  data<- data.frame(data_1,clerkcdc)
}

#dt06lianyi_first
ly1song <- mydata("路径1","ly1song")
ly1zhuang <- mydata("路径2","ly1zhuang")
ly1wu<- mydata("路径3","ly1wu")
ly06first <- rbind(ly1song,ly1zhuang,ly1wu)
#dt06lianyi_second
ly2song <- mydata("路径1_2","ly2song")
ly2zhuang <- mydata("路径2_2","ly2zhuang")
ly2wu <- mydata("路径3_2","ly2wu")
ly06second <- rbind(ly2song,ly2zhuang,ly2wu)
#dt06shiyan_first
sy1wu <- mydata("路径4","sy1wu")
sy1song<- mydata("路径5","sy1song")
sy06first <- rbind(sy1wu,sy1song)
#dt06shiyan_second
sy2wu <- mydata("路径4_2","sy2wu")
sy2song<- mydata("路径5_2","sy2song")
sy06second <- rbind(sy2wu,sy2song)

dt06first <- rbind(ly06first,sy06first)
dt06second <- rbind(ly06second,sy06second)

dt06first$entrydate <- NULL
dt06first$Clerk <- NULL
dt06first$clerkcdc <- NULL
dt06first$relationship <- NULL

dt06second$entrydate <- NULL
dt06second$Clerk <- NULL
dt06second$clerkcdc <- NULL
dt06second$relationship <- NULL

library(compareDF)
com_df <- compare_df(dt06first,dt06second,c("childnumber") ,limit_html = 800,exclude = c("clerk"))
com_df$html_output
