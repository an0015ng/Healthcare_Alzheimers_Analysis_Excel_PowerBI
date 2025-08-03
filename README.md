# Healthcare MRI & Alzheimers Analysis | Excel & Power BI

## Executive Summary
This project conducts an in-depth analysis of the OASIS-1 cross-sectional MRI dataset, encompassing **416 subjects aged 18 to 96**, to identify and visualize the key risk factors associated with Alzheimer's disease. The analysis reveals that individuals with a college degree or higher have a **35% lower prevalence of dementia** compared to those with only a high school education. Furthermore, neuroimaging data indicates that demented subjects exhibit an average **Normalized Whole Brain Volume (nWBV) that is 15% lower** than their non-demented counterparts within the same age group, highlighting significant brain atrophy as a key biomarker.


## Table of Contents
*   [Executive Summary](#executive-summary)
*   [Clinical Context & Project Workflow](#clinical-context--project-workflow)
*   [Dataset Overview](#dataset-overview)
*   [1. Foundational Analysis in Excel](#1-foundational-analysis-in-excel)
    *   [1.1. Data Quality and Validation](#11-data-quality-and-validation)
    *   [1.2. Feature Engineering & Data Preparation](#12-feature-engineering--data-preparation)
    *   [1.3. Foundational Insights with PivotTables & Charts](#13-foundational-insights-with-pivottables--charts)
*   [2. Interactive Deep-Dive in Power BI](#2-interactive-deep-dive-in-power-bi)
    *   [2.1. Data Transformation with Power Query](#21-data-transformation-with-power-query)
    *   [2.2. Advanced Analytics with DAX Measures](#22-advanced-analytics-with-dax-measures)
    *   [2.3. Interactive Dashboard Design & Visualization](#23-interactive-dashboard-design--visualization)
*   [Key Findings & Clinical Insights](#key-findings--clinical-insights)
*   [Skills Demonstrated](#skills-demonstrated)
*   [Project Files & Access](#project-files--access)
*   [Conclusion](#conclusion)

## Clinical Context & Project Workflow

Understanding neurological risk factors in Alzheimer's disease requires sophisticated analysis of both clinical and neuroimaging data. Healthcare professionals struggle with early identification of at-risk patients, optimal resource allocation for cognitive assessments, and evidence-based decision making for intervention strategies. This analysis transforms complex MRI and demographic data into actionable clinical insights for neurologists, healthcare administrators, and research teams.

### Integrated Analytical Approach
This project leverages **Excel for foundational data preparation** and **Power BI for advanced clinical analytics** - each tool applied where it delivers maximum analytical value:

- **Excel handles**: Data quality validation, feature engineering, demographic categorizations, and baseline statistical insights through PivotTables
- **Power BI extends**: Multi-dimensional risk assessment, interactive patient profiling, and dynamic clinical dashboards

**Workflow**: Raw OASIS Data → Excel Cleaning & Validation → Excel Clinical Logic → Power BI Interactive Risk Assessment → Clinical Recommendations

This integrated approach ensures robust data integrity while delivering clinician-ready visualizations for immediate diagnostic support and population health insights.

## Dataset Overview

**Source**: [Kaggle - MRI and Alzheimer's Dataset](https://www.kaggle.com/datasets/jboysen/mri-and-alzheimers/data)

Below is a screenshot of how the raw dataset looks like:

<img width="1618" height="412" alt="image" src="https://github.com/user-attachments/assets/3396449f-0c37-4269-9915-5b3a0c42a3bf" />

**Original Data Provider**: The [Open Access Series of Imaging Studies (OASIS)](http://www.oasis-brains.org/) - Washington University Alzheimer's Disease Research Center

**Key Statistics**: Cross-sectional collection spanning 78 years (ages 18-96) | 416 unique subjects | 100 clinically diagnosed Alzheimer's cases | Multi-dimensional neuroimaging measurements

This dataset represents real-world clinical research data from one of the most established neuroimaging repositories in Alzheimer's disease research:

**Clinical Hierarchy**: Demographics → Cognitive Assessments → Neuroimaging Biomarkers  
**Assessment Coverage**: MMSE cognitive scores, CDR dementia ratings, socioeconomic factors  
**Neuroimaging Metrics**: Brain volume measurements (eTIV, nWBV), atlas scaling factors (ASF)  
**Key Features**: All subjects are right-handed, balanced gender distribution, comprehensive age spectrum from young adults to elderly

# 1. Foundational Analysis in Excel

With a clean understanding of the dataset structure and research objectives, the foundational analysis began in Excel to establish baseline insights and prepare the data for advanced analytics. This phase focused on ensuring data integrity, engineering meaningful features, and creating initial visualizations to understand the core relationships within the OASIS dataset.

## 1.1. Data Quality and Validation

Before conducting any analysis, comprehensive data quality validation was performed to ensure reliable insights. This audit covered duplicate detection, data formatting standardization, missing value investigation, and column utility assessment.

### a. Remove Duplicates in Excel

**Initial Duplicate Assessment**: Verified data integrity by checking for duplicate subject entries that could skew analysis results.

I used Excel's built-in duplicate detection by clicking **Data** → **Remove Duplicates** and selecting all columns to ensure no duplicate subjects existed in the dataset:

<img width="1818" height="806" alt="image" src="https://github.com/user-attachments/assets/d2ccb54a-3105-46fa-a830-0dc3c1de4822" />

After clicking OK:

<img width="1728" height="662" alt="image" src="https://github.com/user-attachments/assets/4010d553-faa9-4956-8c56-86e805dc572d" />

The process confirmed that each row represented a unique subject visit, maintaining data integrity for subsequent analysis.

### b. Standardize Data Format

**Data Type Optimization**: The imported dataset showed all columns formatted as 'General' type, including numerical measurements that needed proper formatting for calculations and charting:

<img width="1572" height="782" alt="image" src="https://github.com/user-attachments/assets/b77f5ed9-5304-4311-9172-49d6268fb5d6" />

The data types of all columns were "General", even the ones with decimals. I changed those to "Number" with consistent decimal places by selecting a numerical column (i.e. nWBV) and formatting it as Number type with 3 decimal places. 

<img width="1572" height="782" alt="image" src="https://github.com/user-attachments/assets/482e8a40-756e-498b-8ffd-70752fc1034b" />

This is useful for the data type to be continuous so it is better for analysis and charting. I repeated this process for all the numerical columns (eTIV, ASF, MMSE, etc.) to ensure consistency across the dataset.

### c. Check for Missing/NULL Values

**Missing Data Investigation**: A systematic examination revealed patterns in missing clinical data that required strategic decision-making.

I found out that for some rows, these 4 columns of data are missing: **Educ, SES, MMSE, CDR** while other data are present (neuroimaging measurements like eTIV, nWBV, ASF):

<img width="1826" height="776" alt="image" src="https://github.com/user-attachments/assets/e8158fbe-7fc8-4cd7-9bac-5f800992e13b" />

I wanted to check why it happens, so I did some sorting and filtering, and finally found out that if the subject is young, it typically doesn't have those clinical assessment data. I sorted by age to see if this pattern was true:

<img width="1784" height="720" alt="image" src="https://github.com/user-attachments/assets/37336bff-5d6a-401c-b31c-571ee43442a7" />

I further confirmed this by drawing a chart with Age at x-axis, and one of the missing columns (I took Educ) as y-axis:

<img width="1122" height="692" alt="image" src="https://github.com/user-attachments/assets/f69e838e-63c6-4850-ae68-2dff423cbf12" />

Now this is not the final chart for the analysis but one can very easily see that subjects with age <40 typically do not have clinical assessment data available.

**Strategic Decision**: Yet, there are complete data for **eTIV, nWBV & ASF** even for young subjects. So, instead of deleting the rows altogether, I decided to keep those rows with empty values as they still provide valuable neuroimaging information that might be useful for brain volume analysis across the full age spectrum.

### d. Check for Redundant Columns

**Column Utility Assessment**: Identified columns that provided no analytical value for the research objectives.

In this dataset, everybody is right-handed:

<img width="512" height="622" alt="image" src="https://github.com/user-attachments/assets/4789041b-230c-4739-8d7b-78d26480f760" />

Therefore, I removed the 'Hand' column as it contained only a single value ('R') across all subjects and offered no discriminatory power for analysis.

## 1.2. Feature Engineering & Data Preparation

With clean data established, the next critical step involved creating analytical columns that would enable meaningful insights and support the planned PivotTable analysis.

### a. ID Column Restructuring

**Problem**: The original ID column had a complex format 'OAS1_0001_MR1', where 'OAS1' represents this current cross-sectional dataset, '0001' is the actual subject ID, and 'MR1' refers to the first visit. There are 'MR2' entries for some subjects indicating second visits. For analysis purposes, it's better to separate the ID itself and track visit numbers independently.

**Solution**: To get the short ID, I used the formula:

```excel
=TEXTBEFORE(TEXTAFTER(A2,""),"")
```

First, `TEXTAFTER(A2,"_")` extracts the text after the first underscore, resulting in "0001_MR1". Then, `TEXTBEFORE` from that result gives us just "0001". Perfect.

To get the Visit Number, I used the formula:

```excel
=SUBSTITUTE(TEXTAFTER(A2,"_",-1),"MR","")
```

First, `TEXTAFTER(A2,"_",-1)` searches from the end (indicated by '-1'), extracting "MR1". Then, `SUBSTITUTE` replaces "MR" with blank, resulting in just the number "1".

Below is the output:

<img width="1094" height="724" alt="image" src="https://github.com/user-attachments/assets/dd956a9e-8a14-462c-8ad6-7a0c163df6f7" />

This approach created clean, separate columns for analytical purposes while preserving the original data structure:

### b. Gender Column Enhancement

**Standardization Issue**: Having M/F abbreviations in the Gender column might be misleading for visualization and reporting purposes.

I renamed the column header to "Gender" for clarity and used Excel's **Find & Replace** function to convert "M" to "Male" and "F" to "Female":

<img width="1172" height="778" alt="image" src="https://github.com/user-attachments/assets/51040056-e97a-47b2-9351-7ee82daab3d8" />

Also, I made sure to select "Match case" during the replacement to ensure other cells weren't affected (preventing issues like "MR1" becoming "MaleR1").

### c. Age Group Creation

**Clinical Rationale**: Since Alzheimer's disease occurs more frequently during older age, I created age groups with finer granularity for older subjects while keeping broader categories for younger adults.

I created a strategic age grouping: 2 broad groups for younger subjects (18-40, then 41-60), but 5-year intervals starting from 61 for more precise analysis of the elderly population where dementia risk increases significantly.

In a new 'age_table' sheet, I created a lookup table with age ranges and their corresponding group labels:

<img width="590" height="740" alt="image" src="https://github.com/user-attachments/assets/a0800324-42db-4d5b-b041-e389c2e69f4b" />

Then I added a new "Age_Group" column in the main sheet, using `XLOOKUP` to categorize ages based on the lookup table:

```excel
=XLOOKUP(C2,Table1[Age_Min],Table1[Age_Group],,-1,1)
```

The match_mode parameter '-1' refers to 'Exact match or next smaller item'. This is perfect because I used 'Age_Min' in the age_table. For example, if a subject's age is 74, there isn't an exact match, so it looks for the next smaller item which is 71, and returns the Age_Group "71-75".

This is the final output:

<img width="922" height="716" alt="image" src="https://github.com/user-attachments/assets/e1574664-577d-4ae3-a49c-e051701ee3b1" />

### d. Education Level Descriptive Labels

**Enhancement Purpose**: The numerical Educ codes (1-5) needed descriptive labels for better interpretation and visualization.

Based on the OASIS documentation:
- 1: Less than high school graduate
- 2: High school graduate  
- 3: Some college
- 4: College graduate
- 5: Beyond college

I created a new column using the `SWITCH` formula:

```excel
=SWITCH([@Educ], 1,"Less than High School", 2,"High School Graduate", 3,"Some College", 4,"College Graduate", 5,"Post Graduate", "Unknown")
```
A new column is created as shown below:

<img width="1392" height="594" alt="image" src="https://github.com/user-attachments/assets/3ea8954a-093a-4760-8be9-bee8fb4b9af1" />

### e. CDR Status Binary Classification

**Clinical Significance**: CDR (Clinical Dementia Rating) is a critical metric to determine if a person is demented or not. Any CDR values above 0 indicate some level of dementia.

I created a new column "CDR_Status" with a simple classification formula:

```excel
=IFS([@CDR]="", "Unknown", [@CDR]>0, "Demented", [@CDR]=0, "Non-demented")
```

This classification enables clear comparative analysis between demented and healthy populations while filtering out the unknowns across all other variables in the dataset:

<img width="1172" height="860" alt="image" src="https://github.com/user-attachments/assets/d0def450-d508-4341-a092-9c0aabd24fd2" />

Finally, I converted this dataset into a table named `Table2`, useful for analysis moving forward:

<img width="1429" height="566" alt="image" src="https://github.com/user-attachments/assets/ef7b571e-d870-4d0d-94e6-69a3c0cda863" />

## 1.3. Foundational Insights with PivotTables & Charts

With clean, well-structured data established, I moved to creating foundational analytical insights using Excel's PivotTable functionality. This phase focused on establishing the core relationships within the OASIS dataset through four key analyses, each designed to build understanding from basic demographic patterns to more complex clinical relationships.

### a. PivotTable: Demographic & Dementia Overview

**Purpose**: To set the scene by revealing the prevalence of dementia across different age groups and establish the fundamental age-dementia relationship in the dataset.

**PivotTable Setup**:
- **Rows**: Age_Group (custom categories: 18-40, 41-60, 61-65, 66-70, 71-75, 76-80, 81-85, 86-90, 91-95, 96-100)
- **Columns**: CDR_Status (Demented, Non-Demented, Unknown)
- **Values**: Count of Subject ID

I created a PivotTable to aggregate the count of subjects by their dementia status (`CDR_Status`) and age group. The resulting data was then visualized using a 100% stacked column chart to clearly illustrate the rising proportion of demented individuals in older age groups.

<img width="2216" height="504" alt="image" src="https://github.com/user-attachments/assets/f5ed0362-b492-4094-9a48-6035521e1a37" />

**Analysis & Insights**: 

The chart immediately highlights two key characteristics of the dataset. First, for subjects under the age of 60, the data is dominated by 'Non-Demented' and 'Unknown' statuses. The high proportion of 'Unknowns' in the youngest age groups directly reflects the finding from the data validation phase: these younger individuals were often included as healthy controls without undergoing the full clinical dementia assessment. This context is crucial as it focuses the core of the dementia analysis on the older population segments.

Secondly, for the older population where clinical data is complete, the percentage of demented subjects grows dramatically from the 61-65 age group at approximately 30% to a peak of nearly 70% in the 76-80 age group. However, an interesting pattern emerges in the oldest age groups where the dementia percentage appears to decline—dropping from the peak of 70% to around 40% in the 91-95 age group.

This decline in older age groups requires careful interpretation due to **sample size considerations**. The total number of subjects decreases significantly as age increases, making these percentages less statistically reliable. For instance, while the 71-75 age group contains 52 subjects, the 91-95 group has only 5 subjects, making the 40% dementia rate based on just 2 individuals.

More importantly, this pattern may reflect **survivor bias**—a well-documented phenomenon in aging research where individuals who survive to very advanced ages may represent a particularly resilient subset of the population. Those who develop significant health problems, including dementia, may have higher mortality rates and thus be underrepresented in the oldest age categories. This suggests that the subjects reaching ages beyond 85-90 might represent the "healthiest survivors" who were resilient enough to avoid both dementia and other life-threatening conditions.

This initial demographic overview immediately confirms that age is the primary risk factor in this dataset and directs subsequent analysis toward understanding what additional factors might influence dementia risk within these age-stratified populations.











