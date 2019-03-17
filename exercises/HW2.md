Saratoga House Prices
---------------------

The "medium" model performs reasonably well at estimating house prices.
The model includes the following features to predict housing prices: Lot
size, age of house, Size of Living Area, percent college, bedrooms,
fireplaces, bathrooms, rooms, heating, fuel, sewer, waterfront,
newConstruction, and Central Air. The model results are below.

    summary(lm_medium)

    ## 
    ## Call:
    ## lm(formula = price ~ lotSize + age + livingArea + pctCollege + 
    ##     bedrooms + fireplaces + bathrooms + rooms + heating + fuel + 
    ##     centralAir, data = SaratogaHouses)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -232296  -40021   -7679   28919  527748 
    ## 
    ## Coefficients:
    ##                          Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)             28627.732  12224.396   2.342 0.019302 *  
    ## lotSize                  9350.452   2421.118   3.862 0.000117 ***
    ## age                        47.547     65.149   0.730 0.465600    
    ## livingArea                 91.870      5.033  18.253  < 2e-16 ***
    ## pctCollege                296.508    165.531   1.791 0.073428 .  
    ## bedrooms               -15630.719   2885.084  -5.418 6.89e-08 ***
    ## fireplaces                985.061   3385.478   0.291 0.771112    
    ## bathrooms               22006.971   3821.764   5.758 1.00e-08 ***
    ## rooms                    3259.119   1093.631   2.980 0.002922 ** 
    ## heatinghot water/steam  -9429.795   4738.934  -1.990 0.046765 *  
    ## heatingelectric         -3609.986  14009.898  -0.258 0.796689    
    ## fuelelectric           -12094.122  13792.538  -0.877 0.380686    
    ## fueloil                 -8873.140   5395.649  -1.644 0.100257    
    ## centralAirNo           -17112.819   3922.489  -4.363 1.36e-05 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 66280 on 1714 degrees of freedom
    ## Multiple R-squared:   0.55,  Adjusted R-squared:  0.5466 
    ## F-statistic: 161.2 on 13 and 1714 DF,  p-value: < 2.2e-16

An alternative model was tested to better predict housing prices using a
linear regression with different features. This model was "hand-built""
by adding and subtracting various house features considered to be strong
intuitive drivers of housing prices. The model chosen includes lotSize,
bedrooms, bathrooms, age^2, age of house, land value, living area, and
New Construction. All of the variables are statistically significant at
the 5% level. Land Value appears to be a strong driver of housing
prices. In addition, it appears there is a quadratic relationship
between age of a house and the price of a house. The model results are
shown below.

    summary(lmbestmodel)

    ## 
    ## Call:
    ## lm(formula = price ~ lotSize + bedrooms + bathrooms + poly(age, 
    ##     2) + landValue + livingArea + newConstruction, data = SaratogaHouses)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -228709  -35279   -4428   26580  461664 
    ## 
    ## Coefficients:
    ##                     Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)       -3.317e+04  1.000e+04  -3.317 0.000930 ***
    ## lotSize            6.830e+03  2.087e+03   3.273 0.001085 ** 
    ## bedrooms          -6.185e+03  2.420e+03  -2.556 0.010679 *  
    ## bathrooms          2.316e+04  3.405e+03   6.801 1.43e-11 ***
    ## poly(age, 2)1     -2.505e+05  6.798e+04  -3.684 0.000237 ***
    ## poly(age, 2)2      1.716e+05  6.570e+04   2.612 0.009084 ** 
    ## landValue          1.009e+00  4.634e-02  21.777  < 2e-16 ***
    ## livingArea         7.645e+01  4.230e+00  18.074  < 2e-16 ***
    ## newConstructionNo  5.055e+04  7.453e+03   6.782 1.63e-11 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 59600 on 1719 degrees of freedom
    ## Multiple R-squared:  0.6351, Adjusted R-squared:  0.6334 
    ## F-statistic: 374.1 on 8 and 1719 DF,  p-value: < 2.2e-16

A third approach was tested using a KKN approach incorporating the same
features as the "hand-built" model above. The KNN approach was tested
using various K's between 2 to 50.

In order to compare the predictive power of each approach each model was
built using a training data set and compared the RMSE of each model on
the testing data set.

The RMSE for the "medium" model is

    avgrmse1

    ## [1] 66797.95

The RMSE for the "hand-built" model is

    avgrmse2

    ## [1] 59929.3

The best RMSE of the various K's tested from 2 to 50 is

    min(kerrors)

    ## [1] 61011.47

A plot of the RMSE for various K's can be seen below. The optimal range
for K appears to be between 10 and 20.

    ggplot(data = df_knn) + 
      geom_point(mapping = aes(x = K, y = kerrors)) + labs(
        title = "RMSE's versus K for Predicting Housing Prices",
        x = "K",
        y = "RMSE")

![](HW2_files/figure-markdown_strict/unnamed-chunk-8-1.png)

The above results show that the "hand-built" model performs the best out
of sample. The KNN approach performs better than the "medium" model but
performs slightly worse compared to the "hand-built" model.

Hospital Audit
--------------

In order to determine which radiologists are more conservative when
controlling for other risk factors we built a logit model predicting
recall rates. Various models were tested including different features to
determine the most robust model for predicting recall rates. All of the
models included the radiologist dummy variables to determine which
radiologist was the most conservative.

The following models were tested:

Model 1: age + history + symptoms + menopause + density + radiologist
Model 2: history + symptoms + menopause + density + radiologis Model 3:
age + history + symptoms + density + radiologist Model 4: history +
symptoms + density + radiologist Model 5: age + symptoms + menopause +
density + radiologist Model 6: symptoms + density + radiologist

The out of sample RMSEs were tested for each of the models to select the
most robust model to predict recall rates. As seen from the RMSEs below
model 6 had the best out of sample RMSE of all models tested.

Model 1 RMSE:

    avgrmse1

    ## [1] 2.143305

Model 2 RMSE:

    avgrmse2

    ## [1] 2.137975

Model 3 RMSE:

    avgrmse3

    ## [1] 2.122685

Model 4 RMSE:

    avgrmse4

    ## [1] 2.11536

Model 5 RMSE:

    avgrmse5

    ## [1] 2.138307

Model 6 RMSE:

    avgrmse6

    ## [1] 2.11095

The model results for model 6 are below.

    auditmodel6 = glm(recall ~ symptoms + density + radiologist, data=brca, family ='binomial')
    summary(auditmodel6)

    ## 
    ## Call:
    ## glm(formula = recall ~ symptoms + density + radiologist, family = "binomial", 
    ##     data = brca)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -0.9932  -0.6145  -0.5201  -0.4061   2.7310  
    ## 
    ## Coefficients:
    ##                          Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)               -3.1833     0.5540  -5.746 9.16e-09 ***
    ## symptoms                   0.7357     0.3543   2.076  0.03786 *  
    ## densitydensity2            1.2510     0.5374   2.328  0.01991 *  
    ## densitydensity3            1.5235     0.5295   2.877  0.00401 ** 
    ## densitydensity4            1.1599     0.5872   1.975  0.04823 *  
    ## radiologistradiologist34  -0.5214     0.3264  -1.598  0.11015    
    ## radiologistradiologist66   0.3610     0.2751   1.312  0.18942    
    ## radiologistradiologist89   0.4742     0.2775   1.709  0.08752 .  
    ## radiologistradiologist95  -0.0282     0.2914  -0.097  0.92292    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 834.25  on 986  degrees of freedom
    ## Residual deviance: 805.07  on 978  degrees of freedom
    ## AIC: 823.07
    ## 
    ## Number of Fisher Scoring iterations: 5

As seen above, when controlling for factors such as symptoms and
density, the coefficient for radiologist89 is the largest amongst the
dummy variables for the five radiologists. The odds of a patient being
recalled for the radiologist89, holding all else equal is increased by:

    probrad89 = as.numeric(auditmodel6$coef[8])
    prob = exp(probrad89)
    prob

    ## [1] 1.606749

The data was analyzed also to determine if there are certain factors
that should considered more heavily when determining the decision to
recall a patient. In this exercise cancer was regressed against recall
rates. In addition, various models were tested to determine if cancer
outcomes could be better predicted using other factors. The following
models were tested:

Model 1: recall Model 2: recall + age + history + symptoms + menopause +
density + radiologist Model 3: recall + age70plus + density4 Model 4:
recall + age + density Model 5: symptoms + density + age

The out of sample RMSEs were tested for each of the models to select the
most robust model to predict cancer outcomes. As seen from the RMSEs
below model 1 had the best out of sample RMSE of all models tested.

Model 1 RMSE:

    avgrmse1

    ## [1] 3.805958

Model 2 RMSE:

    avgrmse2

    ## [1] 4.814619

Model 3 RMSE:

    avgrmse3

    ## [1] 3.968904

Model 4 RMSE:

    avgrmse4

    ## [1] 4.691235

Model 5 RMSE:

    avgrmse5

    ## [1] 4.218943

The model results for model 1 are below.

    audit1 = glm(cancer ~ recall, data=brca, family ='binomial')
    summary(audit1)

    ## 
    ## Call:
    ## glm(formula = cancer ~ recall, family = "binomial", data = brca)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -0.5673  -0.1900  -0.1900  -0.1900   2.8370  
    ## 
    ## Coefficients:
    ##             Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)  -4.0061     0.2605 -15.378  < 2e-16 ***
    ## recall        2.2609     0.3482   6.493 8.43e-11 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 315.59  on 986  degrees of freedom
    ## Residual deviance: 274.88  on 985  degrees of freedom
    ## AIC: 278.88
    ## 
    ## Number of Fisher Scoring iterations: 6

The results of the analysis indicate that there aren't additional
factors that should be weighed in order to better predict cancer
outcomes.

Predicting when articles go viral
---------------------------------

In order to predict if an article goes viral several linear regression
models were tested to determine which model was the most accurate. The
models tested were the following:

Model 1: avg\_positive\_polarity + avg\_negative\_polarity +
global\_rate\_positive\_words + global\_rate\_negative\_words +
self\_reference\_avg\_sharess Model 2: avg\_negative\_polarity +
self\_reference\_avg\_sharess + num\_imgs + num\_videos Model 3:
avg\_negative\_polarity + self\_reference\_avg\_sharess + num\_imgs +
num\_videos +n\_tokens\_title + n\_tokens\_content Model 4:
avg\_negative\_polarity + self\_reference\_avg\_sharess + num\_imgs +
num\_videos + n\_tokens\_content + weekday\_is\_monday +
weekday\_is\_tuesday + weekday\_is\_wednesday + weekday\_is\_thursday +
weekday\_is\_friday + weekday\_is\_saturday Model 5:
avg\_negative\_polarity + self\_reference\_avg\_sharess + num\_imgs +
num\_videos + n\_tokens\_content

The best model tested was model 5.

The out of sample confusion matrix for the model is below:

    confusion

    ##          0        1
    ## 0    0.924    2.230
    ## 1    2.230 3910.880

The TPR, FPR, and FDR out of sample accuracy measures are below for
model 5:

    tpr

    ## [1] 0.9994301

    fpr

    ## [1] 0.9997699

    fdr

    ## [1] 0.0005698792

The overall accuracy rate is:

    sum(diag(confusion))/sum(confusion)

    ## [1] 0.9988612

The absolute improvement to the null model is:

    absolute

    ##         0 
    ## 0.4983818

The relative improvatment to the null model is:

    relative

    ##        0 
    ## 1.995809

An alternative approach to predict if an article goes viral was tested
using a logistic regression model. Several models were tested to
determine which model was the most accurate. The models tested were the
following:

Model 1: avg\_positive\_polarity + avg\_negative\_polarity +
global\_rate\_positive\_words + global\_rate\_negative\_words +
self\_reference\_avg\_sharess

Model 2: avg\_negative\_polarity + self\_reference\_avg\_sharess +
num\_imgs + num\_videos

Model 3: avg\_negative\_polarity + self\_reference\_avg\_sharess +
num\_imgs + num\_videos +n\_tokens\_title + n\_tokens\_content

Model 4: avg\_negative\_polarity + self\_reference\_avg\_sharess +
num\_imgs + num\_videos + n\_tokens\_content + weekday\_is\_monday +
weekday\_is\_tuesday + weekday\_is\_wednesday + weekday\_is\_thursday +
weekday\_is\_friday + weekday\_is\_saturday

Model 5: avg\_negative\_polarity + self\_reference\_avg\_sharess +
num\_imgs + num\_videos + n\_tokens\_content

Model 6:avg\_negative\_polarity + avg\_positive\_polarity +
self\_reference\_avg\_sharess + num\_imgs + num\_videos +
n\_tokens\_content + n\_tokens\_title + weekday\_is\_monday +
weekday\_is\_tuesday + weekday\_is\_wednesday + weekday\_is\_thursday +
weekday\_is\_friday + weekday\_is\_saturday

The best model tested was model 6.

The out of sample confusion matrix for the model is below:

    confusion

    ##          0        1
    ## 0 3706.812 3258.858
    ## 1 3258.858  654.630

The TPR, FPR, and FDR out of sample accuracy measures are below for
model 5:

    tpr

    ## [1] 0.1672753

    fpr

    ## [1] 0.07687687

    fdr

    ## [1] 0.8327247

The overall error rate is:

    sum(diag(confusion))/sum(confusion)

    ## [1] 0.4008989

The absolute improvement to the null model is:

    absolute

    ##           0 
    ## -0.09958592

The relative improvatment to the null model is:

    relative

    ##         0 
    ## 0.8010211

The threshold first and then regress approach performs much worse
compared to the regress first and then threshold approach. This may be
due to the linear regression performing better at predicting the number
of shares compared to estimating the probability of an article going
viral based on a somewhat arbitrary cutoff.
