![CTSgetR](https://github.com/dgrapov/CTSgetR/blob/master/etc/ctsgetR_logo.png?raw=true)

R interface to the [Chemical Translation Service (CTS)] (http://cts.fiehnlab.ucdavis.edu/)

### Installation

```r
#library(devtools) # install.packages("devtools") if missing
#install_github(repo = "CTSgetR", username = "dgrapov",ref="simple")
library(CTSgetR)
```

### How to use the interface
```r
help(CTSgetR)
```

### View possible translation options between > 200 databases.

```r
trans<-unlist(CTS.options())
head(trans,10)
```

```
##  [1] "BioCyc"                    "CAS"                      
##  [3] "ChEBI"                     "Chemical Name"            
##  [5] "Human Metabolome Database" "InChI Code"               
##  [7] "InChIKey"                  "KEGG"                     
##  [9] "LMSD"                      "LipidMAPS"
```

### Find a database of interest.

```r
want<-'zinc'
fuzzy<-1 # larger more fuzzy matching
trans[agrepl(want,trans,ignore.case=TRUE,max.distance=fuzzy)]
```

```
## [1] "InChI Code"                    "InChIKey"                     
## [3] "ZINC"                          "Tetrahedron Scientific Inc"   
## [5] "AK Scientific, Inc. (AKSCI)"   "Ark Pharm, Inc."              
## [7] "Zancheng Functional Chemicals"
```

### Example usage

```r
library(CTSgetR)
#translate from chemical name to InchiKey
id<-"alanine"
from<-"Chemical Name"
to<-"InChIKey"
CTSgetR(id,from,to,progress=FALSE)
```

```
##   fromIdentifier searchTerm toIdentifier                       value
## 1  Chemical Name    alanine     InChIKey QNAYBMKLOCPYGJ-REOHCLBHSA-N
```

```r
#translate from one to many identifiers 
id<-c("DMULVCHRPCFFGV-UHFFFAOYSA-N","ZPUCINDJVBIVPJ-LJISPDSOSA-N","ZAGRKAFMISFKIO-QMTHXVAHSA-N")
from<-"InChIKey"
to<- c("Chemical Name", "PubChem CID", "KEGG","Human Metabolome Database")
CTSgetR(id,from,to,progress=FALSE,limit.values = FALSE)
```

```
##    fromIdentifier                  searchTerm              toIdentifier
## 1        InChIKey DMULVCHRPCFFGV-UHFFFAOYSA-N             Chemical Name
## 2        InChIKey DMULVCHRPCFFGV-UHFFFAOYSA-N             Chemical Name
## 3        InChIKey ZPUCINDJVBIVPJ-LJISPDSOSA-N             Chemical Name
## 4        InChIKey ZPUCINDJVBIVPJ-LJISPDSOSA-N             Chemical Name
## 5        InChIKey ZAGRKAFMISFKIO-QMTHXVAHSA-N             Chemical Name
## 6        InChIKey ZAGRKAFMISFKIO-QMTHXVAHSA-N             Chemical Name
## 7        InChIKey DMULVCHRPCFFGV-UHFFFAOYSA-N               PubChem CID
## 8        InChIKey ZPUCINDJVBIVPJ-LJISPDSOSA-N               PubChem CID
## 9        InChIKey ZAGRKAFMISFKIO-QMTHXVAHSA-N               PubChem CID
## 10       InChIKey ZAGRKAFMISFKIO-QMTHXVAHSA-N               PubChem CID
## 11       InChIKey DMULVCHRPCFFGV-UHFFFAOYSA-N                      KEGG
## 12       InChIKey ZPUCINDJVBIVPJ-LJISPDSOSA-N                      KEGG
## 13       InChIKey ZAGRKAFMISFKIO-QMTHXVAHSA-N                      KEGG
## 14       InChIKey DMULVCHRPCFFGV-UHFFFAOYSA-N Human Metabolome Database
## 15       InChIKey ZPUCINDJVBIVPJ-LJISPDSOSA-N Human Metabolome Database
## 16       InChIKey ZAGRKAFMISFKIO-QMTHXVAHSA-N Human Metabolome Database
##                                                                                                  value
## 1                                                             2-(1H-Indol-3-yl)-N,N-dimethylethanamine
## 2                                                                1H-Indole-3-ethanamine, N,N-dimethyl-
## 3  8-Azabicyclo[3.2.1]octane-2-carboxylic acid, 3-(benzoyloxy)-8-methyl-, methyl ester, (1R,2R,3S,5S)-
## 4                 Methyl (1R,2R,3S,5S)-3-(benzoyloxy)-8-methyl-8-azabicyclo[3.2.1]octane-2-carboxylate
## 5                                            (8beta)-6-Methyl-9,10-didehydroergoline-8-carboxylic acid
## 6                                       Ergoline-8-carboxylic acid, 9,10-didehydro-6-methyl-, (8beta)-
## 7                                                                                                 6089
## 8                                                                                               446220
## 9                                                                                             11861108
## 10                                                                                                6717
## 11                                                                                              C08302
## 12                                                                                              C01416
## 13                                                                                                    
## 14                                                                                           HMDB05973
## 15                                                                                                    
## 16
```

### Check out some more [translation examples](https://github.com/dgrapov/CTSgetR/wiki/Chemical-Translation-System-in-R).

## TODO
- [ ] Get POST to work
- [ ] Make it more awesome!

