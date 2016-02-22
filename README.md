# 19.feb.16
library(foreign)
sociodemo <- read.dbf("C:\\Users\\SALA-C9\\Downloads\\SDEMT215.dbf")
table(sociodemo$CD_A)
table(sociodemo$CLASE1)
sociodemo$R_DEF1<-as.numeric(as.character(sociodemo$R_DEF))
sociodemo$C_RES1<-as.numeric(as.character(sociodemo$C_RES))
sociodemo$EDA1<-as.numeric(as.character(sociodemo$EDA))
precod<-subset(sociodemo, ((R_DEF1==0) & (C_RES1==1 | C_RES1==3) & (EDA1>=15 & EDA1<=98)),select = c(EDA1, SEX, HRSOCUP, CLASE2, CLASE1, CLASE3))
table(precod$R_DEF1)
table(precod$C_RES1)
table(precod$EDA1)
#####  =! diferentre en R
attach(precod)
CLASE2V1<-table(CLASE2)
CLASE2V1
#### histograma
hist(CLASE2,)
hist(CLASE2, main="Grafica 1. Distribucion de la poblacion de 15 años o mas, 2015",
     xlab="Tipo de ocupada", ylab="Poblacion (miles)",
     xlim=c(1,4), ylim=c(0,200000), 
     border= F, pch=18,col=c("yellow","orange","green","black"))
CLASE2V1<-as.numeric(as.character(CLASE2)) ## se convierte a numerico

sd1<-subset(sociodemo,CLASE2==1,select=c(EDA,SEX,HRSOCUP,CLASE2,CLASE1,CLASE3,EDA5C,IMSSISSSTE))
frec<-table(sd1$IMSSISSSTE)
frec
pie(frec)
### labels le ponemos la etiqueta debe ser vector
pie(frec,labels=c("Imss","Issste","Otra","No recibe","No especificado"),
    main="Institución de atención medica")
### col para poner color a cada sector en este caso es un vector
pie(frec,labels=c("Imss","Issste","Otra","No recibe","No especificado"),
    main="Institución de atención medica",
    col=c("green","red","blue","yellow","orange"))
frec1<-table(sd1$EDA5C)
barplot(frec1)
barplot(frec1,main="Cinco grupos de edad")
barplot(frec1,main="Cinco grupos de edad",col=c("green","red","blue","yellow","orange"))
frec
## etiquetas se pueden poner con names.arg
barplot(frec1,main="Grafica 1. Cinco grupos de edad",col=c("green","red","blue","yellow","orange"),
        names.arg=c("menor","14 a 24","25 a 44","45 a 64","65 y más","n.e"))
barplot(frec1,main="Grafica 1. Cinco grupos de edad",col=c("green","red","blue","yellow","orange"),
        names.arg=c("menor","14 a 24","25 a 44","45 a 64","65 y más","n.e"),ylim=c(0,85000))
## tambien podemos poner los nombres en nuestra variable
names(frec1)<-c("menor a 14","14-24","25-44","45-64","65+","n.e")
barplot(frec1,main="Cinco grupos de edad", col=c("green","red","blue","yellow","orange"))
## xlab y ylab es para pner los titulos de los ejes
barplot(frec1,main="Cinco grupos de edad", col=c("green","red","blue","yellow","orange"),
        names.arg=c("menor a 14","14-24","25-44","45-64","65+","n.e"),
        xlab="Edad",ylab="Poblacion",ylim=c(0,90000))
help(memory.size)
