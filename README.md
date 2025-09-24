# NBA-Teams-Case-Study

### Table of Contents
1. Introduction
2. Background
3. Scenario
4. Ask
5. Prepare
6. Process
7. Analyze
8. Share
9. Act

## 1. Introduction 

## 2. Background

## 3. Scenario 

## 4. Ask

## 5. Prepare

### Data Source

```r
# Install and load necessary packages
install.packages("stringr")
library(stringr)
install.packages("dplyr")
library(dplyr)

# Install Packages for Population and Income
household_income <- read.csv("HouseIncome.csv")
metropolitan_population <- read.csv("MetroPop.csv")

# Cleaning and Formatting
metropolitan_population$MSA <- str_replace_all(metropolitan_population$MSA, fixed("."), "")
metropolitan_population$MSA <- str_remove(metropolitan_population$MSA, ",.*")
household_income$MSA <- str_remove(household_income$MSA, ",.*")

# Combine the Data
combined_data <- left_join(
  household_income,
  metropolitan_population,
  by = "MSA",
  relationship = "many-to-many"
)

# Export Combined data to make adjustments on spreadsheets
write.csv(combined_data, file = "combined_data.csv", row.names = FALSE)
getwd("combined_data.csv")

# Import freshly cleaned combined data from spreadsheets
MSA_combined <- read.csv("MSAcombined.csv")

# Rename Columns 
MSA_combined <- MSA_combined %>%
  rename("Per Captial Personal Income" = "Per.Capita.Personal.Income",
         "2024 Population" = "X2024.Population")

# Install remaining packages
ncaab_rankings <- read.csv("NCAAB.csv")
sports_bars <- read.csv("SportsBars.csv")
fortune_500 <- read.csv("Fortune500.csv")

# Rename Columns 
sports_bars <- sports_bars %>% 
  rename(`Location Quotient` = `Location.quotient`)
ncaab_rankings <- ncaab_rankings %>% 
  rename(`Titles` = `Titiles`)
fortune_500 <- fortune_500 %>%
  rename(`Fortune 500 Companies` = `Fortune.500.Companies`)
```
