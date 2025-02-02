# integrated_fishglob_surveys

[![DOI](https://zenodo.org/badge/580133169.svg)](https://zenodo.org/badge/latestdoi/580133169)

Database and processing methods to load, clean, and process public bottom trawl surveys related to the manuscript "An integrated database of fish biodiversity sampled with scientific bottom trawl surveys"

Project linked to FishGlob: Fish biodiversity under global change – a worldwide assessment from scientific trawl surveys https://www.fondationbiodiversite.fr/en/the-frb-in-action/programs-and-projects/le-cesab/fishglob/

<img src ="https://github.com/AquaAuma/integrated_fishglob_surveys/blob/main/fishglob_logo.png" width ="200">

Contributors to repository and related manuscript: Aurore A. Maureaud, Juliano Palacios-Abrantes, Zoë Kitchel, Laura Mannocci, Malin L. Pinsky, Alexa Fredston, Esther Beukhof, Daniel L. Forrest, Romain Frelat, Maria L.D. Palomares, Laurene Pecuchet, James T. Thorson, P. Daniël van Denderen, Bastien Mérigot

Main contact: Aurore A. Maureaud aurore.aqua@gmail.com

### Structure of the repository

*The repository doesn't hold any dataset or any analysis, additional repository will be created for each project.*

**/standard_formats/** includes:
- the fishglob data format, with column names, descriptions and units file *fishglob_data_columns.xlsx*
- the survey standard ids provided by the data owners or us file *Surveys_ID.xlsx*

**/explore.metadata/** to a few updates of the survey metadata (survey id, long, lat, year) to create maps of survey effort

**/taxa_analysis/** contains the taxonomic cleaning procedure for all surveys prior to survey cleaning, list of taxa inclusive (e.g. pelagic taxa) but removes invertebrates and non-marine taxa. List of taxa first created to extract taxa list for trait data compilation. Reference taxonomy from WoRMS https://www.marinespecies.org/, but fishbase also checked.

**/cleaning.codes/** includes all cleaning codes of surveys:
- get.XX.R: R scripts to clean a survey, cleaning and homogenization of each separate survey or groups of surveys (if shared raw format), XX follows the name/abbreviation of the provider/survey described in the file *Surveys_ID.xlsx*
- merge.R : merge all the survey (+ other cleaning task to be done with all data together?)
- compile.R : R script from OceanAdapt
- source_DATRAS_wing_doorspread.R : R code used to clean DATRAS surveys

**/functions/** contains useful functions used in other scripts
- clean_taxa.R: extract accepted taxa name from worms and looks for synonyms matching, cleans taxonomy for aphiaID or scientific names provided - extract aphiaID, fishbaseID, classification, rank and taxa accepted name
- name.filter.fun.R: 
- name.matching.fun.R: 
- cleanspl.R: clean classical problems from taxa
- write_clean_data.R: writes the file with the clean data in the google drive, so that we don't store private data in the github repo
- get_length_weight_coeffs.R: extract length-weights relationship coefficients for a taxa in a specific ecosystem from fishbase

**/length.weight/** contains the length-weight relationships extracted for surveys where weights have to be calculated from abundance at length data: NOR-BTS, DATRAS

**/metadata_docs/** has a README with notes about each survey. This is a place to document changes in survey methods, quirks, etc. It is a growing list. Please add to it.

**/summary/** will contain the quality check plots for all surveys, list of plots required, check the template.Rmd for an overview of plots and items displayed:
1. overview of survey data table
2. number of hauls per year
3. boxplots: area swept, haul duration, depth and number of taxa per year
4. total abundance/weight per year under the different standardization
5. extreme weight/abundance values per year
6. abundance/weight and number of taxa against swept area
7. abundance/weight trends of the 6 most abundant taxa
8. map of survey hauls
9. taxonomic flagging method results 
10. spatio-temporal flagging method results

**/data_descriptor_figures/** contains the R script to construct figures 2-4 for the data descriptor manuscript. 

### Survey data cleaning steps

**Steps** 

1. Merge sub-datasets for one survey

2. Clean & homogenize column names(possible in the same format as CleanTrawlNAmEUr/OceanAdapt to make it easier) following the format described in *fishglob_data_columns.xlsx*

3. Create missing column/make everything in the same units using the standard fishglob format *fishglob_data_columns.xlsx*

4. Integrate the cleaned taxonomy by merging old names with new clean name created in *taxa_data_routine.Rmd*

5. Quality checks on surveys in the summary folder

6. Merge surveys with the merge.R code


### Survey data standardization and flags

**Steps**

1. Taxonomic std: run flag_spp() for each survey region

2. Spatio-temporal footprint flagging for each survey-season/quarter, using the survey_unit column according to two methods in functions apply_trimming_per_survey_unit_method1() and apply_trimming_per_survey_unit_method2() 

3. Display and integrate results in summary files
  

### Contributions per task

*Contributors to code*

- **Cleaning taxonomy**: Juliano 
- **Cleaning surveys**: Juliano, Aurore, Zoë, Dan
- **Summary of surveys**: Juliano, Aurore, Zoë, Laura
- **Merge surveys**: Aurore
- **Standardize surveys**: Laura, Malin, Aurore, Zoë, Alexa
