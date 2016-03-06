# Categorical-data-analysis
# Mantel M^2 Test

ranktest <- function(datalol){
  
  datalol <- as.data.frame(datalol)
  row_number <- dim(datalol)[1]
  col_number <- dim(datalol)[2]
  
  aq<- 0
  rankuu <- NULL
  for(i in 1:col_number){
    aq[1]=0
    aq[i+1] <- sum(datalol[1:row_number,i])+aq[i]
    rankuu[i] <- (1+aq[i+1]+aq[i])/2
  }
  
  bq <- NULL
  rankvv <- NULL
  for(i in 1:row_number){
    bq[1]=0
    bq[i+1] <- sum(datalol[i,1:col_number])+bq[i]
    rankvv[i] <- (1+bq[i+1]+bq[i])/2
  }
  
  zero <- abs(length(rankuu)-length(rankvv))
  a <- matrix(c(rankuu,rankvv, rep(0,zero)),nrow=length(rankuu))
  
  x <- NULL
  for(i in 1:col_number){
    x <- c(x, rep(a[i,1],colSums(datalol)[[i]]))
  }
  
  y <- NULL
  for(i in 1:col_number){
    for(j in 1:row_number){
      y <- c(y,rep(a[j,2],datalol[j,i]))
    }
  }
  
  total <- as.matrix(rowSums(datalol))
  yt <<-cor(x,y)^2*(colSums(total)-1)
  print(cor(x,y)^2*(colSums(total)-1))
  
}
edu_salary <- matrix(c(11,52,23,22,9,44,13,10,9,41,12,27), nrow = 3, byrow = T,
                     dimnames = list(salary=c("low", "middle", "high"), edu=c("a","b","c","d")))
ranktest(edu_salary)
