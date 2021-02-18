# Covid-19 Prediction

## Objective
To predict the spread of the Covid-19 pandemic.

## Data and Model
### Data
The data used includes the following sources:
- 

### Model
We will use SIR-F model that is a customized ODE model derived from SIR model. To evaluate the effect of measures, parameter estimation of SIR-F will be applied to subsets of time series data in each country. Parameter change points will be determined by S-R trend analysis.

SIR model is a simple mathematical model to understand outbreak of infectious diseases.  
[The SIR epidemic model - Learning Scientific Programming with Python](https://scipython.com/book/chapter-8-scipy/additional-examples/the-sir-epidemic-model/)

 * S: Susceptible (=All - Confirmed)
 * I: Infected (=Confirmed - Recovered - Deaths)
 * R: Recovered or fatal (=Recovered + Deaths)
 
Note: THIS IS NOT THE GENERAL MODEL!  
Though R in SIR model is "Recovered and have immunity", I defined "R as Recovered or fatal". This is because mortality rate cannot be ignored in the real COVID-19 data.

Model:  
\begin{align*}
\mathrm{S} \overset{\beta I}{\longrightarrow} \mathrm{I} \overset{\gamma}{\longrightarrow} \mathrm{R}  \\
\end{align*}

$\beta$: Effective contact rate [1/min]  
$\gamma$: Recovery(+Mortality) rate [1/min]  

Ordinary Differential Equation (ODE):  
\begin{align*}
& \frac{\mathrm{d}S}{\mathrm{d}T}= - N^{-1}\beta S I  \\
& \frac{\mathrm{d}I}{\mathrm{d}T}= N^{-1}\beta S I - \gamma I  \\
& \frac{\mathrm{d}R}{\mathrm{d}T}= \gamma I  \\
\end{align*}

Where $N=S+I+R$ is the total population, $T$ is the elapsed time from the start date.

## Results

As you can see below, the prediction was a little off since Germany actually got knocked out at the group stage of the tournament and France won the tournament, while Brazil were knocked out by Belgium in the quarter finals. The reasons for this relatively poor performance are two-fold:
- Firstly, the model and data used were overly simplistic since it used the FIFA ranking of the nations in order to predict which team would win, which explains why the two top ranked teams prior to the tournament were predicted to reach the finals with the number one ranked team winning. Whilst this may be a good way to predict results between teams that are far apart in rankings such as Germany and South Korea (albeit there was a shock this time), when two top ranked teams face off the differences are far more nuanced and so a simple model such as this would be insufficient for predicting the result accurately.
- Secondly, this world cup had a lot of shocks - no one could've expected Germany to be knocked so early in the tournament. This was the first time since the 1930s where Germany was knocked out at the group stage for example. Shocks are difficult to factor into models.

**Prediction**

![image](https://user-images.githubusercontent.com/45533954/92147181-a39cb680-ee12-11ea-980a-0ffd3e33fcf5.png)

**Actual**

![image](https://user-images.githubusercontent.com/45533954/92147630-4f460680-ee13-11ea-9744-11a3fc403f41.png)

## Next Steps
As mentioned above, this model is overly simplistic as it uses the relative rankings of the teams to predict the winner and so in order to progress this model, it would be best to include some other features related to each team's strengths and weaknesses such as the average age, international caps, or some other player specific features such as football manager ratings to establish the quality of the players. Alternatively, we could perform some sentiment analysis based on recent newspaper articles to determine how the world media sees each team's chances (no one predicted Germany to go out that early though!).
