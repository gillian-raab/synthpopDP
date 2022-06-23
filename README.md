# synthpopDP
New version of synthpop with catall and ipf having options for differential privacy
For general synthpop info go to CRAN or to www,synthpop.org.uk
To read papar about this go to https://arxiv.org/abs/2206.01362
Here is some R code to get you started.


#########################################################
library(synthpop)

test <- SD2011[,c("sex","agegr","socprof","marital")]

set.seed(56342)

############ synthesise non DP

syncatall <- syn(test, method= "catall", catall.priorn = 10, catall.epsilon = 0)

synipf <- syn(test, method= "ipf", ipf.priorn = 10, ipf.epsilon = 0)

############ synthesise  DP

syncatallDP <- syn(test, method= "catall", catall.priorn = 10, catall.epsilon = .1)

synipfDP <- syn(test, method= "ipf", ipf.priorn = 10, ipf.epsilon = .1)

########### disclosure measure percent replicated ubiques

ru_catall <- replicated.uniques(syncatall, test)$per.replications ;ru_catall

ru_ipf <- replicated.uniques(synipf, test)$per.replications ;ru_ipf

ru_catallDP <- replicated.uniques(syncatallDP, test)$per.replications ;ru_catallDP

ru_ipfDP <- replicated.uniques(synipfDP, test)$per.replications ;ru_ipfDP


############ utility S_pMSE

Ucatall <- mean(utility.tables(syncatall,test,"twoway",  plot = FALSE,)$tabs[,2]);Ucatall

Uipf <- mean(utility.tables(synipf,test,"twoway",  plot = FALSE,)$tabs[,2]);Uipf

UcatallDP <- mean(utility.tables(syncatallDP,test,"twoway",  plot = FALSE,)$tabs[,2]);UcatallDP

UipfDP <- mean(utility.tables(synipfDP,test,"twoway",  plot = FALSE,)$tabs[,2]);UipfDP

#############################################
