# R-batch-download-MODIS

1.  MODIS data:  generate a file of urls to download from http://reverb.echo.nasa.gov/reverb
2.  Get a username and password from reverb.
You can call it anything; here the name is "mod11a1_JUN2002-MAY2003.csv"

2. Execute the following code in R:
```R
library(httr)
indir = "C:/Users/tbiggs/AppData/MODIS_downloads/" # Directory with the cvs file from reverb.  Data will be downloaded to this directory
url.list.fname = "mod11a1_JUN2002-MAY2003.csv"
file.list = read.table(paste(indir,url.list.fname,sep=""))

for (j in 1:length(file.list)){
	wgeturl = as.character(file.list[j])
	dest.fname = strsplit(as.character(file.list[j]),"/")[[1]][9]  # Get the filename without the rest of the url.
	b = GET(wgeturl,write_disk(paste0(indir,dest.fname),overwrite=TRUE),authenticate("yourusername","yourpwd"))
	print(paste(j,"of ",length(file.list)))
  	flush.console()
}
```
