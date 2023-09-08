# Machine_Learning_Project

### Topic: Forecasting Tesla Stock Prices with Sentimental Analysis of Elon Musk-Related Social Media Information

* The project was conducted in November 2022
-------------------------------------------------------------------------------
### 1. Background
- To verify the hypothesis that Elon Musk's social activity has any impact on Tesla's stock price and, if any, how much impact it has 
- To forecast Tesla stock prices using social data based on the upper hypothesis

### 2. Data
- Elon Musk's tweet sentiment data from Kaggle
  * The sentiment data classified by using RoBERTa natural language analysis model.
  * The data is from June 4, 2010, when Elon Musk first started Twitter, to November 10, 2022.
- Tesla Stock Price data
  * Using Yahoo Finance API
  * The data is from the date of Tesla listing(June 29, 2010) to the latest date of sentimental data secured(November 10, 2022).
  * Scaled with Min-Max Normalization

### 3. Data Pre-processing
   #### 1) Feature Selection
   - Among 18 columns of the Twitter sentimental data, there are five columns selected as ["Date", "reply count", "retweet count", "likecount", "senetiment"]
  
   #### 2) Feature Definition
   - How to define the 'sentimental' feature, which is defined by three categorical values: 'positive', 'negative', and 'neutral'

      ###### 2-1) Scenario 1
      - Numerical value = positive +1 / negative -1 / neutral 0
        </br>: Under the assumption that positive comments will have a positive effect on stock prices and other values are defined for the same reason

      - weight = each commitment / total commitment
        </br>: Newly designed value
        </br>: Due to not only one sentiment in one date but also several sentiments
        
      - commitment = retweet count + likecount
      - Sentimental Feature = numerical value * weight
       
      
      ###### 2-2) Scenario 2
     - Numerical value = positive +2 / negative 0 / neutral 1
     - Set the most sentiment value as the main value by each date
     - Make mean with the sentiment values which has the same max value
       
  #### 3) Input/Output
  - y value: the recent n-year period data which is relatively more active than in the 2010s

### 4. Model Selection
  #### 1) Linear Regression
  - Based on the rvalue of the previous scenarios, it is difficult to find a correlation between 'sentiment' feature as the only one feature in stock price prediction
  #### 2) LSTM + Sentiment
  - Parameters
    * Windows = 60
    * epochs = 200
    * batch_size = 20
  - Created based on the hypothesis that if stock prices with intrinsic elements are implemented using sentimental data and LSTML models, performance can be improved.

### 5. Results
- It was confirmed that the performance of LSTM with sentimental data was less than that of general LSTM model



