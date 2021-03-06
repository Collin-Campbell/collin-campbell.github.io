---
layout: post
title: A major disaster today? Well, let me check my stocks...
subtitle: Are abnormal daily percentage changes of certain stocks and precious metals indicative of a federally declared disaster?
cover-img: /assets/img/disaster1.jpg
thumbnail-img: /assets/img/stocks.jpg
share-img: /assets/img/stocks.jpg
tags: [Disasters, stocks, metals, FEMA]
---


### The Theory:

Often, the occurrence of major events are used to predict a future change in the prices of certain goods.  For instance, consider a presidential candidate who supports clean energy.  If this candidate were to win, we might expect an increase in the stock prices of companies associated with green technology as well as a decrease in the prices of commodities associated with non-renewable energy, such as crude oil.  But, could the opposite be true as well?  Could the daily percentage change of certain stocks and precious metals be indicative of the occurrence of a major event, such as a natural disaster?  For example, consider the following event:  a Category 5 hurricane strikes the State of Florida and causes severe damage to the local infrastructure.  In response, the President of the United States declares an emergency.  Over the course of that day, the stock prices of insurance companies that insure buildings in the affected area plummet significantly.  Hypothetically, if this were true, we could use these significant changes in prices to predict whether or not the President declared an emergency. 


{: .box-note}
**What constitutes a major disaster?** 

The President of the United States has the power, through the Federal Emergency Management Agency (FEMA), to declare a major disaster when it is determined that State or Native American Tribal governments require supplemental emergency services in order to avert the threat of a catastrophe.  The disaster must be of such severity and magnitude that the the response is beyond the capabilities of the local government.  Major disasters can be declared for any natural event, including any:  ***hurricane, tornado, storm, high water, wind-driven water, tidal wave, tsunami, earthquake, volcanic eruption, landslide, mudslide, snowstorm, or drought, or, regardless of cause, fire, flood, or explosion.***    
    

![FEMA](/assets/img/FEMA.jpg){:class="img-responsive"}


### Wrangling the data

I was able to source my FEMA data from [Kaggle](https://www.kaggle.com/fema/federal-disasters).  This dataset included a feature called 'Declaration Date' which included a list of dates on which the President declared an emergency.  I pulled out this column and eventually used it to create my target vector (a categorical column with 'Yes' or 'No' for if an emergency was declared on a specific day).  I also sourced my precious metals data from [Kaggle](https://www.kaggle.com/lsind18/daily-london-metal-fix-prices).  This dataset contained the AM and PM London Fix Prices for gold, platinum, and palladium.  I used these columns to engineer new features:  the daily percentage change of of each precious metal.  I then sourced stock data from Yahoo Finance.  The stocks I chose and my reasoning for each are as follows:

- Home Depot:  home improvement, supplier of tools and construction products
- Lowe's:  home improvement, supplier of tools and construction products
- Walmart:  sells food, water and clothing, all needed items during a natural disaster 
- Bank of America:  increase stress on the economy, supply chain distruption 
- American International Group (AIG):  insurancy company
- Halliburton:  construction company

From each of these datasets, I engineered a new feature for the daily percentage change of each stock based on open and close prices.  Keeping only the percentage change of each commodity or stock, I merged all the datasets on the date columns.  Lastly, I engineered a new feature for each column of the merged dataframe that denoted if a large change in percentage had occurred on that day.  I defined 'large change' as follows:  If the percentage change at a single observation was greater than the average of the positive values in that column OR less than the average of the negative values in that column, return 1. Otherwise, return 0.  A value of 1 indicated a large change had occurred.  


### My baseline:

'No' was the majority class with a baseline accuracy of: 0.7701062215477997

![baseline](/assets/img/Baseline.png){:class="img-responsive"}


### Building the models:

XGB_model = XGBClassifier(random_state=42, n_jobs=-1, 
                          n_estimators=400, max_depth=3)

Logistic_Regression_model = LogisticRegression()

Random_Forest_model = RandomForestClassifier(n_estimators=400,
                            random_state=42, max_depth=12)


### How they performed:

The XGB boost model was best fitting, but the Random Forest model scored the highest accuracy on the testing data.  With that being said, all models failed to show any significant improvement above baseline.

![accuracy scores](/assets/img/scores.png){:class="img-responsive"}


### Conclusion:

Percentage change in gold was the most important feature, as shown in the following plot: 

![permutation importances](/assets/img/Perm_imp.png){:class="img-responsive"}


As the daily percentage change in gold approached 0, it became more likely that an emergency was not declared.  As the daily percentage change in gold surpassed 2, the likelihood of a declared emergency increased. 

![PDP feature](/assets/img/PDP_feature.png){:class="img-responsive"}


As shown in the PDP interaction plot, the percentage change in gold had a much greater impact on the predicted outcome of the Random Forest model than the percentage change in Home Depot stock.  The impact was more relevant at large negative and large positive changes, with the large positive changes being most important.

![PDP interact](/assets/img/PDP_interact.png){:class="img-responsive"}


### My shortcomings

- Models were not useful.  As can be seen in the confusion matrix, the Random Forest model was unable to correctly identify true emergencies. 

![confusion matrix](/assets/img/Conf_mat.png){:class="img-responsive"}

- The major fault in my reasoning:  the time at which an emergency is declared depends on when the local government applies for assistance.  Meaning, the declaration could occur days or even weeks after the actual catastrophic event.  Additionally, other variables could impact the prices of metals or stocks.  For instance, maybe there was a newly discovered use for palladium that caused a drastic increase in its price. 


Link to my work [here](https://github.com/Collin-Campbell/BuildWeek2/blob/main/project.ipynb)

![ship](/assets/img/ship.jpg){:class="img-responsive"}
