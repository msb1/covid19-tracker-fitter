<h3>covid19-tracker-fitter</h3>
<h6>Download daily Johns Hopkins COVID19 data, track and fit deaths to sigmoid like function. Also use data from NY State to fit
coefficients for SEIR (QP) viral transmission model using LMA and Hamiltonian (Markov Chain) Monte Carlo
Data is updated at 8pm EST each day.</h6>

<h6>Note: there have been dramatic adjustments to the deaths attributed to COVID19 in numerous states, especially in New York. 
This of course significantly changes model predictions. Hopefully, this is honest reporting but there are issues of concern which 
stem from adding many issues not standard in causal death reporting. Dr. Deborah Birx, CDC Coronavirus Coordinator has expressed
concern as have many other prominent researchers, physicians and coroners.</h6>

<h4>CovidTracker.ipynb</h4>
<ol>
<li>Download daily Johns Hopkins COVID19 csv data with Python Pandas method into dataframe</li>
<li>Aggregate data by country and by each US state</li>
<li>For each country and state, compute the death rate (fraction of deaths per confirmed cases for each country)</li>
<li>Plot confirmed cases and deaths for each country and each state</li>
</ol>

<ul>
<li><i>IHME has been using worldwide COVID19 data to predict cases, deaths and hospitalization in the US. 
 These models have been used in US policy making decisions regarding the response to COVID19</i></li>
<li><i>This worldwide COVID19 data was not been sampled properly and has limited applicability to predict US COVID19 deaths, 
 hospitalizations, and ICU beds. This led to all sorts of bad advice and public policy.
 <ol>
 <li>First there needs to be understanding of probability vs non-probability sampling.</li>
 <li>A probability sample is a sample in which every unit in the population has a chance (greater than zero) 
 of being selected in the sample, and this probability can be accurately determined. The combination of these 
 traits makes it possible to produce unbiased estimates of population totals, by weighting sampled units according to their probability of selection. </li>
 <li>Nonprobability sampling is any sampling method where some elements of the population have no chance of selection 
 or where the probability of selection can't be accurately determined. Hence, because the selection of elements is 
 nonrandom, nonprobability sampling does not allow the estimation of sampling errors. These conditions give rise to exclusion bias, placing limits on 
 how much information a sample can provide about the population. Information about the relationship between sample and population is limited, <u>making 
 it difficult to extrapolate from the sample to the population.</u></li>
 <li>All of the worldwide COVID19 data appears to be in the form of non-probability sampling
  <li>Indeed the lack of predictive capability of the IHME models support the above assertions.
 </ol>
 </li>
 </ol>
 </i></li>
</ul>

<h4>CovidFitter.ipynb</h4>
<ol><li>The IHME has published a model for predicting (and tracking) COVID19. A preprint of
the model can be found here: http://www.healthdata.org/sites/default/files/files/research_articles/2020/COVID-forecasting-03252020_4.pdf?mc_cid=0d35e5e860&mc_eid=bb1324380c</li>
<li>This model fits worldwide and domestic US COVID19 death data with a modified Gaussian Error Function and mentions they have tested other
 sigmoidal functions but have the "best results" with this function</li>
 <li>The CovidFitter presented here has tested several modified sigmoidal functions (sigmoid, tanh, and Gaussian Error) on US COVID19 Death data only - 
  since it is known that the US Data is the most accurate (including state-to-state reporting).</li>
  <li>A modified sigmoid is used in CovidFitter since there is little difference with other functions tested.</li>
  <li>In each sigmoidal function, a rate of increase coefficient, an offset (at the half level) and a max are fit to the data.
  <li>The IHME python model uses curve fitting regression models written at Univ Washington (by graduate students). Here LMFIT is used for the curve fit 
  since it is one of the 'gold standards' for curve fitting in Python. It also provides std. error for each of the parameters fit and this can be 
  converted to 95% confidence by multiplying it by +/- 1.96.</li>
  <li>Each day the model is updated at 8pm EST when John Hopkins provides its daily updates</li>
  <li>Data is plotted by cumulatively by state with 95% confidence bands and the cumulative data is summed for the entire US. The first derivative of 
  the cumulative data is also shown to estimate the US Death Rate Peaking.</li>
</ol>

<h4>SEIR-ODE-Fitter.ipynb</h4>
<ol><li>There is a well known viral transmission model - SEIR model. Some Italian researchers published a preprint of a nice version of this
model with extension to COVID19 in Italy. They optimize the differential equation parameters using a Particle Swarm Optimization (PSO) algorithm.</li>
<li>This model solves the differential equations similarly but optimizes the parmaters with LMFit with a minimization problem enabled by the
Levenburg Marquadt Algorithm (LMA).</li>
<li>Recently published data for New York suggesting ~30% of the population has had COVID19 is in line with the model predictions.</li>
<li>This model suggests that the high transmissibility of the COVID19 virus takes weeks rather than months for widespread outbreak. And one of the
model parameters is an inflection date which represents when the infected reach a critical mass - e.g., 1% of population</li>
<li>By setting this parameter to determine inflection date, the actual date of inflection in the model occurs on March 20, 2020. This date is represents
when mitigation - shelter-in-place - was beginning to take affect. The US Federal Government issues shelter-in-place guideline on March 16, 2020 and the
State of New York issued similar orders on March 22, 2020 at 8pm (effectively March 23).</li>
<li>Prior to the inflection date, a different problem is being solved since there was effectively limited mitigation before this date.</li>
</ol>

<h4>SEIR-ODE-MCMC.ipynb</h4>
<ol><li>There is a well known viral transmission model - SEIR model. Some Italian researchers published a preprint of a nice version of this
model with extension to COVID19 in Italy. They optimize the differential equation parameters using a Particle Swarm Optimization (PSO) algorithm.</li>
<li>This model solves the differential equations similarly but optimizes the parmaters with a Hamiltonian Monte Carlo</li>
<li>Recently published data for New York suggesting ~30% of the population has had COVID19 is in line with the model predictions.</li>
<li>This model suggests that the high transmissibility of the COVID19 virus takes weeks rather than months for widespread outbreak. And one of the
model parameters is an inflection date which represents when the infected reach a critical mass - e.g., 1% of population</li>
<li>By setting this parameter to determine inflection date, the actual date of inflection in the model occurs on March 20, 2020. This date is represents
when mitigation - shelter-in-place - was beginning to take affect. The US Federal Government issues shelter-in-place guideline on March 16, 2020 and the
State of New York issued similar orders on March 22, 2020 at 8pm (effectively March 23).</li>
<li>Prior to the inflection date, a different problem is being solved since there was effectively limited mitigation before this date.</li>
<li>Gibbs sampling is used with a flat prior since the model estimates 7 coefficients. The likelihood is determined from a normalized sum square
residuals (SSR) and a new event is only accepted if the ratio with the prior event likelihood is greate than one.</li>
<li>Note that New York (in particular) has been changing the way they record COVID19 deaths since about April 17, 2020. This has led to difficulties
with all models that fit to data since there have been prior deaths added in artificially that need to be tallied on their actual dates and the "slope"
has changed since more deaths are attributed to COVID19 - i.e., according to latest CDC guidelines (which are discussed at the top of this readme file)</li>
<li>To account for this difficult, linear weighting has been applied to the normalized SSR residuals so that the most recent error data is weighted the
greatest. (Exponential weighting was also tested but the results were very sensitive to the base weighting factor.)</li>
</ol>


<h4>YEARLY Seasonal Influenza Data</h4>
<ol>
<li>For reference, the yearly influenza data is also a significant health concern. In 2017-2018
season, with the widespread availability of a vaccine, there were approx. 45M cases of influenza with 61K deaths and 810K hospitalizations. (CDC data -see image below from a CDC presentation</li>
<li>The current influenza vaccine includes 4 viral strains that have been studied from a prior year and
predicted to be a problem in the upcoming year. Quite often, the "experts" miss 1 - 2 viral strains and
a large part of the population gets the illness. This is why many emphasize that the influenza vaccine is
only a partial vaccine.</li>
<li>This further underscores the notion that effective treatments are as important as potential vaccines especially given the propensity of viruses to undergo mutation and the length of time it takes to prepare/test vaccines.
</ol>
<br/>

![Influenza Seasonal Tracker from CDC](https://github.com/msb1/covid19-tracker-fitter/blob/master/influenza-by-season.png)
