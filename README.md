# Data332_Project No.1
# Blen Buticho

![sentiment analysis (1)](https://user-images.githubusercontent.com/118494123/223373760-330bd6dd-5e84-4783-84ed-4acc32e6a418.jpeg)

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

   1. I created a grpah to show the number of times cerrtain words occured and what their sentiments looked like. based of that i conducted an analysis
   2. Eight fundamental emotions (angry, fear, anticipation, trust, surprise, sadness, joy, and disgust) and two sentiments are listed in the NRC Emotion 
      Lexicon (negative and positive).
   3. In this graph we can see joy was the highest emotion recorded while digust and suprise were the two lowest emotions recorded from this Data 
   4. Positive sentiments outweighed negative showing there were more postive thoughts in the customers feedabck 

## Word Count by Sentiment using the bing lexicon 

lexicon = get_sentiments("bing")

      df_3%>%
         ggplot(aes(x=n, y=sentiment)) +
         geom_bar(stat="identity", fill="green")+
         labs(x = "word count", y = "Sentiment")+
         geom_text(aes(label=NA), vjust=-0.3, size=3.5)+
         theme_minimal()

![Rplot01sjcej](https://user-images.githubusercontent.com/118494123/223344090-9dabaf79-0a8f-47ed-a9c4-0727aeff20d7.png)

   1. Bing lexicon being. binary lexicon, it only displays two variables which are negative and positive
   2. it this anlysis done from the Problems that customers experienced which were issues there were twenty four words that displayed negative or positive.
   3. Because this was based on issues, which typically is negative feedback, the negative sentiment outweighs the positive.
   4. Negative sentiments like Improper, fraud, false etc. had their counts added to sum over 200,000. While the likes convinence, promise and protetction
      were under positive adding up to less than 25,000
      


# 3. Word Cloud 

      lexicon = get_sentiments("nrc")

      df_3 %>%
         inner_join(get_sentiments("bing")) %>%
         count(word, sentiment, sort = TRUE) %>%
         acast(word ~ sentiment, value.var = "n", fill = 0) %>%
         comparison.cloud(colors = c("purple", "blue"),
                   max.words = 100)
               
![Rplot01ks](https://user-images.githubusercontent.com/118494123/223343557-cbc05562-f60b-4907-90b3-1d79b9175b04.png)

   1. A word cloud is a group or collection of words that are displayed in various sizes. 
   2. The more pronounced and bold a word is, the more frequently it has been used.
   3. This word cloud will enable us to more clearly see when customers' general sentiments were

# 4. Shiny App 

      column_names<-colnames(df_2) #for input selections
      ui<-fluidPage( 

      titlePanel(title = " Customer Complaints"),

      fluidRow(
      column(2,
       selectInput('X', 'Choose X',column_names,column_names[4]),
       selectInput('Y', 'Choose Y',column_names,column_names[2])
      ),
      column(4,plotOutput('plot_01')),
      column(6,DT::dataTableOutput("table_01", width = "100%"))
      )
      )

      server<-function(input,output){
  
      output$plot_01 <- renderPlot({
    ggplot(df_2,aes_string(x=input$X, y=input$Y, colour=Input$Splitby))+
      geom_smooth()
      }

      shinyApp(ui=ui, server=server)
 
# 5. Conclusion 

1. In conclusion, 10 emotions and 2 sentiments were used to analyze the given data. 
2. Using the a binary lexicon, i have found out that customers had major disputes.
3. Overall when customers provided their issues, the have had negative sentimnets. This shows that customers weren't satisfied and needed response from the companies


