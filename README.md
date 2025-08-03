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
- **Power BI extends**: Multi-dimensional risk assessment, interactive patient profiling, AI-powered pattern recognition, and dynamic clinical dashboards

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
