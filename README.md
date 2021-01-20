[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="888" alt="Visit QuantNet">](http://quantlet.de/)

## [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **VISAplot** [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/)

```yaml

Name of Quantlet: VISAplot

Published in: Quantlet

Description: ‘Quant analysis of financial time series´

Keywords: VISA, financial time series, moving average 

Author: Maria Culjak 
```

![Picture1](Overall%20MA%20plot.png)

### R Code
```r

setwd("/Users/mariaculjak/Downloads/Metis")
getwd()
install.packages("readxl")
library(readxl)
overall <- read_excel("Overseas spend(WH).xlsx", sheet = "total overseas spend")
overall
Japan=read_excel("Overseas spend(WH).xlsx", sheet = "Japan")
Japan=Japan[,-1]
Japan=Japan[,-2]
Japan=Japan[ , c("CPD Date", "Amt (USD)")]
Japan=Japan[order(as.Date(Japan$`CPD Date`, format="%d/%m/%Y")),]
Japan
Australia=read_excel("Overseas spend(WH).xlsx", sheet = "Australia")
Australia=Australia[,-1]
Australia=Australia[,-2]
Australia=Australia[ , c("CPD Date", "Amt (USD)")]
Australia=Australia[order(as.Date(Australia$`CPD Date`, format="%d/%m/%Y")),]
Australia
USA=read_excel("Overseas spend(WH).xlsx", sheet = "USA")
USA=USA[,-1]
USA=USA[,-2]
USA=USA[ , c("CPD Date", "Amt (USD)")]
USA=USA[order(as.Date(USA$`CPD Date`, format="%d/%m/%Y")),]
USA
par(bg=NA)
plot(overall, type="l", xlab ="Date", bg=NA)
plot(Japan, xlab ="Date", bg=NA, type="l")
plot(Australia, xlab="Date", bg=NA, type="l")
plot(USA, xlab="Date", bg=NA, type="l")
graphics.off()
install.packages("forecast")
library(forecast)
par(mfrow=c(4,1))
Acf(overall$`Amt (USD)`, lag.max = 30, type = c("correlation", "covariance", "partial"), plot = TRUE, na.action = na.contiguous, demean = TRUE, main="Overall")
Acf(Japan$`Amt (USD)`, lag.max = 30, type = c("correlation", "covariance", "partial"), plot = TRUE, na.action = na.contiguous, demean = TRUE, main="Japan")
Acf(Australia$`Amt (USD)`, lag.max = 30, type = c("correlation", "covariance", "partial"), plot = TRUE, na.action = na.contiguous, demean = TRUE, main="Australia")
Acf(USA$`Amt (USD)`, lag.max = 30, type = c("correlation", "covariance", "partial"), plot = TRUE, na.action = na.contiguous, demean = TRUE, main="USA")
par(mfrow=c(4,1))
Pacf(overall$`Amt (USD)`, lag.max = 30, plot = TRUE, na.action = na.contiguous, demean = TRUE, main="Overall")
Pacf(Japan$`Amt (USD)`, lag.max = 30, plot = TRUE, na.action = na.contiguous, demean = TRUE, main="Japan")
Pacf(Australia$`Amt (USD)`, lag.max = 30, plot = TRUE, na.action = na.contiguous, demean = TRUE, main="Australia")
Pacf(USA$`Amt (USD)`, lag.max = 30, plot = TRUE, na.action = na.contiguous, demean = TRUE, main="USA")
install.packages("zoo")
library(zoo)
par(bg=NA)
m.av<-rollmean(overall$`Amt (USD)`, 7,fill = list(NA, NULL, NA))
plot(overall, type="l", xlab ="Date", bg=NA)
lines(overall$`CPD Date`, m.av, col="red")
m.av1<-rollmean(Japan$`Amt (USD)`, 7,fill = list(NA, NULL, NA))
plot(Japan, type="l", xlab ="Date", bg=NA)
lines(Japan$`CPD Date`, m.av1, col="red")
m.av2<-rollmean(Australia$`Amt (USD)`, 7,fill = list(NA, NULL, NA))
plot(Australia, type="l", xlab ="Date", bg=NA)
lines(Australia$`CPD Date`, m.av2, col="red")
m.av3<-rollmean(USA$`Amt (USD)`, 7,fill = list(NA, NULL, NA))
plot(USA, type="l", xlab ="Date", bg=NA)
lines(USA$`CPD Date`, m.av3, col="red")





```

automatically created on 2021-01-20