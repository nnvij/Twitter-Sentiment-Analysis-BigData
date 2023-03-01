# Twitter-Sentiment-Analysis--BigData
## Introduction:
- Sentiment analysis is used to analyse text data inorder understand the underlying sentiment (positive or negavtive).
- Sentiment analysis uses  Natural language processing(NLP) and machine learning to determine emotional intent behind a communication.
- Twittershutdown, Riptwitter was trending when Elon Musk took charge and hundreds of twitter employees send in their resignations.
- This project will perform Sentiment anlaysis on tweets collected for hastags #Twittershutdown, #Riptwitter, #Elon Musk and so on.

## Problem Statement:
- Collect tweets using Twitter Api by launching an AWS EC2 instance, stream the tweets using Kinesis firehose and store the data in AWS S3 bucket.
- Create a binary classification model to classify sentiment of each tweet (positive or negative), label= sentiment(0>negative, 1>positive) .
- Create a Quicksight dashboard for the data collected and also predictions from the classification model.

### Tools used:
- AWS, Twitter Api, Amazon Kinesis firehose, Pyspark, Amazon Quicksight, Databricks

## Data
### Data Collection:
- 399333 tweets were collected using Twitter Api and stored in AWS S3
- Using Databricks environment connect to S3 bucket and mount the data by creating a spark session.
  ![image](https://user-images.githubusercontent.com/103464406/214683406-cce6feab-4d1a-4836-8726-f1199e3c15d9.png)
  ![image](https://user-images.githubusercontent.com/103464406/214683454-b3111e40-311e-4450-900a-d62c8a7671c9.png)


### Data preprocessing:
- Created a pyspark dataframe object twitter data.
- Checked for null values and drop rows with Null values.
- Converted create_at to datetime column.
- Used regular expression to clean the tweet, location columns. 
  ![image](https://user-images.githubusercontent.com/103464406/214684035-bba678e9-b194-4f0f-8267-7badd78e42d7.png).
- Textblob which is a library in python for text analysis can be used to assign sentiment for each tweet. 
- Created a  column Sentiment which will have values 0 if a tweet has nagative sentiment and 1 for positive sentiment.
- After cleaning we have 135,083 tweets out of which 45,760  tweets were with positive sentiment and 89,323 were tweets with negative sentiment.

## Model:
### Feature Engineering:
- Using library Tokenizer convert tweet column to lowercase and split it by white spaces, outputColumn="tokens"
- Remove stopwords from tokens using library StopWordsRemover,outputColumn="filtered" .
- Convert filtered tweets into matrix of token counts using CountVectorizer library,outputColumn="cv" .
- Inverse document frequency (IDF) library will check for relevant words in the tweet and remove sparse words, outputcolumn = "1gram_idf".
- Ngram (n=2) library is feature transformer that converts the input array of strings into an array of n-grams, outputcolumn= "2gram".
- HashingTF will map a sequence of terms to their term frequencies using the hashing trick, numFeatures=20000,outputcolumn= "2gram_tf".
- Again perform IDf to remove sparse terms, outputColumn="2gram_idf"
- VectorAssembler will  merges "1gram_idf", "2gram_tf" columns into a vector column="rawFeatures"
- ChiSqSelector will select  categorical features from rawFeatures, outputCol="features" and reduce the number of features to 16000

### Model Development and Evaluation:
- Data was split into 90% train and 10% test data.
- Sentiment column is the label. 0 > negative sentiment, 1> positive sentiment
- We tried RandomforestClassifier and Logisticregression models to classify if the tweet in the test data is positive or negative
- With RandomForestClassifer we acheived 66% accuracy and 72.87% Roc-Auc score
- Classification report for RandomForestClassifer as follows:
  ![image](https://user-images.githubusercontent.com/103464406/214699709-55a6af80-122c-43f2-b8fb-a2f1380b2d20.png)
- LogisticRegression gave us an accuracy score of 90.425 and Roc-Auc score of 92.83
- Classification report for LogisticRegression as follows:
    ![image](https://user-images.githubusercontent.com/103464406/214700094-46d76a87-3711-4069-92b8-0b03f28bf70e.png)

#### LogisticRegresssion model gave us better accuracy, the predictions are saved back to AWS S3 bucket

## QuickSight Dashboard
### Tweets post data preprocessing:
 - 66% of the tweets were with negative sentiment
 - Top 10 location in terms of number of tweet, location as a feature doesnot seem to be a contributor in tweet sentiment as they almost have equal percentage of both negative and positive tweets
  ![image](https://user-images.githubusercontent.com/103464406/214701168-8bf81ce5-3b17-429f-850a-f0d23c38ace7.png)
  ![image](https://user-images.githubusercontent.com/103464406/214701250-3d46aa48-c45e-469a-9fd1-84b292999de4.png)


### Predictions:
- from the 8.9K negative tweets, the model was able to correctly predict 8.19K tweets as tweets with negative sentiment.
  ![image](https://user-images.githubusercontent.com/103464406/214701322-038c7012-76af-4a82-a20f-a527059312d3.png)
  

