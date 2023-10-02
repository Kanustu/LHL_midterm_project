# LHL_midterm_project
LHL Midterm Project: Data Analysis, Visualization and Statistical Modelling of US Tornadoes
---

By : Jordan Kanustu and Brigitte Sullivan
Submitted on: Tuesday, October 3, 2023
Lighthouse Labs Data Science Program

# Project/Goals


- Ask a relevant question of the data and uncover meaningful insights using statistical modelling and data vizualization practices
- form highlevel question for the data  In this project, we hypothesized about the relationship between tornado frequency and climate change (specifically annual average temperature). We assumed and wanted to test the idea  that as global temperatures rise so will the frequency of tornadoes in the US. This hypothesis can be framed as:
### **Null hypothesis:** 
There is no relationship beween the annual frequency of tornadoes and the US's annual average temperature. 

### **Alternative hypothesis:** 
There is a relationship between the annual frequency of tornadoes and the US's annual average temperature.


# Process

## 1, Extract Data 
- find a data sources:
    - tornado data set found on Kaggle 
    - researched external data source that contained the average annual temperature in the US for roughly the same period of time as our data set
- load both data sources into pandas dataframes and merge the USA annual average temperature for each year. 

[Link - Joining)](https://github.com/Kanustu/LHL_midterm_project/blob/main/notebooks/1_joining.ipynb)

## 2. Clean Data 
- Cleaning steps performed:
     - renamed columns with more descriptive terms
     - droped extraneous, duplicated columns (month, day)
- Validate against source Data Dictionary
    - Kaggle data set was partially pre-cleaned, however when researching data, we found the original [source data and data dictionary](https://www.spc.noaa.gov/wcm/data/SPC_severe_database_description.pdf) which presented several potential cleaning tasks. Steps performed to connfirm whether our data set had addressed these issues or not. 
- Missing values:
    - Determine proportion of null values for all rows. Only two features contained missing values. 
        - Magnitude had .05% nulls, and so these records were removed. 
        - Property loss had nearly 40% nulls, so an alternative method of addressing these missing values would be required since removing 40% of the records could significantly affect the analysis quality. 
        - Preliminary EDA revealed that existing values of property loss showed significant proportion of outliers. 
        - mising values for propertly loss were filled with the median property loss value for that year 
        - QA:
            - new column added with complete values for all records,  
            - locating a median value for one year and locating the missing value record and confirmed the new value was correctly loaded
- Normalize Data
    - due to the wide range in possible numeric values for many features the data set was scaled between values 0-1 and exported into a seperate file to determine if the statistical model improves using scalled data.
- Export normalized clean data and clean data into two csv files


[Link - Cleaning Notebook)](https://github.com/Kanustu/LHL_midterm_project/blob/main/notebooks/2_cleaning.ipynb)

## 3. Exploratory Data Analysis (EDA)

- methodical process to EDA was adopted, EDA included:
    - getting summary statistics 
    - confirming the count of null records (which was 0 due to the cleaning steps performed, this step QA'd the cleaning done previously)
    - checking for duplicates. Duplicates were found in the ID feature, however the source data explains that each tornado is uniquely identified using an ID, but that one tornado may have multiple records if it crosses state/county borders
- Vizualizations: 
    - produced a variety of vizualizations using heatmaps, scatter plots, box plots, line charts, bar charts, histograms to get a sense of the data. 

[Link - EDA Notebook)](https://github.com/Kanustu/LHL_midterm_project/blob/main/notebooks/3_eda.ipynb)

## 4. Statistical Modelling

- Perform statistical modelling with limited scope and time permitting return and refine modelling. 
- chose to focus on total unique tornadoes per year and the annual average temperature. 
- used scalled data for the statistical model to control for the different scales each features.  
- the results of the statistical modelling are summarized in the **Results** section of this document. 


[Link - Statistical Modelling Notebook](https://github.com/Kanustu/LHL_midterm_project/blob/main/notebooks/4_modelling.ipynb)


## 5. Vizualise Data using Dashboards

- load clean data set into Tableau and create vizualizations. 
- vizualizations. 

[Link - Tableau Workbook](https://github.com/Kanustu/LHL_midterm_project/blob/main/notebooks/4_modelling.ipynb)


# Results

- tornadoes are a east cost midwest problem. West coast sees little tornadoes. 
- several times in the data where there was a significant increase in the frequency of tornadoes per year followed by a sizeable drop the following year. Especially 1974, 2008, and 2011 saw historically high degree of tornadoes and also occurred during a la nina year

Here are the results of the statistical modelling performed: 

* The adjusted R-quare value in the latest model was **0.186**. 
    * Meaning that 18.6% of the variance in the dependent variable (sum_tornadoes) can be explained by the independent variable (average annual US temperature). 
    * This is considered a fairly weak relationship, and the model's ability to accurately predict the number of tornadoes per year is poor.
* Despite the adjusted r-squared being relatively weak, annual US avg temperature is still statistically significant with a p-value of 0.000 in predicting total tornadoes per year. 
* The model's f-statistic has a low value of 0.000115 indicates there is sufficient evidence to reject the null hypothesis that there is no relationship between number of tornadoes per year and annual average us temperature. 
* Our teams original hypothesis that as global temperatures rise, as will the frequencyof tornadoes is supported by this model. 

# Challenges
- unclear expectations regarding collaboration on github meant much of upfront project time was spent trying to understand git rather than the project. 



# Future Goals
- Perform multivariate linear regression to find a stronger model.
- Population density from the 1950's to 2019 would more than likely be different in these locations which would effect fatalities and prop loss. 
- Investigate the seasonablity of significant increase followed by significant decrease the following year and it's relationship to the the el nino/la nina weather patterns. El nino/el nina's specifically effect the south, south/east regions of the u.s.. Perform classification model to determine the relationship with el nino/el nina and tornado frequency. 
