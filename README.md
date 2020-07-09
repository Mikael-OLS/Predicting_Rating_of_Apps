# Predicting Mobile Apps Rating
## A Linear Model Project
It feels like everyone have atleast one app idea that they say would make milloins. Ironically, I don't know anybody that actually have gone through with their idea. But if they did, would the app be successful? In this project a linear model will be created to predict the rating of mobile apps. The goals of this project are:

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
After cleaning the data, we are left with 13 variables and 9360 observations. The dependent variablehas the following distribution.

![bild](https://user-images.githubusercontent.com/62875997/87072253-c304d200-c21b-11ea-8f0c-fe88daddd638.png)

The variable, Rating, is between 1-5 and seems skeewed to the higher possible values.

![bild](https://user-images.githubusercontent.com/62875997/87072443-0a8b5e00-c21c-11ea-8f59-c7d4f12052c4.png)

![bild](https://user-images.githubusercontent.com/62875997/87072479-1aa33d80-c21c-11ea-89c7-21f7a7e91c14.png)

Since the variable "Number of Reviews" is either very low or enormous, we use the logarithm of the variable instead.

![bild](https://user-images.githubusercontent.com/62875997/87072611-635af680-c21c-11ea-9d84-36196041b67e.png)

This plot shows the relationsship between the variables "Reviews" and "The logarithm of Number of Reviews". As one can see, when the "The logarithm of Number of Reviews" goes up, the spread of the "Ratings" shortens.

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

## Final Dataset
The dataset used to predict with has the following variables:
*Rating
*Sport
*Size
*Installs
*Reviews_log
*Free
*Mobile_word
*Video_word
*Mature 17+
*Finance
*Last_Updated

## Modelling

### Benchmark

To compare our final model, we need a benchmark model. Below is that models performance:
Mean Absolute Error: 0.3524030362361836
Mean Squared Error: 0.2603782619610998
Root Mean Squared Error: 0.5102727329194652




