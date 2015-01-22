koleso_razmer-data-downloading
==============================

library(xlm)
library(xlsx)

weburl <- "http://www.koleso-razmer.ru/"

 doc1 <- htmlParse(weburl)
 
 links <- xpathSApply(doc1, "//a/@href")
 
 free(doc1)
 
 linkvec1 <- as.vector(links)
 
linkvec1

linkvec11 <- linkvec1[6:113]

linksto2 <- gsub(" ", "", paste("http://www.koleso-razmer.ru",linkvec11))

lp <- function(x){

x1 <- htmlParse(x)

links <- xpathSApply( x1 , "//a/@href")

free(x1)

linvec <- as.vector(links)}

fvec <- lapply(linksto2, lp)

fvec2 <- cbind(rep(seq_along(fvec), times=sapply(fvec, length)), unlist(fvec))

write.xlsx(fvec2, "links_adresses_raw.xlsx")

--Download result into the Excel process and upload back for next steps. It cuts needed time.

ltosize <- read.xlsx("links_adresses_raw.xlsx", 1)

l <- ltosize[ ,"X2"]

linktosize <- gsub(" ", "", paste("http://www.koleso-razmer.ru", l))

sizef <- function(x){

doc <- htmlParse(x)

car <- xpathSApply(doc, "//td", xmlValue)

ca1 <- gsub("\t", "" , car)

ca2 <- gsub("\n", "" , ca1)

ca3 <- gsub("\r", "" , ca2)

free(doc)

cars <- as.vector(ca3)

return(cars)
}

SizeList2 <- cbind(rep(seq_along(SizeList), times=sapply(SizeList, length)), unlist(SizeList))

--slm1 <- as.matrix(SizeList2) 

write.table(SizeList2, file = "sizemat.txt", row.names=FALSE, col.names=FALSE)
