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

Often, the occurrence of major events are used to predict a future change in the prices of certain goods.  For instance, consider a presidential candidate who supports clean energy.  If this candidate were to win, we might expect an increase in the stock prices of companies associated with green technology as well as a decrease in the prices of commodities associated with non-renewable energy, such as crude oil.  But, could the opposite be true as well?  Could the daily percentage change of certain stocks and precious metals be indicative of the occurrence of a major event, such as a natural disaster?  For example, consider the following event:  a Category 5 hurricane strikes the State of Florida and causes severe damage to the local infrastructure.  In response, the President of the United States declares an emergency.  Over the course of that day, the stock prices of insurance companies that insure buildings in the affected area plummet significantly.  Hypothetically, if this were true, we could use these significant changes in prices to predict whether or not the President declared an emergency on a specified date. 

{: .box-note}
**What constitutes a major disaster?** The President of the United States has the power, through the Federal Emergency Management Agency (FEMA), to declare a major disaster when it is determined that State or Native American Tribal governments require supplemental emergency services in order to avert the threat of a catastrophe.  The disaster must be of such severity and magnitude that the the response is beyond the capabilities of the local government.  Major disasters can be declared for any natural event, including any:  hurricane, tornado, storm, high water, wind-driven water, tidal wave, tsunami, earthquake, volcanic eruption, landslide, mudslide, snowstorm, or drought, or, regardless of cause, fire, flood, or explosion.    

### What prices I used
As the sport grew and became more inclusive, it became apparent that who could simply "lift the most" was an inadequate measuring stick.  People come in all shapes and sizes, and so the need arose to develop a way to compare relative strength.  Initially, this began simply by dividing the amount lifted by an individual's body mass.  This ratio was then used to compare individual lifters.  Over time, the measuring stick has evolved to statistical models.  Currently, the official formula used in powerlifting is the Wilks formula.  *In order to calculate the Wilks Coefficient, the total weight lifted (in kg) is multiplied by the Coefficient to find the standard amount lifted normalized across all body weights*:     

![Wilks](/assets/img/Screen Shot 2020-09-25 at 9.47.51 AM.png){:class="img-responsive"}


### The process

I was able to source my original data from [Kaggle](https://www.kaggle.com/open-powerlifting/powerlifting-database).  This powerlifting database, maintained by the OpenPowerlifting project which aims to create an open archive of the world's powerlifting data, contains data from over 22,000 meets and 412,000 lifters from competitions worldwide.  Because the Wilks formula makes use of the total weight lifted, I removed lifters that did not perform all three of the standardized lifts (squat, bench press and deadlift).  I also only accounted for lifters that performed un-equipped or 'raw' lifts, simply to maintain consistency.  A few rows of my cleaned data can be seen below:  

![Cleaned Data](/assets/img/Screen Shot 2020-09-25 at 10.12.40 AM.png){:class="img-responsive"}

In order to determine the latitude of each meet location, as can be seen in the two columns on the right, I manually looked up latitudes for 116 country states, rounded these values to the nearest whole integer, and then created a function that would add them to all 273,373 rows in my cleaned dataframe.  I then calculated the correlation coefficient between the values for Latitude (in degrees) and the Wilks scores.  With Wilks on the y-axis and Latitude on the x-axis, a negative linear correlation would be indicative of a decreasing Wilks score with increasing latitude.  My calculated correlation coefficient was -0.044, suggesting a very weak negative linear relationship.  Because this value is within -0.1 to 0.1, I cannot significantly say there is a linear relationship present between the two variables.  

But, maybe there is some bias present in my data.  According to [Robert Frederick](http://www.strongur.io/can-we-do-better-than-wilks-absolutely/) in his blog post, the Wilks scoring system, although partially successful, still seems to favor absolute strength.  In order to account for any gender or age bias, I isolated my data based on the most prevalent gender and age class (Males aged 24-34 years old) in the dataset.  To account for any bias between the northern and southern hemispheres due to Earth's tilt, I took it a step further and isolated my data by the most prevalent hemisphere (North).  My newly calculated correlation coefficients were as follows:

- Only Males:  -0.054
- Only Males aged 24-34 years old:  -0.019
- Only Males aged 24-34 years old in the Northern Hemisphere:  -0.027

Although negative, the values are not significant enough to clearly say that powerlifters receive an advantage for competing closer to the equator.  


![Scatterplot](/assets/img/All_Datapoints.png){:class="img-responsive"}


![Line Graph](/assets/img/Averages.png){:class="img-responsive"}


### My shortcomings

- Did not account for changes in elevation
- Rounding latitude values weakened data accuracy
- Spread of latitude values not great, and concentrated
- Wilks bias


Link to my work [here](https://github.com/Collin-Campbell/BuildWeek2/blob/main/project.ipynb)

![FEMA](/assets/img/FEMA.jpg){:class="img-responsive"}
