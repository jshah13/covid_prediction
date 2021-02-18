# Covid-19 Prediction

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

As you can see below, the prediction for the UK is a little odd since it sppears there are no individuals that recover from Covid-19. This is because the UK did not release recovry figures and so the model assumes no one recovers.

Secondly, for India, the infection figures seem too high since this 

**Prediction**

UK:
![image](https://user-images.githubusercontent.com/45533954/108425702-b9702d80-7232-11eb-8c5f-f086bf0e1aa1.png)

India:
![image](https://user-images.githubusercontent.com/45533954/108425587-904f9d00-7232-11eb-9eed-a21bfbeabf89.png)


## Next Steps
As mentioned above, this model is overly simplistic as it uses the relative rankings of the teams to predict the winner and so in order to progress this model, it would be best to include some other features related to each team's strengths and weaknesses such as the average age, international caps, or some other player specific features such as football manager ratings to establish the quality of the players. Alternatively, we could perform some sentiment analysis based on recent newspaper articles to determine how the world media sees each team's chances (no one predicted Germany to go out that early though!).
