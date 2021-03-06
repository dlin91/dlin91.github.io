---
layout: post
title: Twitter Gender Prediction
---

<h1 style="font-size:200%;">
Introduction:
</h1>

Targeted ads are a simple way to increase revenue through users. By knowing what types of products a person might have will increase the chances of a person buying the product. If we are able to know the gender of the user, we could potentially increase the chances that a user will buy a product. We can send targeted products based on gender, for example, sending beauty product ads to females and video game ads to males. This of course isn’t to say only females buy beauty products and only males buy video games, this just increases our chances of a person buying the product. 

 
<h1 style="font-size:200%;">
Overview:
</h1>

The twitter profiles of users can contain a lot of information. The goal of this project is to determine if we can use the elements on a user’s profile to determine their gender. Could we build a model that will predict the gender of the user? This is, in other words, a classification problem. Using the dataset from Kaggle,  we see there are a lot of features that we could potentially use in our model. So let's begin! 
 
<h1 style="font-size:200%;">
The Method:
</h1>

To start out we take a good look at the data set and determine if there are features that we don’t need. We don’t need the user name since that's based on personal preference and the names could be incoherent words linked together. Parsing them could be a difficult task, so we just remove them for now. Time zone was also removed since different genders live all across the world. I decided to remove link color because there was also sidebar color to use so I decided to just take one of them. 
	
We can see that other features include text, description, favorite number, tweet count, retweet count, and gender. Using these features, let’s start doing some cleaning of the data and build some models. The first cleaning part is to clean the ‘text’, and ‘description’ features. We want to remove all the leading spaces, punctuation, and random symbols. I used regular expressions to remove them and labeled the new columns of ‘clean text’ and ‘clean description’. Lets also remove any rows that contain NaN. 

After cleaning the text up we can start analyzing the text. The first step is to tokenize the corpus of words. By using the built in function Count Vectorizer from scikit learn, we can make an array of words that are used in text. Let's set some parameters of the count vectorizer, I set the n-grams to 1 since I want to capture the single words. The token pattern is all english letters, and everything is changed to lowercase. The max df is set to 0.8, meaning that words that appear in more than 80% of the documents are removed. Words such as ‘the’, ‘a’ ...etc are filler words and appear more often but contain no value. Finally, the max features are set to 100, this is because I only want to look at the top 100 words that appear in the corpus. After we’ve tokenized the words and made it a dataframe, we can merge it to the original dataframe. 

Now that we have our features ready for processing, let’s not forget to take a look at the dependent variable we’re trying to determine. Looking at the gender column we can see that there are more values than just ‘male’, and ‘female’. Let’s remove anything that is not male or female and take a look at the distribution of male and female. We have a pretty good distribution between male and female so we don’t have to manipulate out sampling. 

 
<h1 style="font-size:200%;">
The Analysis:
</h1>

Our features are ready so let’s begin the  train, test, split. We can use scikit learn’s built in function to help us with that. The next step is to scale our features to make them easier to work with. 

The first model we’re going to try is Decision Tree. I wrote a function that loops through 1-30 depths to find the depth of the decision tree that will give the best score. Looking at the graph we can see that it's 3. After running the model with depth of 3 we can see that it has a ROC/AUC score of 0.59. Not bad for a first model. 

![Decision Tree Depth]({{dlin91.github.io}}/images/decisiontree)
![Decision Tree ROC/AUC Curve]({{dlin91.github.io}}/images/decisiontree1.png)

Next lets try Random Forest. Using the same loop method we loop through depths that will give us the best depth. Looking at the graph we can see that the depth that gives us the best score is max depth of 4. This results in a ROC/AUC score of 0.59 as well. 

![Random Forest Depth]({{dlin91.github.io}}/images/randomforest)
![Random Forest ROC/AUC Curve]({{dlin91.github.io}}/images/randomforest1.png)

Next let’s take a look at KNN. Using the same method, again, we can find the best K to use. Looking at the graph we can see that the best k is 2. The best ROC/AUC score is 0.55. Slightly lower than the previous models. 

![KNN - k]({{dlin91.github.io}}/images/knn)
![KNN ROC/AUC Curve]({{dlin91.github.io}}/images/knn1.png)

For Logistic Regression, I tried setting the hyperparameter C to 0.1. The resulting ROC/AUC score is 0.59 as well. 

![Logistic Regression ROC/AUC Curve]({{dlin91.github.io}}/images/lg.png)

Finally lets run a few Naive Bayes models. This includes multinomial, gaussian, and bernoulli. Multinomial achieved a 0.59 ROC/AUC score, Gaussian received a 0.58 score, and Bernoulli received a 0.58 as well. 

![Multinomial NB ROC/AUC Curve]({{dlin91.github.io}}/images/mnb.png)
![Gaussian NB ROC/AUC Curve]({{dlin91.github.io}}/images/gnb.png)
![Bernoulli NB ROC/AUC Curve]({{dlin91.github.io}}/images/bnb.png)

 
<h1 style="font-size:200%;">
The Conclusion:
</h1>

Finally, using a pipeline function we confirm the best parameters to use for each model and plot the ROC/AUC graphs together. The best ROC/AUC score is the Random Forest, followed by logistic regression. When considering which metric to use to measure which model did best I used ROC/AUC score. When considering precision vs recall, I thought about the consequences of low precision: meaning that there is a high false positive rate. This means that if we are trying to promote a makeup ad for females, we may accidentally find a male as female. This means that we just wasted money putting out an ad to someone that would most likely not buy it. For low recall, it means that we have a high false negative rate, meaning that our model can accidentally identify a female as male. This can result in our ad not appearing to that user and miss our chance to promote a product. After thinking about these, I decided that both metrics are important, it really depends on the cost of an ad and how much you lose if you place the wrong ad (precision), and how much you lose if you miss your chance to sell a product (recall). Therefore, I decided to use the ROC/AUC score since you can adjust the threshold to balance precision and recall to whatever metric you consider more. 

![Final ROC/AUC Curves]({{dlin91.github.io}}/images/rocauc.png)

<h1 style="font-size:200%;">
Future Exploration:
</h1>

For future exploration, I would like to gather more data from users such as how many people are following the user, what type of people is the person follwoing. This will help us evaluate more features and see if there are better features with better predictive power. I would also like to confirm their genders using other platforms such as instagram or facebook. If we are able to confirm their gender using two platforms, this will give us more confidence in the actual gender of the user. 
 
 
 




