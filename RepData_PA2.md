# Reproducible Research: Peer Assessment 2: Storm Damage

<!-- Check for data, download, unpack -->
<!-- We have added the file to the git ignore because it is 47 MB compressed, 535 MB expanded. -->

<!-- This assignment should have a max of 3 figures, which may contain multiple plots, but still only 3 figures -->

<!-- The underlying questions are simple:
Across the US, Which types of events (EVTYPE) were most harmful to population health?
Across the US, which types of events have the greatest economic consequences?
-->


```r
if(!file.exists("repdata_data_StormData.csv")) {
  if(!file.exists("repdata_data_StormData.csv.bz2")) {
    download.file("https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2FStormData.csv.bz2", "repdata_data_StormData.csv.bz2", quiet = TRUE)
  }
  # unzip("repdata_data_StormData.csv.bz2")
  # error, but worked last assignment on a .zip...
}


csvSample <- read.csv("repdata_data_StormData.csv", header = TRUE, nrows = 1000)
csc = sapply(csvSample, class)
#csvSampleClasses["BGN_DATE"] <- "Date"
# csvSampleClasses["BGN_TIME"] <- "numeric" #hopefully will fix issue with leading zeros
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

csc = c("NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", 
        "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", 
        "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL",
        "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL")


# one strategy is to disregard events before 2000 when the classification method changed.

raw_csv <- read.csv("repdata_data_StormData.csv", header = TRUE, colClasses = csc,
                    nrows = 1000)

raw_csv
```

```
## data frame with 0 columns and 0 rows
```

```r
# classes <- sapply(raw_csv, class)
# classes

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

remove(csvSample)
remove(csc)

# 37 variables, 902297 observations, caching is very helpful here.
```

