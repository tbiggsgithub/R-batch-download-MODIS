# R-batch-download-MODIS

1.  MODIS data:  generate a .inp file of urls do download from http://reverb.echo.nasa.gov/reverb

2. Execute the following code in R:
```R
library(RCurl)
library(rgdal)
indir = "C:/Users/tbiggs/AppData/MODIS_downloads/" # Directory with the inp file from reverb
url.list = "urls_to_download.inp" # Name of file generated from reverb website

file.list = read.table(paste(indir,url.list,sep=""))
food = unlist(file.list)

for (j in 1:length(food)){
	wgeturl = as.character(file.list[j,])
	foo = strsplit(as.character(file.list[j,]),"/")[[1]][9]
	dest.fname = strsplit(foo,"\\?")[[1]][1]
	foo = download.file(wgeturl, destfile=paste(workd,dest.fname,sep=""), mode="wb", method='internal')
}
```R
