Reading in files:
```
##File Path
PAT <- file.path("../COLONY_2026", "BZFull_20260825.Paternity")
## Read in file
pat <- read.delim(PAT, sep = ",", header = TRUE) #commas used to seperate values
```

How find list the files in a specific folder: `> list.files(path = "data/cleannames")`
### Setting up code chunks
If you want a code chunk to not show any of the warnings, message when rending rMarkdowns:
`{R, message=FALSE, warning=FALSE, echo=FALSE}`

### Writing files to output directories
```
# Set the directory
output_dir <- "data/outputexploration"
# create the directory if it doesn't exist
dir.create(
  output_dir,
  recursive = TRUE,
  showWarnings = FALSE
)
# Write the file to that out directory
write_csv(
  selected_hatchlings,
  file = file.path(output_dir,"FDN_M008_FDN_M009_hatchlings.csv"),
  na = ""
)
```

How to write multiple files at once:

```
library(purrr)
# Create an output directory
output_dir <- "data/cleannames"

dir.create(
  output_dir,
  recursive = TRUE,
  showWarnings = FALSE
)

# Put cleaned outputs in a named list
clean_colony_outputs <- list(
  BestConfig    = bestconfig_clean,
  Paternity     = pat_clean,
  FullSibDyad   = fullsib_clean,
  HalfSibDyad   = halfsib_clean,
  ParentPair    = parentpair_clean
)

# Write each data frame to a CSV
purrr::iwalk(
  clean_colony_outputs,
  \(dat, output_name) {
    readr::write_csv(
      dat,
      file = file.path(
        output_dir,
        paste0(output_name, "_clean.csv")
      ),
      na = ""
    )
  }
)
```
### Tables for markdowns: 
```
knitr::kable(
  head(maternity_review_display, 25),
  col.names = c(
    "Offspring",
    "Best mother",
    "Best probability",
    "Candidate rank",
    "Candidate mother",
    "Candidate probability"
  ),
  align = c("l", "l", "r", "r", "l", "r")
) |>  
  kable_styling() %>%
  scroll_box(height = "400px")
```
