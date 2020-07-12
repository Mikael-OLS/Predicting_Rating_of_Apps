# Predicting Mobile Apps Rating
## A Linear Model Project
It feels like everyone has at least had one app idea that they say would make millions. Ironically, I don't know anyone that actually have gone through with their idea. Neverthelsee, if they did, would the app be successful? In this project a linear model will be created to predict the rating of mobile apps. The goals of this project are:

* Make a model that successfully predicts the rating.
* Find out which variables that are important for predicting.

In the end, the first goal is completed whilst the second one leaves more to be desired. 

## Table of contents
1. [Data Exploration](#Data)
2. [Final Dataset](#Final)
3. [Modelling](#Modelling)
 01.  [Benchmark Model](#Bench)
 02.  [Final Model](#Final2)
3. [Summary](#Summary)

<a name="Data"></a>
## Data Exploration
After cleaning the data, we are left with 13 variables and 9360 observations. The dependent variable has the following distribution.

![bild](https://user-images.githubusercontent.com/62875997/87072253-c304d200-c21b-11ea-8f0c-fe88daddd638.png)

The variable, Rating, is between 1-5 and seems skeewed to the higher possible values.

![bild](https://user-images.githubusercontent.com/62875997/87072443-0a8b5e00-c21c-11ea-8f59-c7d4f12052c4.png)

![bild](https://user-images.githubusercontent.com/62875997/87072479-1aa33d80-c21c-11ea-89c7-21f7a7e91c14.png)

Since the variable "Number of Reviews" is either very low or enormous, we use the logarithm of the variable instead.

![bild](https://user-images.githubusercontent.com/62875997/87072611-635af680-c21c-11ea-9d84-36196041b67e.png)

This plot shows the relationship between the variables "Reviews" and "The logarithm of Number of Reviews". As one can see, when the "The logarithm of Number of Reviews" goes up, the spread of the "Ratings" shortens.

![bild](https://user-images.githubusercontent.com/62875997/87073106-293e2480-c21d-11ea-8ef5-fbdcd84faf33.png)

Unsurprisingly , the more popular apps have higher rating. 

![Skärmklipp 2020-07-09 19 45 56](https://user-images.githubusercontent.com/62875997/87072893-d1072280-c21c-11ea-9cce-ddd0170e3672.png)

![Skärmklipp 2020-07-09 19 45 50](https://user-images.githubusercontent.com/62875997/87072915-d95f5d80-c21c-11ea-9994-d870f72123f2.png)

The words mobile and video are two frequently words used in the title of the apps. They are going to be used as dummies when predicting. 

![bild](https://user-images.githubusercontent.com/62875997/87073212-5094f180-c21d-11ea-8b57-13b8e9b0108a.png)

If an app is free, it is more likely to be rated higher. My hypothesis is that if an app costs, then ones expectations are higher and often not met. 

![bild](https://user-images.githubusercontent.com/62875997/87073403-a36ea900-c21d-11ea-8ff4-4be86027a4a2.png)

Mature 17+ is standing out here. Further in the project, we will create a dummy for Mature 17+.

![bild](https://user-images.githubusercontent.com/62875997/87073502-cc8f3980-c21d-11ea-9771-522e5af0fbcf.png)

![bild](https://user-images.githubusercontent.com/62875997/87073567-e466bd80-c21d-11ea-8309-6706c3890b70.png)

Sports and Finance will be two last dummies.

<a name="Final"></a>
## Final Dataset
The dataset used to predict with has the following variables:
* Rating
* Sport
* Size
* Installs
* Reviews_log
* Free
* Mobile_word
* Video_word
* Mature 17+
* Finance
* Last_Updated

<a name="Modelling"></a>
## Modelling

<a name="Bench"></a>
### Benchmark

To compare our final model, we need a benchmark model. Below is that models performance:

* Mean Absolute Error: 0.3524030362361836
* Mean Squared Error: 0.2603782619610998
* Root Mean Squared Error: 0.5102727329194652

Since the scale of our dependent varaible is between 1-5. A MSE of .35 is actually pretty good.

![bild](https://user-images.githubusercontent.com/62875997/87222736-af21b300-c376-11ea-980b-18e7890f9b6b.png)

![bild](https://user-images.githubusercontent.com/62875997/87222743-be086580-c376-11ea-9305-593aacb60469.png)

![bild](https://user-images.githubusercontent.com/62875997/87222749-c6f93700-c376-11ea-86d0-5b163a451f5b.png)

<a name="Final2"></a>
## Final model
The benchmark model is good. However, it seems to have a problem to identify the apps with lower ratings. To improve the model, we can start by looking at how the number of variables effects the R^2.

![bild](https://user-images.githubusercontent.com/62875997/87222800-5c94c680-c377-11ea-8243-5d68cb885e36.png)

After 7 variables, the R^2 only improves slightly. A R^2 of only 6.5% is not good and indicates that the variation in the dependent variable can be hard to capture. However, one solution to get a higher R^2 could be to include interactions.

![bild](https://user-images.githubusercontent.com/62875997/87222814-8352fd00-c377-11ea-9f14-19fcee8c4d57.png)

This is better! Now we have 19 variables and 17 of them are going to be used to predict the rating. Below is the variables that are going to be included in our model:

* Sport
* Size
* Installs
* Reviews_log
* Free
* Mobile_word
* Video_word
* Mature 17+
* Finance
* Last_Updated
* Size_Reviews_log
* Size_Last_Updated
* Installs_Reviews_log
* Installs_Last_Updated
* Reviews_log^2
* Reviews_log_Last_Updated
* Last_Updated^2

Where, Reviews_log^2 is the most influencial variable. Creating a linear model on our new set of variables gives us the following performance:

*Mean Absolute Error: 0.3381119469057047
*Mean Squared Error: 0.23561621079238187
*Root Mean Squared Error: 0.48540314254481487

Let's take the difference of the performance of the final model vs the benchmark model.


* Mean Absolute Error diff: -0.0007167293664471219
* Mean Squared Error diff: -0.003009087501957358
* Root Mean Squared Error diff: -0.0030897420444483403

This means that our new model perform slightly better than the benchmark! Below is the intercept and the betas of the model: 

* Intercept:                  4.4618228199
* Sport:                      1.071296e-02
* Size:                      -1.894181e-09
* Installs:                  -6.423399e-10
* Reviews_log:               -5.266128e-02
* Free:                      -1.730735e-01
* Mobile_word:               -1.588689e-01
* Video_word:                 1.177296e-01
* Mature 17+:                -1.203399e-01
* Finance:                    3.133079e-03
* Last_Updated:               3.800360e-04
* Size_Reviews_log:           1.378599e-10
* Size_Last_Updated:         -2.519119e-12
* Installs_Reviews_log:       1.152280e-11
* Installs_Last_Updated:      5.728949e-12
* Reviews_log_Reviews_log:    4.756994e-03
* Reviews_log_Last_Updated:  -1.269595e-05
* Last_Updated_Last_Updated:  9.705829e-08

<a name="Summary"></a>
## Summary
We succeed with the half of the goals by creating a model that predicts the popularity fairly well. The model has a MSE of 0.34 when predicting the ratings that span from 1 to 5. Unfortunally, the R^2 of the model is only around 0.09. This can only be seen as a faluire. The bad R^2 is probably due to the dependent variable being very hard to predict. However, would we choose one variable that explains the variation of our dependent variable, then it would be Reviews_log^2.

If one would be interesting in doing a similar project - I would recommend trying to predict the ratings through ML instead of a linear model.

## Thanks for reading!
