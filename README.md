# Research internship on the SHARE Study (see [SHARE Project](http://www.share-project.org/home0.html))
I am currently doing analysis of epidemiological data from the SHARE Study.
My subject is "Analysis of epidemiological data : relationship between socioeconomic status, risk behaviors and cancer incidence".

I have access to a sample size of n=46733, which allows me to have a high statistical power and a lot of information to exploit. 

The goal is simply to explore as much as possible the available data, via various statistical and learning methods. So far I did the descriptive statistics, some basics tests (chi-square and Student's test) to see if there are significant first differences in cancer incidence for each variable and logistic regressions (using the stepwise algorithm) to see which variables are the most predictive of cancer incidence. The next step is to perform clustering analysis (using k-prototyps algorithm, as proposed by Huang in 1998).

I will put the code (and the results !) I used for the analysis as soon as I finish and clean it up.

IMPORTANT : I am publishing here only the results of the statistical analysis, not everything that was done for this research. Indeed, I omit here the literature review carried out beforehand as well as the general description of the collection of raw data (how and where were the questionnaires made? what is the population? Etc). Also, the results should be interpreted sparingly and put in the context of the original data. Finally, these results are not a substitute for peer-reviewed research papers (which is not the case here).

# Description of the variables used

## 1 - Income (quantitative)

Last year's annual income after payment of taxes (converted in euro). I transformed this variable into a z-score. 
### $z_i = \frac{X_i - \bar{X}}{σ}$

With:

$X_i$ = The income of individual i

$\bar{X}$ = The average income of the individual's country

σ = The standard deviation of income from the mean of individual i's country

## 2 - UPA (quantitative)

A score that represents an individual's total cigarette consumption. A score of X is interpreted as follows: Individual i has consumed X packs of cigarettes per day for one year OR has consumed 1 pack of cigarettes per day for X years. 
### $UPA = \frac{N \times Q}{20}$

With:

Q = The total amount of time the person has smoked throughout their life

N = The number of cigarettes consumed per day, on average

20 = The average number of cigarettes in a pack

## 3 - Alcool (quantitative)

The average number of units of alcohol consumed per week. 

## 4 - Children (quantitative)

The number of children alive at the time of the questionnaire.

## 5 - Social aids (qualitative and dichotomic) 

The fact of receiving, or not, social assistance such as poverty reliefs, child benefits or housing allowances. 

## 6 - Frequency of sport (moderate and vigorous, both qualitatives with the same modalities)

These 2 variables have 5 different modalities :

More than 1/week ; 1/week ; 1-3/month ; Less than 1/month.

## 7 Education (measured with the ISCED-2011 index ; qualitative)

This index have 9 differents modalities, from early childhood education to getting a Ph.D.

I declined it in 3 modalities: low, medium and high, as described [here](https://ec.europa.eu/eurostat/statistics-explained/index.php?title=International_Standard_Classification_of_Education_(ISCED).

## 8 - Marital status (qualitative)

This variable has 6 different modalities :

Maried and living together ; Maried but don't live together ; Divorced ; Widowed ; Registred partership ; Never maried

## 9 - Cancer incidence

If individuals say that a doctor has ever told them that they have/had cancer, then the SHARE study considers these people to have cancer.

# Relationship between cancer incidence and each variable

Here are the tests I did. This is not the main part of the analysis but I consider it as a good start when doing data analysis. All tests were done for each variable in relation to the cancer incidence and see if there were significant differences (at the p<0.05 risk level). I also calculate the Cohen's d and Cramer's V for the significant tests.

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




















