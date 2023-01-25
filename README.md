# Twitter-Sentiment-Analysis--BigData
## Introduction:
- Sentiment analysis is used to analyse text data inorder understand the underlying sentiment (positive or negavtive).
- Sentiment analysis uses  Natural language processing(NLP) and machine learning to determine emotional intent behind a communication.
- Twittershutdown, Riptwitter was trending when Elon Musk took charge and hundreds of twitter employees send in their resignations.
- Perform sentiment nalaysis on tweets collected for hastags #Twittershutdown, #Riptwitter, Elon Musk.

## Problem Statement:
- Collect tweets using Twitter Api by launching an AWS EC2 instance, stream the tweets using Kinesis firehose and store the data in AWS S3 bucket.
- Built a classification model to classify sentiment of each tweet.
- Build a Quicksight dashboard for the data collected and also predictions from the classification model.

### Tools used:
- AWS,Twitter Api, Amazon Kinesis firehose,Pyspark,Amazon Quicksight, Databricks

## Data
### Data Collection:
- 399333 tweets were collected using twitter Api and stored in AWS S3
- using Databricks environment connect to S3 bucket and mount the data by creating a spark session.
- ![image](https://user-images.githubusercontent.com/103464406/214683406-cce6feab-4d1a-4836-8726-f1199e3c15d9.png)
![image](https://user-images.githubusercontent.com/103464406/214683454-b3111e40-311e-4450-900a-d62c8a7671c9.png)


### Data preprocessing:
- Creating pyspark dataframe object twitter data
- Drop Null values 
