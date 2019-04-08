Green Buildings
---------------

Two approaches were tested in order to develop the best model to predict
the rent of a building. The first approach uses Lasso in order to select
the best model. The second approach uses stepwise approach to identify
the best predictive model. The data was modified before conducting both
modeling approaches. First all buildings with leasing rates below 10
were excluded from the data set because these outliers could affect
model estimation. In addition, the effect of either LEED or Energystar
green energy certification was not isolated and thus dropped from the
data set. Only the effect of a green rating certification was examined
during the analysis.

The Lasso model approach identified the model with the lowest AIC. The
resulting model coefficients are shown below.

    coef(sclasso)

    ## 18 x 1 sparse Matrix of class "dgCMatrix"
    ##                          seg100
    ## intercept         -4.255153e+00
    ## size               5.774489e-06
    ## empl_gr            1.205468e-02
    ## leasing_rate       3.914338e-03
    ## stories            .           
    ## age               -1.036928e-02
    ## renovated         -1.092966e-01
    ## class_a            1.884364e+00
    ## class_b            2.570854e-01
    ## green_rating       4.201310e-01
    ## net               -1.794333e+00
    ## amenities          3.865451e-01
    ## cd_total_07       -1.070062e-04
    ## hd_total07         2.473604e-04
    ## total_dd_07        .           
    ## Gas_Costs         -1.355128e+02
    ## Electricity_Costs  9.027255e+01
    ## cluster_rent       1.035996e+00

The stepwise approach was conducted using a forward stepwise in order to
identify the best model by AIC.

The forward stepwise identified the following model.

    summary(lm_forward)

    ## 
    ## Call:
    ## lm(formula = Rent ~ cluster_rent + size + class_a + class_b + 
    ##     cd_total_07 + age + net + empl_gr + Electricity_Costs + leasing_rate + 
    ##     green_rating + amenities + cluster_rent:size + cd_total_07:net + 
    ##     class_b:age + class_a:age + cluster_rent:Electricity_Costs + 
    ##     size:Electricity_Costs + size:cd_total_07 + class_a:empl_gr + 
    ##     cluster_rent:age + age:Electricity_Costs + size:leasing_rate + 
    ##     size:class_a + cluster_rent:leasing_rate + cluster_rent:net + 
    ##     green_rating:amenities + cd_total_07:age + cluster_rent:class_a + 
    ##     cluster_rent:class_b + Electricity_Costs:amenities + cluster_rent:amenities + 
    ##     size:class_b + size:age + size:amenities + class_b:amenities + 
    ##     cluster_rent:cd_total_07 + empl_gr:Electricity_Costs + size:empl_gr + 
    ##     age:green_rating, data = greenbuild)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -55.746  -3.518  -0.590   2.531 156.338 
    ## 
    ## Coefficients:
    ##                                  Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)                     3.130e+00  2.555e+00   1.225 0.220626    
    ## cluster_rent                    7.720e-01  8.306e-02   9.295  < 2e-16 ***
    ## size                           -1.116e-05  4.951e-06  -2.255 0.024162 *  
    ## class_a                         9.794e+00  1.515e+00   6.466 1.07e-10 ***
    ## class_b                         7.012e+00  1.347e+00   5.207 1.97e-07 ***
    ## cd_total_07                     6.630e-04  4.647e-04   1.427 0.153703    
    ## age                             4.080e-02  1.770e-02   2.306 0.021157 *  
    ## net                            -5.864e-01  1.804e+00  -0.325 0.745189    
    ## empl_gr                         7.655e-01  3.696e-01   2.071 0.038351 *  
    ## Electricity_Costs              -1.901e+02  6.182e+01  -3.074 0.002116 ** 
    ## leasing_rate                   -5.417e-02  1.991e-02  -2.721 0.006524 ** 
    ## green_rating                    1.518e+00  9.203e-01   1.649 0.099123 .  
    ## amenities                      -1.837e+00  1.031e+00  -1.781 0.074952 .  
    ## cluster_rent:size               4.703e-07  4.794e-08   9.811  < 2e-16 ***
    ## cd_total_07:net                 9.873e-04  4.174e-04   2.365 0.018047 *  
    ## class_b:age                    -4.712e-02  1.109e-02  -4.249 2.18e-05 ***
    ## class_a:age                    -3.467e-02  1.574e-02  -2.202 0.027705 *  
    ## cluster_rent:Electricity_Costs  5.898e+00  1.499e+00   3.934 8.43e-05 ***
    ## size:Electricity_Costs          2.169e-04  7.267e-05   2.984 0.002850 ** 
    ## size:cd_total_07               -1.746e-09  4.539e-10  -3.848 0.000120 ***
    ## class_a:empl_gr                 5.466e-02  3.037e-02   1.800 0.071917 .  
    ## cluster_rent:age               -2.507e-03  5.045e-04  -4.969 6.86e-07 ***
    ## age:Electricity_Costs           1.857e+00  5.254e-01   3.535 0.000411 ***
    ## size:leasing_rate               1.189e-07  3.280e-08   3.626 0.000290 ***
    ## size:class_a                   -1.310e-05  3.593e-06  -3.646 0.000268 ***
    ## cluster_rent:leasing_rate       1.929e-03  6.935e-04   2.781 0.005429 ** 
    ## cluster_rent:net               -1.115e-01  5.581e-02  -1.997 0.045807 *  
    ## green_rating:amenities         -2.157e+00  8.352e-01  -2.583 0.009811 ** 
    ## cd_total_07:age                -8.407e-06  4.056e-06  -2.073 0.038204 *  
    ## cluster_rent:class_a           -1.256e-01  4.265e-02  -2.946 0.003234 ** 
    ## cluster_rent:class_b           -8.654e-02  3.606e-02  -2.400 0.016410 *  
    ## Electricity_Costs:amenities     1.049e+02  3.269e+01   3.207 0.001345 ** 
    ## cluster_rent:amenities         -5.997e-02  2.707e-02  -2.215 0.026797 *  
    ## size:class_b                   -9.205e-06  3.451e-06  -2.667 0.007664 ** 
    ## size:age                       -4.242e-08  2.156e-08  -1.967 0.049184 *  
    ## size:amenities                  2.616e-06  1.197e-06   2.186 0.028870 *  
    ## class_b:amenities               9.489e-01  5.211e-01   1.821 0.068653 .  
    ## cluster_rent:cd_total_07       -3.091e-05  1.643e-05  -1.882 0.059913 .  
    ## empl_gr:Electricity_Costs      -3.269e+01  1.560e+01  -2.096 0.036114 *  
    ## size:empl_gr                    1.458e-07  1.019e-07   1.431 0.152509    
    ## age:green_rating                3.308e-02  2.316e-02   1.428 0.153277    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 9.116 on 7620 degrees of freedom
    ## Multiple R-squared:  0.6392, Adjusted R-squared:  0.6373 
    ## F-statistic: 337.4 on 40 and 7620 DF,  p-value: < 2.2e-16

To determine which approach was the most robust the out of sample RMSE
were calculated.

The out-of-sample RMSE for the Lasso approach is:

    avgrmse1

    ## [1] 9.520651

The out-of-sample RMSE for the stepwise approach is:

    avgrmse2

    ## [1] 8.952263

As a result, the best model is the model identified using the stepwise
approach which has the lower out of sample RMSE. Using the stepwise
model we can determine the effect of a green building certification on
rents. The average building has amenities and is 46.95 years old. Thus
an average building holding all other variables constant, has rents that
are $0.91/sqft higher. This model also shows us that the green rating
certification effect is different for buildings that have amenities and
those of different ages. A building with a green rating certification
and has amenities has rents that are $2.16/sqft less than buildings
without a green rating certification. In addition, a building that has a
green rating certification increases rents the older the building is.

What Causes What?
-----------------

1.  Why can’t I just get data from a few different cities and run the
    regression of “Crime” on “Police” to understand how more cops in the
    streets affect crime? (“Crime” refers to some measure of crime rate
    and “Police” measures the number of cops in a city.)

A number of factors could influence crime and often more crime results
in policies that increase the number of police presence to combat crime.
As a result, there is an endogeniety problem that prevents us from being
able to statistically determine if more police impacts crime rates.

1.  How were the researchers from UPenn able to isolate this effect?
    Briefly describe their approach and discuss their result in the
    “Table 2” below, from the researcher's paper.

In order to isolate this effect they analyzed days in DC where there
were high alerts that resulted in increased police presence due to
terrorism concerns. As a result, the increased police was independent of
rates of crime and thus could be used to determine if the increased
police presence resulted in decreased crime rates on days there were
high alerts. The researchers found that the increased police presence on
high alert days resulted in decreased crime rates. They also found that
changes in the number of tourists and citizens traveling throughout the
city did not impact crime rates. Therefore, this shows that the
increased police presence was responsible for decreased crime rates.

1.  Why did they have to control for Metro ridership? What was that
    trying to capture?

They controlled for Metro ridership to test the hypothesis that on days
when there was a high alert that it did not impact the number of people
going out and traveling throughout the city. If on days with a high
alert there was reduced ridership then a decrease in crime rates could
be due to fewer numbers of victims.

1.  Below I am showing you "Table 4" from the researchers' paper. Just
    focus on the first column of the table. Can you describe the model
    being estimated here? What is the conclusion?

The model estimated includes an interaction between high alert days and
if the crime occured in the first district, an interaction between high
alert days and crime occuring in all other police districts, and metro
ridership. The first police district covers most of the area of the
national mall including high sensitive targets such as the washington
monument, the capitol building, and other museums and art galleries. As
a result, the increased police presence would be concentrated in first
police district which would allows us to determine if increased police
presence directly reduces crime. The model results show that the
coefficient for the interaction between high alert days and crimes in
the first district is negative and statistically significant. Therefore,
it shows that increased police presence does reduce the number of
crimes.
