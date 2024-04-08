# Data_Warehouse
# Marketing Campaign Evaluation Project

## Table of Contents

- [Introduction](#introduction)
- [Data Model](#data-model)
- [Feasibility Queries](#feasibility-queries)
- [Evaluation of Marketing Campaigns](#evaluation-of-marketing-campaigns)
  - [Business Process Description](#business-process-description)
  - [Typical Questions](#typical-questions)
  - [Data Sources](#data-sources)

## Introduction

This repository contains documentation for a project focused on evaluating marketing campaigns conducted by Beauty Haven. The project involves analyzing various metrics related to social media engagement, sales, and store traffic to assess the effectiveness of different marketing strategies.

## Data Model

### Fact Table: Store_monitoring

- **SK_DateID**: Numeric (Foreign Key to Dim_Date) - Date of monitoring
- **SK_CampaignID**: Numeric (Foreign Key to Dim_Campaign) - Campaign conducted
- **SK_LocalisationID**: Numeric (Foreign Key to Dim_Localisation) - Localisation of a store that is monitored
- **SK_Store**: Numeric (Foreign Key to Dim_Store) - Store which is monitored
- **TrafficRatio**: Numeric - Traffic ratio, calculated as current traffic in comparison to base year traffic
- **SalesRatio**: Numeric - Sales ratio, calculated as current sales in comparison to base year sales

### Dimension Tables:

1. **Dim_Date**:
   - **SK_Date_ID**: Numeric (Primary Key) - Date ID
   - **Date**: Date - Date
   - **Year**: 4 digits - Year
   - **Month**: Numeric - Month’s numeric value
   - **Day**: 2 digits - Day

2. **Dim_Campaign**:
   - **SK_CampaignID**: Numeric (Primary Key) - Campaign ID
   - **Company**: Varchar(3) - Company which conducted specific marketing campaign
   - **Platform**: Varchar(20) - Name of the platform where the marketing campaign was conducted (e.g., TikTok, Instagram)
   - **Cost**: Varchar(20) - Cost of the marketing campaign in PLN
   - **Cost_category**: Varchar(20) - Cost category (allowed values: small, medium, big, huge)

3. **Dim_SME**:
   - **SK_EngagementID**: Numeric (Primary Key) - Engagement ID
   - **SMETotal**: Varchar(20) - SME category (allowed values: small, medium, big, huge)
   - **Views**: Varchar(20) - Number of views
   - **Followers**: Varchar(20) - Number of gained followers
   - **Likes**: Varchar(20) - Number of likes
   - **Comments**: Varchar(20) - Number of comments

4. **Dim_Localisation**:
   - **LocalisationID**: Numeric (Primary Key) - Localisation ID
   - **Inhabitants**: Varchar(20) - Number of people living at specific localisation
   - **Inhabitants_category**: Varchar(20) - Inhabitants category (allowed values: small, medium, big)

5. **Dim_Store**:
   - **SK_Store**: Numeric (Primary Key) - Store ID
   - **BK_StoreID**: Numeric - BK
   - **Activeness**: Varchar(20) - Active if information is current, otherwise inactive (SCD2 implementation)
   - **Size**: Varchar(20) - Size categories (allowed values: small, medium, big)

### Dimensional Model Fact Definitions

- **Fact 1: Store monitoring fact**:
  - Granularity: a specified submission for a specific date, store, localisation, marketing campaign, and social media engagement
  - Measures: Number of store monitoring facts, TrafficRatio sum, Average TrafficRatio, SalesRatio sum, Average SalesRatio

## Feasibility Queries

Feasibility queries based on the multidimensional model for evaluating marketing campaigns include:

1. Compare TrafficRatio over the years.
2. Compare SalesRatio over the years.
3. Compare the average sales ratio and traffic ratio from a certain month and year to the SMETotal.
4. Examine the relationship between average monthly traffic volume and the size of the stores.
5. Determine which social media platform generates the biggest sales ratio and traffic ratio at a specific year.
6. Identify the company providing marketing campaigns that create the biggest traffic ratio at a specific year.
7. Explore the relationship between the cost of marketing campaigns and the SalesRatio.

## Evaluation of Marketing Campaigns

### Business Process Description

The evaluation process of marketing campaigns involves extracting data about every post and video included in a specific campaign. This data includes metrics such as likes, comments, views, and the number of new followers gained. The evaluation takes place after the campaign finishes, where Beauty Haven identifies the most successful campaign based on the accumulated likes, views, and comments.

### Typical Questions

Typical questions in evaluating marketing campaigns include:

1. How many likes, comments, views, and new followers were generated by a campaign after a specific duration?
2. On which platform (TikTok or Instagram) did a campaign generate the highest number of views?
3. How does sales change before and after the start of a campaign?
4. Is store traffic affected by a specific marketing campaign?

### Data Sources

Data sources for the evaluation of marketing campaigns include:

- Beauty Days database: Contains information about daily store activities, sales, traffic, localisation, and basic store data.
- Excel file: Contains data about companies conducting marketing campaigns, including company IDs and names.
