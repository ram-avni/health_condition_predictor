# health_condition_predictor

In this project I built a model to predict whether a person has asthma, using data records from the CDC National Health And Nutrition Examination Survey. These surveys are frequently used to provide national estimates on a wide range of major public health issues. I combined features from various surveys, and ran the model to test for this particular health condition (asthma). I found great interest in the CDC website because it contains many other datasets that can be used to predict other conditions as well, so this project was a way to get famiiliar with a very useful and practical source which data scientists use nationally.

* [Data](#data)
  * [Source](#source)
* [Features](#features)
  * [EDA and Feature Engineering](#eda)
  * [Hand Crafted Features](#byhand)
  * [Features from Libraries](#fromlibraries)
* [Modeling](#modeling)
  * [Choosing the Model](#choosingthemodel)
  * [Interpretation of Feature Importance](#featureimportance)
* [Closing Thoughts](#closing)
* [Next Steps](#nextsteps)

## Data <a name="data"></a>
### Source <a name="source"></a>
The CDC's National Health And Nutrition Examination Survey (NHANES) contains annual questionnaires, which in turn contain multiple datasets, including:
- Demographics Data
- Dietary Data
- Examination Data
- Laboratory Data 
- Questionnaire Data
- Medical Conditions
- Limited Access Data

I used the annual questionnaires from 2015-2016 (which is the latest available dataset as of October 2019 due to the rigorous procedure of the CDC data collection and statistical methods).
The target variable is: “Still having asthma”, classified as 1, is a Positive (2 means never was diagnosed with asthma or no longer with asthma).

Starting with about 10,000 observations (different individuals), I reduced the size to about 8,000 observations after cleaning and merging datasets.

Most features were taken from:
- Medical:
  - Diagnosed with asthma
  - Age when first had asthma
  - Family history / genetics
- Demographics:
  - Household size
  - Family income to poverty ratio
- Dietary:
  - Essential nutrients and vitamins

Of these two categories, there was a roughly 70/30 split between NAH and NTA, as seen below in the pie chart of class distribution.

![pie chart of class distribution](https://github.com/h-parker/AITA_classifier/blob/master/Images/class_dist.png)

### Features <a name="features"></a>

## EDA & Feature Engineering <a name="eda"></a>
### Hand Crafted Features  <a name="byhand"></a>
We started by putting together several features that seemed naturally like they could be indicative of a person being a jerk, and those features were
- Number of:
 - !
 - ?


### Features from Libraries  <a name="fromlibraries"></a>
Then we turned to Python libraries!
#### Semantic Analysis
Not knowing what would give us the best results, we tried semantic analysis of title and description using TextBlob, VADER, and Afinn.
- TextBlob - we made features from title and description polarity and subjectivity, and the difference between the polarity of the title and description, and between the subjectivity of the title and description.
- VADER - VADER was more straightforward; we made features from the compound VADER scores for the title, description, and the 

We looked jerk -- maybe they would pose their question innocently, then have a much different attitude in the description. 

#### TF-IDF, LSA, and LDA
Finally, we loon fell under. After that, we had about 2300 words, which was far too many words to stop there.

We first tried latent semanr each submission, and that became our topic feature. 
**We realized that we needed to one-hot encode the topics! We will go back and change this!**

## Modeling <a name="modeling"></a>
After using SMOTE to account for class imbalance in our data (using the imblearn library), we dove into modeling.
### Choosing the Model <a name="choosingthemodel"></a>
We initially considered r improvement -- unfortunately, no model had a false negative rate lower than 50%!
![final model confusion matrix ](https://github.com/h-parker/AITA_classifier/blob/master/Images/rf_cm.png)

### Interpretation of Feature Importance  <a name="featureimportance"></a>
From the feature importance graph (shown below), the top 5 most important features were curse count, quote count, Afinn title sentiment, question count
![feature importance](https://github.com/h-parker/AITA_classifier/blob/master/Images/rf_feature_importance.png)


## Closing Thoughts <a name="closing"></a>
This project is not done and over with

## Next Steps <a name="nextsteps"></a>
Moving forward, we definitely have a few things we'd really like to do:
1. Create more visualizations, like wordclouds for the words in NTA vs TA submissions and for the topics created by LDA

