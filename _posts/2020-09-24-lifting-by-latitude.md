---
layout: post
title: Powerlifting... with some latitude!
subtitle: Can your location on the planet lead to higher PRs?
cover-img: /assets/img/1280px-Boys_+82_kg_Weightlifting_2018_YOG_25.jpg
thumbnail-img: /assets/img/Lasha_Talakhadze_Rio_2016.jpg
share-img: /assets/img/Lasha_Talakhadze_Rio_2016.jpg
tags: [Powerlifting, gravity]
---


### Did you know?

<img align="left" style="float:left; padding-right:10px" src="/assets/img/istockphoto-841956772-170667a.jpg"> The surface of the Earth at the equator spins roughly *1,000 miles per hour*.  As a result of this insane rotation, Earth actually bulges out at the equator, forming an oblate spheroid rather than a sphere.  Meaning, the diameter around the equator is larger than the diameter connecting the poles.  And so, a person standing on the surface at the equator, being further from the center of the Earth than a person standing on the surface at the poles, experiences less gravity (approximately 0.5% less gravity, in fact).  With this is mind, I sought out to determine whether or not powerlifters benefit from this information.  **Are powerlifters able to lift more weight (and score higher) at locations closer to the Equator?  Is there a correlation between lower latitudes (closer to the Equator) and higher scores in competition?**  


### Powerlifting, a quick overview

Powerlifting began all the way back in Ancient China and Greece, where men would lift stones to display their strength and see who could lift the most.  At the time and up through the 1950s, powerlifting was akin to the strongman competition today, meaning it involved various "odd lifts" for competition.  Eventually, the sport evolved and the lifts became standardized to the current three:  squat, bench press, and deadllift.  

{: .box-note}
**Fun Fact:** Modern powerlifters are able to perform lifts with or without equipment (such as knee wraps and other supportive wear).  Un-equipped lifts are also referred to as 'raw' lifts.

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


Link to my work [here](https://github.com/Collin-Campbell/BuildWeek1/blob/master/Collin_BuildWeek_Unit1.ipynb)

![Lifter](/assets/img/CC0_Photos_Fitness_Free_Images_Free_Photos_Gym_High_Resolution_Royalty_Free_Weightlifter-1617119.jpg!d.jpg){:class="img-responsive"}
