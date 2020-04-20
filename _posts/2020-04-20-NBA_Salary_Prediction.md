---
layout: post
title: NBA Salary Prediction Based on NBA Stats
---

<h1 style="font-size:200%;">
Introduction:
</h1>

NBA player make a lot of money, in fact, it is the highest paid sport in the world. Top players in the NBA make over $30 million a year. However, the average NBA player makes around $8 million a year. What determines which NBA player makes more money? Stephen Curry leads the laegue in 3pt made and is making $40 million, the top scoring player James Harden is being paid $37million a year, the top rebounding player Andre Drummond is being paid $27 million a year, Kemba Walker who doesn’t lead the league in anything is being paid $32 million a year. Does a player get paid more because he scores more?  If so, why does Stephen Curry get paid the most? What determines a player’s salary, and can we predict based on his performance how much he will be paid?  
 
<h1 style="font-size:200%;">
Overview:
</h1>

This project's objective is to determine whether there is a linear relationship between NBA player salary and performance. Performance is measured by basketball statistics in categories. Common statistics are minutes played, games played, points, two-pointers, three-pointers, rebounds, turnovers, assists, steals...etc. By looking at categories that have high correlation with salary we can determine if there is a linear relationship. 
 
<h1 style="font-size:200%;">
The Method:
</h1>

Basketball reference has a plethora of basketball information. From player nicknames to advanced player statistics, basketball reference has all the information you need except player salaries from past years. However, ESPN keeps a pretty good record of player salaries. My goal is to scrape these websites for salaries and stats for the past 10 years and perform linear regression to observe the relationship between performance and salary. 

Web-Scrapping: 
We start by importing all the necessary libraries to do analysis. By utilizing beautifulsoup, we are able to scrape stats from basketball reference and ESPN. Lets start with ESPN.com. ESPN has player salary information sorted by seasons, and in each season player salary information for that season is divided into 14 sub pages. Taking a look at the URL of the page we can see that the seasons are part of the URL and by changing the year in the URL we can change the season. Similarly, the sub pages can also be turned by changing the page number in the URL. From here, we write a function that can grab information for the past 10 years. 

Once we have the data frame constructed, we now need to decide how to analyze player salary. I decided to use percentage salary cap space as a measurement of player salary. This is because each year the salary cap for the NBA changes based on how popular the NBA is. In order to normalize salary for each year based on salary cap space, we take the percentage of the cap space a player takes up. This is done by dividing the player salary by the total salary cap for teams. 

The next step was to scrape NBA statistics. This was done using beautifulsoup as well. From the website baskeball-reference.com, we are able to find all the player stats for each year. By changing the year in the URL we are also able to scrape multiple seasons worth of data.
Now that all the statistics we need have been scrapped we create a dataframe for percentage salary cap and NBA stats and combine them. 
 
<h1 style="font-size:200%;">
The Analysis:
</h1>

After constructing a data frame with player stats, percentage salary cap, and year, we can now do some analysis on the data. I removed all players that have played 15 games or less since their stats are on the lower end and could skew the data. I then changed all the NaN to 0 since that would indicate that they just didn’t score or do anything when they were on the court. I first ran a correlation plot to see the correlation between features. As you can see there were a lot of features and the heatmap looks really messy. 

![Correlation Heat Map]({{dlin91.github.io}}/images/corr_heatmap.png)

There wasn’t much information gained from here other than telling me to trim down some categories. I decided to look at just the features that had the highest correlation to percentage cap. These were points, field goals, field goal attempts, free throws, free throw attempts, rebounds, assists, steals, blocks, age, minutes played, turn-overs. I then ran a pairplot of these features to visualize the relationship between features and look for muticollinearity. 

![Pairplot of Features]({{dlin91.github.io}}/images/pairplot.png)

I used the built in variance inflation factor module to assess VIF of categories and removed the once that had high collinearity. PTS was related to MP, FG, FGA, 2P, and 2PA. I removed those and kept PTS. After assessing VIF of features, I ran a statsmodel summary to take a look at the coef and p-values. 

From here, we are ready to train the model. I set the dependent variable (y) to percentage salary cap and the independent variables (x) to AST, age, FT, DRB, log_PTS, and STL as these were the final features that passed the VIF screen. Running a regular regression model I split the model into 80% training and 20% testing. I also did cross-validation using Kfold. The final R2 value was 0.508. 

I decided to do some regulariztion as well. After standardizing the features using standard scaler, I ran a LASSO and Ridge regression model analysis.  The R2 value for the LASSO model was 0.507 and for Ridge it was 0.507 but slightly higher than regular regression and LASSO. I decided to play around with the features more and log-transformed the features to see if I could increase the R2 value. It turns out log transforming the data did not increase the R2 and so I decided to not use log transformation for all of the features. 
 
<h1 style="font-size:200%;">
The Conclusion:
</h1>

After running my model I plotted the actual data vs the predicted. It showed that there was a linear relationship between my prediction and the actual values. My model was not great at predicting higher values. This could be due to the ‘super-star’ effect. Some players are paid more because they can draw in larger audiences and sell more merchandise than others. This means that organizations are willing to pay more to these players so that they can make more money even if their stats don’t represent what they should earn. 

![Predicted VS Actual]({{dlin91.github.io}}/images/predvsactual.png)

<h1 style="font-size:200%;">
Future Exploration:
</h1>

For future exploration, I would like to take advanced stats and see whether there is a relationship between advanced stats and salary. I would also like to assess whether social media presence will have an effect on player salary. 
 
 
 




