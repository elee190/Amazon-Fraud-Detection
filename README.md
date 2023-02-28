# Amazon Fraud Detection Case Study

_By Edward Lee_

Amazon is a very large online retailing platform and has become increasingly important to the sales and distribution plans of brands in various categories. However, since Amazon is a platform that allows third-party selling, brands are subject to risks of counterfeiting or grey market selling. These activities are illegal, and frowned upon, and it is goes without question that any company, nonetheless Amazon, would seek to identify and limit their occurrence.
The top questions we are seeking to answer are:

1) To what extent is a given product in a given sector susceptible to the risk of counterfeiting and grey market selling?
2) What factors increase the risk of becoming a target of grey market sellers?


This Deliverable Includes:

-   A set of Jupyter notebooks and executable scripts that output probabilities of grey market activity
-   Training and testing datasets (upon execution of notebooks)
-   Guidance on future iterations of grey market identification models


## Methodology

**Data Collection** | [Google Drive Link](https://drive.google.com/drive/folders/1zvcqDbtZaCetQwsBum8EjB27g4tBdJ_G)

In order to follow along with the notebooks of this project, please download the pickled dataset titled 'counter_dataset' (no extension) from the link and install to a './datasets/' folder on your local copy of this repository.

**Data Cleaning** 

- **Missing Data** While most features were complete, various features were missing anywhere from a couple hundred to over 95% of values. Various boolean features with a high frequency of missing data could be ignored, as they were non-interesting, non-distinguishing, and severely imbalanced. However, for others, such as ['offer_merchant'], missing values were imputed with 'Unavailable.' 
    
**Target Variable Assignment**

We analyzed the text data within each review body, with a goal identifying "keywords" and "key phrases" used by reviewers after being the target of fraudulent or grey market activity. The process began by analyzing the appearance of the words "fake" and "counterfeit" in all reviews, across all ratings, and identifying instances when the unigrams were used with positive sentiment versus negative. While qualifiable words and phrases associated with grey market activity were found through vectorization, the criterion for adding them to our 'target assignment' list was ultimately subjective, with the primary assumption being that reviewers post truthful reviews, and that the Amazon platform would effectively filter out any non-credible review postings. Each review in the sample set was labeled as 0 or 1, with 1 indicating that the review was associated with grey selling. The labeled reviews dataset was then used to train a classification model to recognize what pre-review characteristics of a purchase would be sufficiently descriptive of illicit market activites.

**Synthetic Data Points**

As with any dataset dealing with fraudulent or illicit activity, classes were severely imbalanced. In our sample, positive cases represented 0.48% of observations. SMOTEN and SMOTENC were used to populate our dataset with synthetic points, for classifications using continuous and combined features, respectively.

**Modeling**

Our initial model, using Random Forest, performed excellently. To derive interpretations, we ran the same set of features through a Logistic Regression with no penalty. While analyzing coefficients, we noticed the most important features were number of “likes” or comments a review received. As individual review data was used to impute our target variables, a serious data leakage violation was detected. After dropping review-related features, and using only price, number of existing reviews, and number of images on a product display page, our model's performance fell but still appeared to be fitting rather well to unseen test data.

The next stage of models included categorical features into our model. This model performed worse specifically on Recall, but outperformed the previous models on all other accounts, with a higher balanced-accuracy score. In respect to the collinearity between our categorical features, as well as the exploded dimensionality of one-hot-encoding our non-ordinal categories, it would be necessary to implement Principal Component Analysis. PCA tuning could not be succesfully executed, however, and will need to be addressed in future iterations. 

## Findings
Unable to provide concrete answers to our mission questions, the sum of our findings rather serve to illuminate the path to more effective, future iterations of our model.

For example, we learned that the more images there on a product display page, the more likely it is to be a target of grey market activity. Additionally, an increase in total reviews indicated a reduced chance of any illicit behaviors. However, these observations, however numeric their coefficients, are ultimately non-interesting observations that are victim to the chicken-and-egg dilemma. Is it the absence of bountiful images that makes a product a gray market target, or is it that gray market listings use unique product codes and that bad actors don't bother with the niceties of uploading images? Either way, gray market actors are constantly evolving, and today in 2023 one would be hard-pressed to find any product display page that is not chockful of sample images. 

Similarly, we learned that items with a Prime guarantee are less likely to host gray-market activity, but even so its coefficient in a logistic regression is quite low and insignificant. Today, there is a much larger number of population of Prime users, as well as an expansion of products as well as sectors covered by Prime guarantees and deliveries. Modern data would certainly serve to be much more interesting than our sample.

## Future Iterations
Not only were certain features entirely nonexistent, amongst those available, there was a high frequency of missing data. The team is highly confident that features such as Minimum Authorized Price, SNS presence, and completed Merchant information would allow this project to be instantly improved and scalable. Acquiring more data would also serve the benefit of developing a clearer picture of the overall Amazon ecommerce landscape. The distribution of brands and categories in the working data sample was not representative of the true distribution of ecommerce categories on the Amazon platform. Having more data upon which we could develop a means of assigning our target, as well as identifying patterns would remove many limitations that we faced.

Improvements could also be made to target aassignment. By removing the restraints of computing on a local device, advanced text mining and NLP could be performed by exhaustively running from unigrams, bigrams, trigrams, etc. Working locally, challenges were caused by the dimensionality of a vectorized corpus, but computing in the cloud would remove these constraints.

Technical limiations of working locally also stymied hyperparameter optimization. While tuning could be performed for ensemble models and simple logistic regressions, it could not be completed for PCA. Due to high collinearity between features such as brand and price, optimizing PCA would be a key component of developing future iterations of the model.


-   Articles:
	-   [https://www.brandalignment.com/shadow-hierarchy-grey-market//](https://www.brandalignment.com/shadow-hierarchy-grey-market//)
	-   [https://greyscout.com/protect-your-brand-and-control-grey-market-activity-on-marketplaces/](https://greyscout.com/protect-your-brand-and-control-grey-market-activity-on-marketplaces/)
    

## Team

Edward Lee | [https://linkedin.com/in/edward-yh-lee/](https://linkedin.com/in/edward-yh-lee/)

