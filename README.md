<h3>covid19-tracker-fitter</h3>
<h6>Download daily Johns Hopkins COVID19 data, track and fit deaths to sigmoid like function. 
Data is updated at 8pm EST each day. Hospitalization data has not been available each day so it 
is not included at present but will be added in upcoming days.</h6>

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
<li><i>This worldwide COVID19 data has not been sampled properly and has limited applicability to predict US COVID19 deaths, 
 hospitalizations, and ICU beds:
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
 <ol>
 <li>The data from China is a complete "FARSE". It is a lie and unrealistic. Just looking at the
  data curves for confirmed cases and deaths from China can lead to this conclusion. Next, there 
  are minimal cases reported in China outside of Wuhan. Yet there have been large numbers of air flights 
  to all major cities (e.g., Beijing, Shanghai, Hong Kong, etc.) every day during the start of this 
  outbreak in Wuhan. The Chinese are simply lying about the rest of their country. See this paper, Fig. 1, 
  published in the Lancet: https://doi.org/10.1016/S0140-6736(20)30260-9. China currently claims  82052, 589, 607 for confirmed case for the entire Mainland, Beijing and 
  Shanghai, respectively. Similary, the COVID19 deaths are 3339, 9 and 7, for the entire Mainland, 
  Beijing and Shanghai, respectively. <b>LIES, LIES, and more LIES!!!</b></li>
  <li> South Korea has been praised for its containment and mitigation. However, it is likely that
  they have significantly underreported as well. They have reported 10,480 confirmed cases and 
  211 deaths for a population of 51.6M. They have likely underreported since the government is highly influenced by large 
  conglomerates like Samsung who want their population working.</li>
  <li>There is an unexplained phenomenon with the number of confirmed cases and deaths in California and Washington State. The number of flights 
  from Wuhan to SFO, LAX and SETAC before the US Travel Ban from Wuhan were the highest from these cities. Therefore the infection rate should be or 
  should have been very high in San Francisco, Los Angeles and Seattle. However this is not the case and there is currently no good explanation for
  this phenomenon. Mitigation does not explain this since it was not practiced in the weeks leading up to the travel been and for many weeks after 
  the travel ban.</li>
  <li>COVID19 testing worldwide cannot be used for any predictions. It can only tell whether an 
  individual person has COVID19. First there has been no reported comparison across countries between sensitivity (test positives / all positives) 
  and the specificity (test negatives / all negative) which are statistical measures of the performance of a binary classification test. 
  Next the testing does not sample the population in any fashion as it is predominantly used for "sick" people who present for testing</li>
  <li>Worldwide COVID19 deaths could be useful but there is no way to estimate the death rate since the number of infected people since there are 
  many more asymptomatic and mildly ill than seriously ill with COVID19. This is indeed the case as shown from the death rates per confirmed cases
   shown in the covid-tracker.</li>
   <li>The accuracy of worldwide COVID19 deaths reported is not fully quantified. China is clearly LYING and it is likely there are many additional
    inaccuracies.</li>
   <li>Reported deaths from other countries are most likely not reported in the same manner as US Deaths where anyone who is infected with COVID19
    at the time of death is recorded as a COVID19 death. Italy (and reports from Spain) have lead to conjecture that they have overstated the deaths
    from COVID19 and are changing the numbers retrospectively.</li>
    <li>Another problem with using COVID19 deaths from other countries is as follows. A patient is seriously ill in the ICU with COVID19 in the US 
    and a foreign country. Is the probability of death similar in both cases? Or is it lower in the US due to better healthcare system.</li>
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
  <li>The IHME python model uses curve fitting regression models written at Univ Washington (by graduate students). Here LMFIT is used for the curve fit 
  since it is one of the 'gold standards' for curve fitting in Python. It also provides std. error for each of the parameters fit and this can be 
  converted to 95% confidence by multiplying it by +/- 1.96.</li>
  <li>Each day the model is updated at 8pm EST when John Hopkins provides its daily updates</li>
  <li>Data is plotted by cumulatively by state with 95% confidence bands and the cumulative data is summed for the entire US. The first derivative of 
  the cumulative data is also shown to estimate the US Death Rate Peaking.</li>
</ol>
