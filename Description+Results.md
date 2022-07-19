# Research internship on the SHARE Study (see [SHARE Project](http://www.share-project.org/home0.html))
I am currently doing analysis of epidemiological data from the SHARE Study.
My subject is "Analysis of epidemiological data : relationship between socioeconomic status, risk behaviors and cancer incidence".

I have access to a sample size of n=46733, which allows me to have a high statistical power and a lot of information to exploit. 

The goal is simply to explore as much as possible the available data, via various statistical and learning methods. So far I did the descriptive statistics, some basics tests (chi-square and Student's test) to see if there are significant first differences in cancer incidence for each variable and logistic regressions (using the stepwise algorithm) to see which variables are the most predictive of cancer incidence. The next step is to perform clustering analysis (using k-prototyps algorithm, as proposed by Huang in 1998).

I will put the code (and the results !) I used for the analysis as soon as I finish and clean it up.





# Descriptive statistics

Here are the descriptives statistics of my data.
PS : I didn't have time to translate the name of the variables but I will do it soon.

The quantitative variables are presented via a bivariate (in relation to cancer) and univariate descriptive analysis. The given values represent the mean and standard deviation in the following form : mean (± sd). I emphasize that the income variable is here a z-score.

The qualitative variables are only presented via a univariate descriptive analysis. The percentages refer to the proportion of my sample that belongs to the modality in question.



<img width="877" alt="Screenshot 2022-07-19 at 16 21 31" src="https://user-images.githubusercontent.com/79746670/179773702-b9e40a31-ea18-4283-aa1b-88fd8eeb5ffc.png">
<img width="878" alt="Screenshot 2022-07-19 at 16 21 49" src="https://user-images.githubusercontent.com/79746670/179773770-867cf194-38d7-404c-9c25-e06d72c24352.png">
<img width="878" alt="Screenshot 2022-07-19 at 16 22 01" src="https://user-images.githubusercontent.com/79746670/179773823-cccf133b-116a-4602-ad90-376174a96127.png">
<img width="878" alt="Screenshot 2022-07-19 at 16 22 16" src="https://user-images.githubusercontent.com/79746670/179773887-dc442ffe-860c-41d5-9cb9-a1afe21b0fae.png">
<img width="878" alt="Screenshot 2022-07-19 at 16 22 30" src="https://user-images.githubusercontent.com/79746670/179773944-afaed64d-5c8c-4332-a682-b2ca50eaceac.png">




# Inferential statistics

Here are the test I did. This is not the main part of the analysis but I consider it as a good start when doing data analysis. All tests were done for each variable in relation to the cancer incidence and see if there were significant differences (at the p<0.05 risk level). I also calculate the Cohen's d and Cramer's V for the significant tests.

## 1 - Quantitatives variables (Student's test or Welch's test when there was detection of heteroskedasticity)

Income : p=0.75

UPA's score (≈ cigarettes consumption during life) : p<0.001* ; d=-0.126 (small size effect)

Alcool : p=0.47

Children : p=0.03* ; d=-0.044 (small size effect)

## 2 - Qualitative variables (Chi-square's test with Yates's correction if necessary)

Social aids (housing allowances, poverty reliefs etc) : p=0.49

Frequency of vigorous physical activity : p<0.001* ; v=0.07 (small size effect)

Frequency of moderate physical activity : p<0.001* ; v=0.058 (small size effect)

Education (ISCED-2011) : p=0.014* ; v=0.013 (small size effect)

Marital status : p<0.001* ; v=0.022 (small size effect)





# Logistic regression

Here you will find the logistic regression model before and after applying the stepwise algorithm. I present here the significativity of the coefficients of the models. For the second regression, I go into more detail with the odds ratios as well as the confidence intervals (95%) of the latter, for each variable.

The first regression with all the variables
<img width="1570" alt="Screenshot 2022-07-19 at 16 25 38" src="https://user-images.githubusercontent.com/79746670/179774717-d967d6c1-3006-4119-96a4-04744519b71a.png">

The new regression after applying the stepwise algorithm
<img width="1566" alt="Screenshot 2022-07-19 at 16 26 15" src="https://user-images.githubusercontent.com/79746670/179774822-1a8985d2-86e7-4082-82b2-27fa89bec90b.png">

## 1 - Marital status (reference modality : Married and live together)

Divorced : p<0.001 ; OR=0.65 [0.52 - 0.79]

Never married : p=0.002 ; OR=0.70 [0.54 - 0.89]

Married but not living together : p=0.782 ; OR=0.91 [0.43 - 1.70]

Registred relationship : p=0.938 ; OR=0.99 [0.68 - 1.39]

Widowed : p<0.001 ; OR=0.83 [0.76 - 0.91]

## 2 - Educational level (reference modality : Low)

Medium : p<0.001 ; OR=1.21 [1.09 - 1.34]

High : p<0.001 ; OR=1.53 [1.37 - 1.71]

## 3 - UPA's score

UPA : p<0.001 ; OR=1.01 [1.00 - 1.01]

## 4 - Sport (reference modality : Less than 1/month, for moderate and vigorous physical activity)

1-3/month vigorous physical activity : p<0.001 ; OR=0.56 [0.48 - 0.66]

1-3/month moderate physical activity : p<0.001 ; OR=0.72 [0.60 - 0.85]

1/week vigorous physical activity : p<0.001 ; OR=0.57 [0.50 - 0.66]

1/week moderate physical activity : p<0.001 ; OR=0.65 [0.56 - 0.75]

More than 1/week vigorous physical activity : p<0.001 ; OR=0.55 [0.50 - 0.62]

More than 1/week moderate physical activity : p<0.001 ; OR=0.70 [0.62 - 0.78]

# Clustering using k-prototypes algorithm

Coming soon.





















