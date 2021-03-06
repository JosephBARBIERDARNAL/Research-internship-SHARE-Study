# Research project on the [SHARE Study](http://www.share-project.org/home0.html)

I am currently doing a research intership in analysis of epidemiological data from the [SHARE Study](http://www.share-project.org/home0.html).
My subject is "Analysis of epidemiological data : relationship between socioeconomic status, risk behaviors and cancer incidence".

I have access to a sample size of n=46733, which allows me to have a high statistical power and a lot of information to exploit. 

The goal is simply to explore as much as possible the available data, via various statistical and learning methods. So far I did the descriptive statistics, some basics tests (chi-square and Student's test) to see if there are significant first differences in cancer incidence for each variable and logistic regressions (using the stepwise algorithm) to see which variables are the most predictive of cancer incidence. The next step is to perform clustering analysis (using k-prototypes algorithm, as proposed by [Huang in 1998](https://link.springer.com/article/10.1023/A:1009769707641)).

I will put the code (and the results) I used for the analysis as soon as I finish and clean it up. Most of it is already posted.

I try to answer theses questions: What is the impact of socioeconomic status and risk behaviors on cancer incidence ? Are there profile categories in risk behaviors and socioeconomic status that have different cancer prevalence ? Spoiler : yes, apparently. 

IMPORTANT : I am publishing here only the results of the statistical analysis, not everything that was done for this research. Indeed, I omit here the literature review carried out beforehand as well as the general description of the collection of raw data (how and where were the questionnaires made? what is the population? Etc). Also, the results should be interpreted sparingly and put in the context of the original data. Finally, these results are not a substitute for peer-reviewed research papers (which is not the case here) on the same subject.






# Description of the variables used

## 1 - Income (quantitative)

Last year's annual income after payment of taxes (converted in euro). I transformed this variable into a z-score. 
### $z_i = \frac{X_i - \bar{X}}{??}$

With:

$X_i$ = The income of individual i

$\bar{X}$ = The average income of the individual's country

?? = The standard deviation of income from the mean of individual i's country

Mean = 0, SD = 1

## 2 - UPA (quantitative)

A score that represents an individual's total cigarette consumption. A score of X is interpreted as follows: Individual i has consumed X packs of cigarettes per day for one year OR has consumed 1 pack of cigarettes per day for X years. 
### $UPA = \frac{N \times Q}{20}$

With:

Q = The total amount of time the person has smoked throughout their life (in years)

N = The number of cigarettes consumed per day, on average

20 = The average number of cigarettes in a pack

Mean = 22, SD = 17

## 3 - Alcool (quantitative)

The average number of units of alcohol consumed per week. 

Mean = 6.4, SD = 6.9

## 4 - Children (quantitative)

The number of children alive at the time of the questionnaire.

Mean = 2, SD = 1

## 5 - Social aids (qualitative and dichotomic) 

The fact of receiving, or not, social assistance such as poverty reliefs, child benefits or housing allowances. 

Yes = 4.75%, No = 95.25%

## 6 - Frequency of sport (moderate and vigorous, both qualitatives with the same modalities)

These 2 variables have 5 different modalities (respectively : moderate and vigorous):

More than 1/week (63.26% and 30.53%) ; 1/week (14.61% and 14.39%) ; 1-3/month (7.14% and 10.81%) ; Less than 1/month (14.98% and 44.27%)

## 7 - Education (measured with the ISCED-2011 index ; qualitative)

This index has 9 differents modalities, from early childhood education to getting a Ph.D.

I declined it in 3 modalities: low (32.34%), medium (39.17%) and high (28.50%), as described [here](https://ec.europa.eu/eurostat/statistics-explained/index.php?title=International_Standard_Classification_of_Education_(ISCED)).

## 8 - Marital status (qualitative)

This variable has 6 different modalities:

Maried and living together (47.9%) ; Maried but don't live together (0.34%) ; Divorced (5.67%) ; Widowed (40.86%) ; Registred partership (1.31%) ; Never maried (3.91%)

## 9 - Cancer incidence

If individuals say that a doctor has ever told them that they have/had cancer, then the [SHARE Study](http://www.share-project.org/home0.html) considers these people to have cancer.

Yes = 5.42%, No = 94.58%




# Missing values 

Because there was a lot of missing values, I have decided to fill them in. Main problem: I have a mixed data-type and most of the imputation's algorithms do not overcome this problem. So I have decided to use a random forest algorithm who predicts the missing values with the observed values (if we summarize a lot...). It is based on a research paper from D. Stekhoven and P. B??hlmann published [here](https://academic.oup.com/bioinformatics/article/28/1/112/219101). 

This imputation has a different interests: it does not require any particular distribution of variables (because it uses random forest as a model: i.e non-parametric) and works for mixed data sets. 



# Relationship between cancer incidence and each variable

Here are the tests I did. This is not the main part of the analysis but I consider it as a good start when doing data analysis. All tests were done for each variable in relation to the cancer incidence and see if there were significant differences (at the p<0.05 risk level). I also calculate the Cohen's d and Cramer's V for the significant tests.

## 1 - Quantitatives variables (Student's test or Welch's test when there was detection of heteroskedasticity)

Income: p=0.75

UPA's score: p<0.001* ; d=-0.126 (small size effect)

Alcool: p=0.47

Children: p=0.03* ; d=-0.044 (small size effect)

## 2 - Qualitative variables (Chi-square's test with Yates's correction if necessary)

Social aids (housing allowances, poverty reliefs etc): p=0.49

Frequency of vigorous physical activity: p<0.001* ; v=0.07 (small size effect)

Frequency of moderate physical activity: p<0.001* ; v=0.058 (small size effect)

Education (ISCED-2011): p=0.014* ; v=0.013 (small size effect)

Marital status: p<0.001* ; v=0.022 (small size effect)






# Logistic regression

Here you will find the logistic regression model before and after applying the stepwise algorithm (using backward elimination via the information's criterion AIC). I present here the significativity of the coefficients of the models. For the second regression, I go into more detail with the odds ratios as well as the confidence intervals (95%) of the latter, for each variable.

The first regression with all the variables

<img width="1570" alt="Screenshot 2022-07-19 at 16 25 38" src="https://user-images.githubusercontent.com/79746670/179774717-d967d6c1-3006-4119-96a4-04744519b71a.png">

The new regression after applying the stepwise algorithm

<img width="1566" alt="Screenshot 2022-07-19 at 16 26 15" src="https://user-images.githubusercontent.com/79746670/179774822-1a8985d2-86e7-4082-82b2-27fa89bec90b.png">

## 1 - Marital status (reference modality : Married and live together)

Divorced: p<0.001 ; OR=0.65 [0.52 - 0.79]

Never married: p=0.002 ; OR=0.70 [0.54 - 0.89]

Married but not living together: p=0.782 ; OR=0.91 [0.43 - 1.70]

Registred relationship: p=0.938 ; OR=0.99 [0.68 - 1.39]

Widowed: p<0.001 ; OR=0.83 [0.76 - 0.91]

## 2 - Educational level (reference modality : Low)

Medium: p<0.001 ; OR=1.21 [1.09 - 1.34]

High: p<0.001 ; OR=1.53 [1.37 - 1.71]

## 3 - UPA's score

UPA: p<0.001 ; OR=1.01 [1.00 - 1.01]

## 4 - Sport (reference modality: Less than 1/month, for moderate and vigorous physical activity)

1-3/month vigorous physical activity: p<0.001 ; OR=0.56 [0.48 - 0.66]

1-3/month moderate physical activity: p<0.001 ; OR=0.72 [0.60 - 0.85]

1/week vigorous physical activity: p<0.001 ; OR=0.57 [0.50 - 0.66]

1/week moderate physical activity: p<0.001 ; OR=0.65 [0.56 - 0.75]

More than 1/week vigorous physical activity: p<0.001 ; OR=0.55 [0.50 - 0.62]

More than 1/week moderate physical activity: p<0.001 ; OR=0.70 [0.62 - 0.78]

# Clustering using k-prototypes algorithm

## 1 - Determination of k 

In order to determine the number k of clusters I will have, I used the elbow method. I have calculated the total wihtinss for 1 to 10 clusters and create this plot in order the choose the optimal number of k. However, it does not seem to have an obvious solution, so I choosed k=3. It would have been perfectly possible to choose a different k. 

<img width="1723" alt="elbow clusters" src="https://user-images.githubusercontent.com/79746670/179923679-17ff7436-05bf-4c18-8a73-c13d443cd112.png">

## 2 - Results

Cluster 1 : n = 8514 

Cluster 2 : n = 17292

Cluster 3 : n = 20927

I present below the caracteristics of the 3 clusters for each variable with a plot. 

![image](https://user-images.githubusercontent.com/79746670/179924102-63bed09d-b926-4d5f-9677-1c73c92c1c1f.png)

![image](https://user-images.githubusercontent.com/79746670/179924412-7f0b05a3-e977-4dd5-bba1-e56282260065.png)

![image](https://user-images.githubusercontent.com/79746670/179924436-21aac140-c620-4954-b1c0-3dbf97eb0e40.png)

![image](https://user-images.githubusercontent.com/79746670/179924456-95b50a52-5ea4-4451-b15f-bfdfaf32cd0f.png)

![image](https://user-images.githubusercontent.com/79746670/179924474-571a99ab-f4fb-4791-ab89-0f8ccf21a762.png)

![image](https://user-images.githubusercontent.com/79746670/179924487-7d54e178-147e-4e6f-9f43-03d992a89a7f.png)

![image](https://user-images.githubusercontent.com/79746670/179924497-0efed876-dd4f-4275-9816-e92337451dc8.png)

![image](https://user-images.githubusercontent.com/79746670/179924519-6a66f282-b23c-4fb8-bf57-eb5ab1a1df71.png)

![image](https://user-images.githubusercontent.com/79746670/179924559-5d12decc-6827-4f01-b931-07b955ea04b7.png)

![image](https://user-images.githubusercontent.com/79746670/179924578-6f58bf0a-40bb-4e31-a46b-2b8567dcf2a9.png)

## 3 - Description

I present here the carcateristics of each cluster for each variable. The modalities in the same colour are for the same variable. The figures in bold are just the ones >50% for a modality. Quantitative variables are represent as follows: mean (??sd).

<img width="867" alt="Screenshot 2022-07-21 at 15 25 48" src="https://user-images.githubusercontent.com/79746670/180224885-84c6e5d6-d058-4d9a-b105-5e597af8746f.png">

## 4 - Interpretation

### Cluster 1

The first cluster (green/turquoise) refers to individuals with the following characteristics:

- higher alcohol consumption

- higher UPA's score 

- rarely participate in high-intensity sports and only slightly in low-intensity sports 

- a low or medium level of education

- mostly widowed 
 
- higher income 

- have more children

- slightly more often on social assistance

- higher incidence of cancer

### Cluster 2

The second cluster (yellow) refers to individuals with the following characteristics

- lower alcohol consumption 

- lower UPA's score 

- lower income 

- a majority of them rarely practice high-intensity sports and a majority of them regularly practice low-intensity sports

- a low level of education for the most part

- almost exclusively widowed

### Cluster 3

The third cluster (purple) designates individuals with the following characteristics

- lower alcool consumption than cluster 1 but superior than cluster 3

- a predominantly regular practice of sport, at low or high intensity

- a medium or high level of education

- lower income 

- less children 

- almost exclusively married and living with their partner

- slightly less likely to receive social assistance

- a lower incidence of cancer















