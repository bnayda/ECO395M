Clustering and PCA
------------------

We can use PCA to determine the color of wine based on the chemical
properties. Below is a plot of two components between red wine and white
wine.

    qplot(scores[,1], scores[,2], color=data$color, xlab='Component 1', ylab='Component 2')

![](HW4_DM_files/figure-markdown_strict/unnamed-chunk-2-1.png)

White wines have more positive component 1 values and red wines have
more negative component 1 values.

Another method to determine the color of the wine based on the chemical
properties is using clustering analysis.

The plot below shows the clustering between red and white wines.

    qplot(total.sulfur.dioxide, residual.sugar, data=data, color=factor(clust1$cluster))

![](HW4_DM_files/figure-markdown_strict/unnamed-chunk-4-1.png)

    qplot(free.sulfur.dioxide, residual.sugar, data=data, color=factor(clust1$cluster))

![](HW4_DM_files/figure-markdown_strict/unnamed-chunk-5-1.png)

    qplot(free.sulfur.dioxide, total.sulfur.dioxide, data=data, color=factor(clust1$cluster))

![](HW4_DM_files/figure-markdown_strict/unnamed-chunk-6-1.png)

The above plots show that it is difficult to develop strongly distinct
clusters using clustering analysis. As a result, PCA is the better
dimensionality reduction technique. Next I attempted to use PCA to
segment the quality of the wine. The plots below there is some distinct
segmentation between low and high quality wines for some components and
less so between others.

    qplot(scores[,1], scores[,2], color=data$quality, xlab='Component 1', ylab='Component 2')

![](HW4_DM_files/figure-markdown_strict/unnamed-chunk-8-1.png)

    qplot(scores[,1], scores[,3], color=data$quality, xlab='Component 1', ylab='Component 3')

![](HW4_DM_files/figure-markdown_strict/unnamed-chunk-9-1.png)

    qplot(scores[,2], scores[,4], color=data$quality, xlab='Component 2', ylab='Component 4')

![](HW4_DM_files/figure-markdown_strict/unnamed-chunk-10-1.png)

    qplot(scores[,1], scores[,5], color=data$quality, xlab='Component 1', ylab='Component 5')

![](HW4_DM_files/figure-markdown_strict/unnamed-chunk-11-1.png)

Market Segmentation
-------------------

I conducted analysis of Twitter post user data using clustering
techniques. The data was first normalized by computing category post
frequencies. Then using k-means clustering I identified different market
segments. The plots below clusters of different segments that should be
targeted.

Users that have high frequencies of posts about photo\_sharing and
cooking is a segment of twitter users that NutrientH20 should target.

    qplot(cooking, photo_sharing, data=ad_data, color=factor(addclust$cluster))

![](HW4_DM_files/figure-markdown_strict/unnamed-chunk-13-1.png)

Another segment that should be targeted are users that post about health
nutrition and cooking.

    qplot(cooking, health_nutrition, data=ad_data, color=factor(addclust$cluster))

![](HW4_DM_files/figure-markdown_strict/unnamed-chunk-14-1.png)

Association Rules for Grocery Purchases
---------------------------------------

Analyzing baskets of grocery store purchases there can be information
gained from common baskets of items purchased. In order to identify
common items purchased association rules can be applied.

After inspection of the associations it appears only those rules with
lift greater than 6 produce reasonable values. These associations are
listed below.

    inspect(subset(rules, lift > 6))

    ##     lhs                      rhs                   support    confidence
    ## [1] {V4=whole milk}       => {V3=other vegetables} 0.01216004 0.5454545 
    ## [2] {V3=other vegetables} => {V4=whole milk}       0.01216004 0.4217687 
    ## [3] {V3=whole milk}       => {V2=other vegetables} 0.01451360 0.3985637 
    ## [4] {V2=other vegetables} => {V3=whole milk}       0.01451360 0.3580645 
    ## [5] {V1=other vegetables} => {V2=whole milk}       0.01366370 0.3584906 
    ## [6] {V2=whole milk}       => {V1=other vegetables} 0.01366370 0.2812921 
    ##     lift      count
    ## [1] 18.918986 186  
    ## [2] 18.918986 186  
    ## [3]  9.832953 222  
    ## [4]  9.832953 222  
    ## [5]  7.380177 209  
    ## [6]  7.380177 209
