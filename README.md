# LHL_midterm_project
LHL Midterm Project: Data Analysis, Visualization, and Statistical Modelling of US Tornadoes
---

By: Jordan Kanustu and Brigitte Sullivan
Submitted on: Tuesday, October 3, 2023
Lighthouse Labs Data Science Program

# Project/Goals

- Perform Data Analysis US Tornadoes Data
    - uncover meaningful insights using statistical modeling and data visualization practices
- Perform Statistical Modelling US Tornadoes Data
    - form high-level questions for the data  In this project, we hypothesized about the relationship between tornado frequency and climate change (specifically annual average temperature). We assumed and wanted to test the idea that as global temperatures rise so will the frequency of tornadoes in the US. This hypothesis can be framed as:
    - ### **Null hypothesis:**  There is no relationship between the annual frequency of tornadoes and the US's annual average temperature. 
    - ### **Alternative hypothesis:** There is a relationship between the annual frequency of tornadoes and the US's annual average temperature.
- Summarize the data visually using Tableau

# Process

## 1. Extract Data 
- find a data sources:
    - tornado data set found on Kaggle 
    - researched external data sources that contained the average annual temperature in the US for roughly the same period as our data set
- load both data sources into pandas dataframes and merge the USA annual average temperature for each year. 

[Link - Joining)](https://github.com/Kanustu/LHL_midterm_project/blob/main/notebooks/1_joining.ipynb)

## 2. Clean Data 
- Cleaning steps performed:
     - renamed columns with more descriptive terms
     - dropped extraneous, duplicated columns (month, day)
- Validate against source Data Dictionary
    - The Kaggle data set was partially pre-cleaned, however when researching data, we found the original [source data and data dictionary](https://www.spc.noaa.gov/wcm/data/SPC_severe_database_description.pdf) which presented several potential cleaning tasks. Steps were performed to confirm whether our data set had addressed these issues or not. 
- Missing values:
    - Determine the proportion of null values for all rows. Only two features contained missing values. 
        - Magnitude had .05% nulls, and so these records were removed. 
        - Property loss had nearly 40% nulls, so an alternative method of addressing these missing values would be required since removing 40% of the records could significantly affect the analysis quality. 
        - Preliminary EDA revealed that existing values of property loss showed a significant proportion of outliers. 
        - missing values for property loss were filled with the median property loss value for that year 
        - QA:
            - A new column added with complete values for all records,  
            - locating a median value for one year locating the missing value record and confirming the new value was correctly loaded
- Normalize Data
    - due to the wide range of possible numeric values for many features the data set was scaled between values 0-1 and exported into a separate file to determine if the statistical model improves using scaled data.
- Export normalized clean data and clean data into two CSV files


[Link - Cleaning Notebook)](https://github.com/Kanustu/LHL_midterm_project/blob/main/notebooks/2_cleaning.ipynb)

## 3. Exploratory Data Analysis (EDA)

- methodical process to EDA was adopted, EDA included:
    - getting summary statistics 
    - confirming the count of null records (which was 0 due to the cleaning steps performed, this step QA'd the cleaning done previously)
    - checking for duplicates. Duplicates were found in the ID feature, however the source data explains that each tornado is uniquely identified using an ID, but that one tornado may have multiple records if it crosses state/county borders
- Visualizations: 
    - produced a variety of visualizations using heatmaps, scatter plots, box plots, line charts, bar charts, and histograms to get a sense of the data. 

[Link - EDA Notebook)](https://github.com/Kanustu/LHL_midterm_project/blob/main/notebooks/3_eda.ipynb)

## 4. Statistical Modelling

- Perform statistical modeling with limited scope and time permitting return and refine modeling. 
- chose to focus on the total unique tornadoes per year and the annual average temperature. 
- used scaled data for the statistical model to control for the different scales of each feature.  
- the results of the statistical modeling are summarized in the **Results** section of this document. 


[Link - Statistical Modelling Notebook](https://github.com/Kanustu/LHL_midterm_project/blob/main/notebooks/4_modelling.ipynb)


## 5. Visualise Data using Dashboards

- load clean data set into Tableau and create visualizations. 
- visualization types include maps, line charts, bar graphs 

[Link - Tableau Workbook](https://github.com/Kanustu/LHL_midterm_project/blob/main/notebooks/4_modelling.ipynb)


# Results
Overall results: 

- tornadoes are an east coast midwest problem. The West Coast sees little tornadoes. 
- several times in the data where there was a significant increase in the frequency of tornadoes per year followed by a sizeable drop the following year. 1974, 2008, and 2011 saw historically high degree of tornadoes and also occurred during an El Nino/Nina year

Here are the results of the statistical modeling performed: 

* The adjusted R-square value in the latest model was **0.186**. 
    * Meaning that 18.6% of the variance in the dependent variable (sum_tornadoes) can be explained by the independent variable (average annual US temperature). 
    * This is considered a fairly weak relationship, and the model's ability to accurately predict the number of tornadoes per year is poor.
* Despite the adjusted r-squared being relatively weak, the annual US average temperature is still statistically significant with a p-value of 0.000 in predicting total tornadoes per year. 
* The model's f-statistic has a low value of 0.000115 indicating there is sufficient evidence to reject the null hypothesis that there is no relationship between the total number of tornadoes per year and annual average us temperature. 
* Our team's original hypothesis that as global temperatures rise, the frequency of tornadoes is supported by this model. 

# Challenges
- unclear expectations regarding collaboration and division of work meant much of upfront project time was spent trying to understand Git rather than on project deliverables
- comflicting messages meant approach to collaboration changed several times and delayed progress
- collaboration accross various timezones and work schedules meant there was limited time for the group to work syncronously



# Future Goals
- Perform multivariate linear regression to find a stronger model.
- Population density from the 1950s to 2019 would more than likely be different in these locations which would affect fatalities and prop loss. 
- Investigate the significant increase followed by a significant decrease in tornadoes the following year and its relationship to the El Nino/La Nina weather patterns. El Nino/El Nina specifically affects the south, south/east regions of the u.s.. Perform a classification model to determine the relationship between El Nino/El Nina and tornado frequency. 