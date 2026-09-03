Reading in files:
```
##File Path
PAT <- file.path("../COLONY_2026", "BZFull_20260825.Paternity")
## Read in file
pat <- read.delim(PAT, sep = ",", header = TRUE) #commas used to seperate values
```

### Setting up code chunks
If you want a code chunk to not show any of the warnings, message when rending rMarkdowns:
`{R, message=FALSE, warning=FALSE, echo=FALSE}`
