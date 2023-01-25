# Twitter-Sentiment-Analysis--BigData
## Introduction:
- Sentiment analysis is used to analyse text data inorder understand the underlying sentiment (positive or negavtive).
- Sentiment analysis uses  Natural language processing(NLP) and machine learning to determine emotional intent behind a communication.
- Twittershutdown, Riptwitter was trending when Elon Musk took charge and hundreds of twitter employees send in their resignations.
- Perform sentiment nalaysis on tweets collected for hastags #Twittershutdown, #Riptwitter, Elon Musk.

## Problem Statement:
- Collect tweets using Twitter Api by launching an AWS EC2 instance, stream the tweets using Kinesis firehose and store the data in AWS S3 bucket.
- Built a binary classification model to classify sentiment of each tweet (positive or negative) .
- Build a Quicksight dashboard for the data collected and also predictions from the classification model.

### Tools used:
- AWS,Twitter Api, Amazon Kinesis firehose,Pyspark,Amazon Quicksight, Databricks

## Data
### Data Collection:
- 399333 tweets were collected using twitter Api and stored in AWS S3
- using Databricks environment connect to S3 bucket and mount the data by creating a spark session.
  ![image](https://user-images.githubusercontent.com/103464406/214683406-cce6feab-4d1a-4836-8726-f1199e3c15d9.png)
  ![image](https://user-images.githubusercontent.com/103464406/214683454-b3111e40-311e-4450-900a-d62c8a7671c9.png)


### Data preprocessing:
- Creating pyspark dataframe object twitter data.
- Check for null values and dropping rows with Null values.
- Convert create_at to datetime column.
- Using regular expression to clean the tweet, location columns. 
  ![image](https://user-images.githubusercontent.com/103464406/214684035-bba678e9-b194-4f0f-8267-7badd78e42d7.png).
- Textblob which is a library in python for text analysis can be used to assign sentiment for each tweet. 
- Create a  column Sentiment which will have values 0 if a tweet has nagative sentiment and 1 for positive sentiment.
- After cleaning we have 135,083 tweets out of which 45760 were tweets with positive sentiment and 89323 were tweets with negative sentiment.

## Model Development:
### Feature Engineering:
- tokenizer library to 
