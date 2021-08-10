# Linear Regression Analysis of KC Housing Data

## Introduction and Background
In this project, the intended stakeholder is a real estate broker looking to obtain a competitve advantage over other brokers by developing a tool that can help its clients sell their home for top-dollar, or purchase a home at fair-value. 

The objective of this project twofold; the primary objective is to build a model that will effectively predict the price of a home (to be sold or purchased) given a specified set of features. The secondary objective is to identify the most important features impacting the price of a home in Kings County. Successful identification of these features will help inform future sellers of potential rennovations/upgrades that may increase the value of the home to be sold. 

## Regression Model

Using OLS regression, the best performing model consisted of the following features:

* sqft_living
* waterfront
* lat
* grade*sqft_living15

The final r-squared score for the train data was approximately 0.717, while the r-squared score for the test data was 0.712, meaning the model can explain the variation in home prices ~71.2% of the time. The model produces a RSE of $211,724, which is the average amount the selling price differs from what the model predicts. While there is no set standard by which to judge RSE, it's fair to say that producing an error this large may be problematic. The RSE is about 39.4% of the average selling price of $537,861, to put it into perspective.

Looking at the regression diagnostics, it can be concluded that all three assumptions for the residuals of a linear regression model have most likely been violated. The distribution of the residuals is leptokurtic, they exhibit heterskedasticity, and the model variables may not have a linear relationship with the target.

## Regression Diagnostics

### Heteroskedasticity
Visualizing the data residuals versus predictions for the training data, it is apparent that the data is concentrated around in the center of the plot, and not randomly distributed. From the Breusch-Pagan test, the model residuals exhibit heterscedasticity. Both the Lagrange multiplier and F statistic are large (~725 and ~32.9, respectively), while their corresponding p-tests are extremely small (on a magnitude of -138), meaning the null hypothesis (homoskedasticity) is rejected.

![heteroskedasticity](/Graphs/download-1.png)

### Normality of residuals
Based on the qqplot and Jarque-Bera test, the residuals violate the normality assumption. The qqplot shows that the residuals have distinctly thin tails. The Jarque-Bera test further coroborates this; the score is far from a score of 0 (~495), which would indicate a normal distribution, and the low chi-squared score (on a magnitude of -108) makes the test score significant at an alpha of 0.05. The residuals have a very slight skew, and the kurtosis measure points to a leptokurtic distribution, which was also indicated in the qqplot. These factors negatively impact the r-squared score.

![normality of resids](/Graphs/download.png)

### Linearity of features relative to target
The feature that exhibited the greatest linearity with respect to the target was sqft_living; it can be seen from the plot below that this linear relationship is pretty loose. Other features were even less linearly related to the target, indicating a strong case for non-linear relationships between the features and the target.

![linearity](/Graphs/download-2.png)

Taking all of this information into account, a linear model may not be the best model to use for this dataset, but a decent linear model was nevertheless created. For the realtor, it does give an idea of the important factors contributing to the sale price of a home out of a pool of features. Some of the features, such as liveable square footage, waterfront properties and renovations may not be surprising as being important. Other features, such as latitude and grade*sqft_living15 are more interesting.

## Final Thoughts

This model should be used in conjunction with realtor experience and intuition in the formulation of an appropriate asking and/or selling price for a client's home. If they are available, adding more features to include in the model as well as more year's worth of data may improve the accuracy of the model. Other predictive models should also be considered; the goal would be to find a predictive model that would increase accuracy while decreasing or maintaining model complexity. This linear model is a great starting point because it is relatively easy to understand and interpret.

## Next Steps
Going back to the histograms of the features prior to log transformation, some of the features, such as sqft_lot, had data points that were significantly larger than the other data points, skewing the distribution. It may be worthwhile to go through each of these features and look for outliers. Taking these outliers into account and potentially adjusting for them may make some the features that were insignificat, significant. This in turn could lead to a better model.
