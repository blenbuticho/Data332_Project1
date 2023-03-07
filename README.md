# Data332_Project No.1
# Blen Buticho

## Overview
This data is a compilation of grievances filed against companies regarding their consumer financial services and goods. The dataset includes customer complaints about financial products and demonstrates how to group text from customer complaints into the following categories: Consumer loans, mortgages, credit cards, credit reporting, student loans, bank accounts or services, payday loans, money transfers, other financial services, and prepaid cards are all examples of debt collection terms.


## Data Dictionary 

   1. Complaint ID: This number is used to identify the individuals who have filed complaints against the company. 
   2. Company: The Companies that received complaints. 
   3. Product: categorized the text of customer complaints. 
   4. Issue: Problems that customers experienced 
   5. Company response to customer: How the listed companies handled customer complaints

## 1. Cleaning the data
    df= read.csv("Consumer_Complaints.csv")
    saveRDS(df,"Consumer_Complaints.rds")
    df=readRDS("Consumer_Complaints.rds")

The downloaded files were CSV files, so they had to be converted into RDS because they include a lot of data and performance is essential when starting a project with a lot of data.

## Sentimental Analysis 

    nrc= tidytext::get_sentiments("nrc")
NRC Sentiment is used to conduct analysis for the first one. This is done by installing Nrc lexicon in R.


