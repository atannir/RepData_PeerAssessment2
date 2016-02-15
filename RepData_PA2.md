# Reproducible Research: Peer Assessment 2: Storm Damage

<!-- Check for data, download, unpack -->
<!-- We have added the file to the git ignore because it is 47 MB compressed, 535 MB expanded. -->

<!-- This assignment should have a max of 3 figures, which may contain multiple plots, but still only 3 figures -->

<!-- The underlying questions are simple:
Across the US, Which types of events (EVTYPE) were most harmful to population health?
Across the US, which types of events have the greatest economic consequences?
-->

<!--
## automatic generation for small sample
##    STATE__   BGN_DATE   BGN_TIME  TIME_ZONE     COUNTY COUNTYNAME 
##  "numeric"   "factor"  "integer"   "factor"  "numeric"   "factor" 
##      STATE     EVTYPE  BGN_RANGE    BGN_AZI BGN_LOCATI   END_DATE 
##   "factor"   "factor"  "numeric"  "logical"  "logical"  "logical" 
##   END_TIME COUNTY_END COUNTYENDN  END_RANGE    END_AZI END_LOCATI 
##  "logical"  "numeric"  "logical"  "numeric"  "logical"  "logical" 
##     LENGTH      WIDTH          F        MAG FATALITIES   INJURIES 
##  "numeric"  "numeric"  "integer"  "numeric"  "numeric"  "numeric" 
##    PROPDMG PROPDMGEXP    CROPDMG CROPDMGEXP        WFO STATEOFFIC 
##  "numeric"   "factor"  "numeric"  "logical"   "factor"  "logical" 
##  ZONENAMES   LATITUDE  LONGITUDE LATITUDE_E LONGITUDE_    REMARKS 
##  "logical"  "numeric"  "numeric"  "numeric"  "numeric"  "logical" 
##     REFNUM 
##  "numeric" 
-->
<!--
## automatically generated classes, not ideal for most. Use "NULL" to skip a column.
##    STATE__   BGN_DATE   BGN_TIME  TIME_ZONE     COUNTY COUNTYNAME 
##  "numeric"   "factor"   "factor"   "factor"  "numeric"   "factor" 
##      STATE     EVTYPE  BGN_RANGE    BGN_AZI BGN_LOCATI   END_DATE 
##   "factor"   "factor"  "numeric"   "factor"   "factor"   "factor" 
##   END_TIME COUNTY_END COUNTYENDN  END_RANGE    END_AZI END_LOCATI 
##   "factor"  "numeric"  "logical"  "numeric"   "factor"   "factor" 
##     LENGTH      WIDTH          F        MAG FATALITIES   INJURIES 
##  "numeric"  "numeric"  "integer"  "numeric"  "numeric"  "numeric" 
##    PROPDMG PROPDMGEXP    CROPDMG CROPDMGEXP        WFO STATEOFFIC 
##  "numeric"   "factor"  "numeric"   "factor"   "factor"   "factor" 
##  ZONENAMES   LATITUDE  LONGITUDE LATITUDE_E LONGITUDE_    REMARKS 
##   "factor"  "numeric"  "numeric"  "numeric"  "numeric"   "factor" 
##     REFNUM 
##  "numeric"
-->



```r
if(!file.exists("repdata_data_StormData.csv")) {
  if(!file.exists("repdata_data_StormData.csv.bz2")) {
    download.file("https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2FStormData.csv.bz2", "repdata_data_StormData.csv.bz2", quiet = TRUE)
  }
  # unzip("repdata_data_StormData.csv.bz2")
  # error on local .bz2, but worked last assignment on a .zip...
}

## http://stackoverflow.com/questions/13022299/specify-date-format-for-colclasses-argument-in-read-table-read-csv
setClass('myDate')
setAs("character","myDate", function(from) as.Date(from, format="%m/%d/%Y") )

csc = c("NULL", "myDate", "NULL", "NULL", "numeric", "factor",
        "factor", "factor", "NULL", "NULL", "NULL", "NULL",
        "NULL", "NULL", "NULL", "NULL", "NULL", "NULL",
        "NULL", "NULL", "NULL", "NULL", "numeric", "numeric",
        "numeric", "factor", "numeric", "factor", "NULL", "NULL",
        "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL")

# one strategy is to disregard events before 2000 when the classification method changed.

raw_csv <- read.csv("repdata_data_StormData.csv", header = TRUE, colClasses = csc) #, nrows = 10000)

remove(csc)
```

