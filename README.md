# Covid-19 Prediction

## Background
On 31 December 2019, the World Health Organization (WHO) was informed of a cluster of cases of pneumonia of unknown cause detected in Wuhan, Hubei Province, China. A novel coronavirus (SARS coronavirus-2 (SARS-CoV-2)) was subsequently identified from patient samples.

Coronaviruses, named for the crown-like spikes on their surfaces, are a large family of viruses that are common in people and many different species of animals, including camels, cattle, cats, and bats. There are many types of human coronaviruses, including some that commonly cause mild upper-respiratory tract illnesses. COVID-19 is a new disease, caused by a novel (or new) coronavirus that has not previously been seen in humans.

![image](https://user-images.githubusercontent.com/45533954/108430269-048d3f00-7239-11eb-8a0d-d6142d65d1ea.png)

As of 06 July 2020 (date of this analysis), the pandemic had spread all over the globe, with nearly 12m cases as shown below:

![image](https://user-images.githubusercontent.com/45533954/108430402-36060a80-7239-11eb-9ffe-1e39d736cf44.png)

![image](https://user-images.githubusercontent.com/45533954/108430646-94cb8400-7239-11eb-9779-7e730d41cd78.png)

## Objective
To predict the spread of the Covid-19 pandemic.

## Data and Model
### Data

The following data is used in this analysis:
- Covid-19 figures from John's Hopkins University by country
- Global population by country including population pyramid to split population by demographics

### Model
We will use SIR-F model that is a customized ODE model derived from SIR model. To evaluate the effect of measures, parameter estimation of SIR-F will be applied to subsets of time series data in each country. Parameter change points will be determined by S-R trend analysis. SIR model is a simple mathematical model to understand outbreak of infectious diseases.  
[The SIR epidemic model - Learning Scientific Programming with Python](https://scipython.com/book/chapter-8-scipy/additional-examples/the-sir-epidemic-model/)

 * S: Susceptible (Population - Confirmed)
 * I: Infected (Confirmed - Recovered - Deaths)
 * R: Recovered or fatal (Recovered + Deaths)
 
Note: This is not the general model! Though R in SIR model is "Recovered and have immunity", I defined "R as Recovered or fatal". This is because mortality rate cannot be ignored in the real COVID-19 data.

![image](https://user-images.githubusercontent.com/45533954/108426207-65197d80-7233-11eb-8ba1-d50308abf911.png)

In the initial phase of COVID-19 outbreak, many cases were confirmed after they died. To consider this issue, "S + I  →  Fatal + I" will be added to the model.

* S: Susceptible (Population - Confirmed)
* S∗: Confirmed and un-categorized
* I: Confirmed and categorized as Infected
* R: Confirmed and categorized as Recovered
* F: Confirmed and categorzied as Fatal

Measurable variables:
Confirmed = I + R + F
Recovered = R 
Deaths = F

![image](https://user-images.githubusercontent.com/45533954/108426763-14565480-7234-11eb-84e1-95c7e0fe6240.png)

Notes on  
S∗ variable:
S∗ describes the cases who are actually carriers of the disease without anyone (including themselves) knowing about it, who either die and they are confirmed positive after death, while some others are moved to infected after being confirmed.

In JHU-style dataset, we know the number of cases who were confirmed with COVID-19, but we do not know the number of died cases who died without COVID-19. Essentially S∗ serves as an auxiliary compartment in SIR-F model to separate the two death situations and insert a probability factor of {α, 1 − α}.

## Results

**Note:** This analysis was performed on 06 July 2020, so figures may be outdated when this is being read.

As you can see below, the prediction for the UK is a little odd since it sppears there are no individuals that recover from Covid-19. This is because the UK did not release recovry figures and so the model assumes no one recovers.

Secondly, for India, the infection figures seem too high since this model predicts nearly 200m people will be infected by COVID. This has occurred due to the large population in India. It can also be seen that the number of deaths is quite low compared to the number of infections which is due to the population demographics, with India being a relatively young nation. Considering the timeline of the prediction, this model predicts that India will be over the worst of the pandemic in early 2021, however, in reality the number of new cases peaked in Q4 2020, which is earlier than predicted.

**Prediction**

UK:

![image](https://user-images.githubusercontent.com/45533954/108425702-b9702d80-7232-11eb-8c5f-f086bf0e1aa1.png)

India:
Prediction:

![image](https://user-images.githubusercontent.com/45533954/108427119-98104100-7234-11eb-829e-a0762010c473.png)

Actual:

![image](https://user-images.githubusercontent.com/45533954/108427353-ef161600-7234-11eb-80f3-a04973808a2a.png)

## Next Steps
As mentioned above, this model is not very accurate nor precise at predicting the spread of the pandemic in the countries tested. However, due to the fluidity of the situation within countries with regards to responses and effectiveness of these as well as global travel links, it would be difficult to model and predict the spread of the disease. Therefore, my next project will be to 'nowcast' more local outbreaks based on Google search and Google mobility report data. 
