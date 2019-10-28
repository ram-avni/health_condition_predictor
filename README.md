# health_condition_predictor

In this project I built a model to predict whether a person has asthma, using data records from the CDC National Health And Nutrition Examination Survey. These surveys are frequently used to provide national estimates on a wide range of major public health issues. I combined features from various surveys, and ran the model to test for this particular health condition (asthma). I found great interest in the CDC website because it contains many other datasets that can be used to predict other conditions as well, so this project was a way to get famiiliar with a very useful and practical source which data scientists use nationally.

* [Data](#data)
  * [Source](#source)
* [Features](#features)
  * [EDA and Feature Engineering](#eda)
* [Modeling](#modeling)
  * [Choosing the Model](#choosingthemodel)
  * [Interpretation of Feature Importance](#featureimportance)
* [Closing Thoughts and Next Steps](#closing)


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

Of the two categories, people with asthma account for less than 10% of the population, as seen below in the pie chart of class distribution.

![pie chart of class distribution](https://github.com/ram-avni/health_condition_predictor/blob/master/visuals/1_class_dist.png)

## Features <a name="features"></a>

### EDA & Feature Engineering <a name="eda"></a>
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
  
  I removed some features whose distribution revealed no impact on the prediction, like gender, as can be seen in the diagram below:
  ![Gender distribution ](https://github.com/ram-avni/health_condition_predictor/blob/master/visuals/3_gender_dist.png)

On the other hand, some features clearly had significant impact, such as family history and hereditary as well as age:

![Distribution of condition in family ](https://github.com/ram-avni/health_condition_predictor/blob/master/visuals/2_family_dist.png)
![Features - close relative with same condition  ](https://github.com/ram-avni/health_condition_predictor/blob/master/visuals/8_feat_hereditary.png)
![Features - age ](https://github.com/ram-avni/health_condition_predictor/blob/master/visuals/7_feat_age.png)


## Modeling <a name="modeling"></a>
After using SMOTE to account for class imbalance in the data (using the imblearn library), I ran a base model with Random Forest, and then finetuned a number of other models (using GridSearch). As shown in the table below, the best models were Naive Bayes and SVC.
![Model comparison ](https://github.com/ram-avni/health_condition_predictor/blob/master/visuals/4_model_comp.png)

### Choosing the Model <a name="choosingthemodel"></a>
Naive Bayes and SVC were the best models since the most desirable outcome is detecting the health condition as early as possible. The most NOT desirable - failing to detect the health condition (represented by number of FN). These models had high recall rate, however the tradeoff is notifying people without the condition that they may have it (represented by number of FP). Therefore, even though we minimize FN, the tradeoff (FPs) is quite large - about 70% of the TP cases.
![final model Confusion Matrix and ROC ](https://github.com/ram-avni/health_condition_predictor/blob/master/visuals/5_cm_roc.png)


### Interpretation of Feature Importance  <a name="featureimportance"></a>
From the feature importance graph (shown below), we can see that the family history (hereditary factor) and age are indeed crucial in making the right prediction.
![feature importance](https://github.com/ram-avni/health_condition_predictor/blob/master/visuals/6_feat_import.png)


## Closing Thoughts and Next Steps <a name="closing"></a>
This project was a great exercise in modeling and studying large, nationally important datasets. The CDC publishes detailed guidelines for professional statiticians and medical researchers, and it would be very interesting to cover the followint guidlines:
- Weighting: when and how to construct weights when combining survey cycles, and how to correctly create subsets within your analysis population.
- Descriptive statistics: checking frequency distribution and normality, generating percentiles, generating means, and generating proportions.
- Hypothesis testing: using t-test and chi-square statistics to test statistical hypotheses about population parameters.
- Logistic regression: to assess the likelihood of a disease or health condition as a function of a risk factor.
