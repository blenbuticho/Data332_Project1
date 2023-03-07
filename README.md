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

  df_3 =df_2 %>%
  inner_join(lexicon) %>%
  group_by(word) %>%
  count(sentiment, sort = TRUE)
  
<img width="283" alt="Screen Shot 2023-03-07 at 12 24 13 AM" src="https://user-images.githubusercontent.com/118494123/223338688-d5937534-a979-448d-babf-7e4ffee9b0bd.png">

## Word count by the sentiment using NRC

      df_3%>%
        ggplot(aes(x=n, y=sentiment)) +
        geom_bar(stat="identity", fill="purple")+
        labs(x = "word count", y = "Sentiment")+
        geom_text(aes(label=NA), vjust=-0.3, size=3.5)+
        theme_minimal()

![NRC LEXICON](https://user-images.githubusercontent.com/118494123/223339419-320efa2f-8a64-41ce-9765-b96cd2dd970e.png)

## Word Count by Sentiment using the bing lexicon 

lexicon = get_sentiments("bing")

      df_3%>%
         ggplot(aes(x=n, y=sentiment)) +
         geom_bar(stat="identity", fill="green")+
         labs(x = "word count", y = "Sentiment")+
         geom_text(aes(label=NA), vjust=-0.3, size=3.5)+
         theme_minimal()

![Rplot](https://user-images.githubusercontent.com/118494123/223342482-f6f82723-0d5e-4746-955b-26a05453f28c.png)

# 3. Word Cloud 

      lexicon = get_sentiments("nrc")

      df_3 %>%
         inner_join(get_sentiments("bing")) %>%
         count(word, sentiment, sort = TRUE) %>%
         acast(word ~ sentiment, value.var = "n", fill = 0) %>%
         comparison.cloud(colors = c("purple", "blue"),
                   max.words = 100)
            
![Rplot01ks](https://user-images.githubusercontent.com/118494123/223343557-cbc05562-f60b-4907-90b3-1d79b9175b04.png)



