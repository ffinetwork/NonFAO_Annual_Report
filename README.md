# Prep Steps

For the more detailed version, refer to the "Annual Report Data
Compilation SOP" which will walk through each step with pictures and
detailed information/instructions. This is just a rough reminder of the
steps.

## Setting up Project Directory 

1. Go to the NonFAO_Annual_Report Github page <            >. 

2. wget https://github.com/[user]/[repo]/archive/[branch].zip
with [user], [repo], and [branch] replaced with the appropriate fields.

Alternatively, if you are having trouble downloading it from Github, you can copy the "NonFAO_Annual_Report" zip file from the FFI annual reports folder to your local computer.

3. Open RStudio and navigate to the NonFAO_Annual_Report folder. Stay in this file location.

## Download Non-FAO Data

1.  Download the most recent non-FAO data from the FAOSTAT website Crops and Livestocks page <       > and
    the Comtrade website <           > by following the instructions in the
    “Instructions for downloading non-FAO data” document in the SOP
    folder.

After following the instructions, you should have three CSV files: 
- `nonfao_trade_data_YEAR.csv` that contains non-FAO trade data from FAOSTAT 
- `nonfao_production_data_YEAR.csv` that contains non-FAO production data from FAOSTAT 
- `comtrade_data_YEAR.csv` that contains non-FAO trade data from Comtrade
(Replace YEAR with the year of the current annual report)

## Run R Code

1. Place the three CSV files in the folder called "Raw_Data". There is already a CSV file in there called `nonfao_country_names.csv` (Edit this if the list of non-FAO countries has changed but be very careful to add country names as listed on the FFI Website exactly!). In total, you should now have four CSV files in the Raw_Data folder.

2.  Open the config.yml document and replace the year with the
    year of the current annual report.

3.  Synchronize the project environment's R packages by:

-   In the R console tab,
    -   install the `renv` package if you do not already have it
        installed. Verify it's installed by running
        `"renv" %in% row.names(installed.packages())` and getting the
        value `TRUE`
-   In the Terminal tab, navigate to the project directory. Type `pwd`
    to get the current directory path
-   In the R console tab,
    -   type `setwd("_")` and replace the blank with the directory path
    -   type `getwd()` and hit the enter button to verify you are in the
        correct directory
    -   type `renv::restore()`

4.  Go back to the terminal tab. Make the three non-FAO grain sheets by:
- First typing `export YEAR="_"` and replace the blank with the current annual report year. This will retrieve the current annual report year as a system environment variable to help the Makefile commands run smoothly
- Then typing `make` to run all the R scripts to create the final three non-FAO grain sheets

# Project Directory Description

-   `Raw_Data/` folder should contain the four raw uncleaned CSV files

    -   "nonfao_trade_data_YEAR.csv"
    -   "nonfao_production_data_YEAR.csv"
    -   "comtrade_data_YEAR.csv"
    -   "nonfao_country_names.csv"

-   `Cleaned_Data/` folder contains the three cleaned RDS files

    -   "nonfao_trade_data_YEAR.rds"
    -   "nonfao_production_data_YEAR.rds"
    -   "comtrade_data_YEAR.rds"

-   `Output_CSV_Files/` folder contains six CSV files (three are sheets
    with FAO crops and livestocks data and three are sheets with
    Comtrade data) [replace YEAR with whatever the year of the current
    annual report is]

    -   "wheat_cropslivestock_YEAR.csv"
    -   "wheat_comtrade_YEAR.csv"
    -   "maize_cropslivestock_YEAR.csv"
    -   "maize_comtrade_YEAR.csv"
    -   "rice_cropslivestock_YEAR.csv"
    -   "rice_comtrade_YEAR.csv"

-   `Final_Output/` folder contains three final CSV files that merge FAO
    crops and livestocks data with Comtrade data for each grain

    -   "nonfao_wheat_YEAR.csv"
    -   "nonfao_maize_YEAR.csv"
    -   "nonfao_rice_YEAR.csv"

-   `Code/` folder contains R scripts described below

-   `Makefile` is a document that specifies how to build the three final
    merged grain sheets automatically. Essentially, it contains rules to
    create each output so one can use a shortcut and doesn't have to run
    all of the individual R code scripts separately.

-   `config.yml` is a document that specifies a parameter or variable
    that we don't want hard-coded into any of the code since it can
    change. It contains one parameter (the year of the current annual
    report) so file names can be customized to the current annual
    report's year

# Code Description

-   `code/clean_data.R`:
    -   clean FAO Crops and Livestocks trade and production data and
        Comtrade dataset from `Raw_Data/` folder
-   `code/wheat_cropslivestock.R`:
    -   read in and compile FAO Crops and Livestocks trade and
        production data from `Raw_Data/` folder for wheat
    -   save wheat trade sheet in `Output_CSV_Files/` folder
-   `code/maize_cropslivestock.R`:
    -   read in and compile FAO Crops and Livestocks trade and
        production data from `Raw_Data/` folder for maize
    -   save maize trade sheet in `Output_CSV_Files/` folder
-   `code/rice_cropslivestock.R`:
    -   read in and compile FAO Crops and Livestocks trade and
        production data from `Raw_Data/` folder for rice
    -   save rice trade sheet in `Output_CSV_Files/` folder
-   `code/wheat_comtrade.R`:
    -   read in and compile Comtrade data from `Raw_Data/` folder for
        wheat
    -   save wheat trade sheet in `Output_CSV_Files/` folder
-   `code/maize_comtrade.R`:
    -   read in and compile Comtrade data from `Raw_Data/` folder for
        maize
    -   save maize trade sheet in `Output_CSV_Files/` folder
-   `code/rice_comtrade.R`:
    -   read in and compile Comtrade data from `Raw_Data/` folder for
        rice
    -   save rice trade sheet in `Output_CSV_Files/` folder
-   `code/nonfao_wheat.R`:
    -   merge FAO Crops and Livestocks and Comtrade wheat sheets
    -   save merged wheat sheet in `Final_Output/` folder
-   `code/nonfao_maize.R`:
    -   merge FAO Crops and Livestocks and Comtrade maize sheets
    -   save merged maize sheet in `Final_Output/` folder
-   `code/nonfao_rice.R`:
    -   merge FAO Crops and Livestocks and Comtrade rice sheets
    -   save merged rice sheet in `Final_Output/` folder
