---
Creator: Nick
categories:
  - Blog
  - Projects
tags:
  - COVID
---
**TLDR:** Using machine learning, I tried to predict if a university with a vaccine mandate would also mandate a booster. [Here](https://covid-university-boosters.herokuapp.com/) are my interactive results with Dash. Preview:

![covid-uni-heroku-preview](\..\images\covid_uni_heroku_preview.png)

Inspired by [my last blog post]({% post_url 2022-6-15-Tracking-Coronavirus-Decisions-At-Top-Universities %}), I wanted to see if I could predict if and when universities made decisions to implement vaccine or booster mandates. I originally used the data I had collected, but since there were only 51 universities and the cost of collecting data was so high (as it was very tedious), I couldn't reasonably use it to create a machine learning model with good generalization. Initially, [I cleaned these data and added features](https://github.com/ncrispino/covid_university_dates/blob/master/Analyzing%20Covid%20Decision%20Dates.ipynb), intending to predict days until a Covid response from universities. I started to do the modeling [in my Covid Model Creation notebook](https://github.com/ncrispino/covid_university_dates/blob/master/Covid%20Model%20Creation.ipynb), but realized my analysis had some problems, so I moved on.

Instead [I found data online](https://github.com/ncrispino/covid_university_dates/blob/master/Vaccine%20Mandates.ipynb) that had more observations (~150) and cleaned it using the same methods, using [a more general script](https://github.com/ncrispino/covid_university_dates/blob/master/cleaning.py) (see [the previous link for my reasoning](https://github.com/ncrispino/covid_university_dates/blob/master/Analyzing%20Covid%20Decision%20Dates.ipynb)). Though this is a relatively small sample size, I knew I could still get good performance, likely with simpler models. With these data, I had when a university implemented a vaccine mandate and if they implemented a booster mandate. Since the number of universities without vaccine mandates was fairly small (~15 samples), I couldn't really predict this without more data. So, instead I decided to predict booster mandates given that a vaccine mandate was already in place. This was more balanced and thus with my small sample size I thought would result in a more accurate predictor, with around 75% of universities in my data opting for no boosters while 25% did.

![nested-cv-preview](\..\images\covid_uni_nested_cv.png)

The bulk of my analysis is done in [my Covid Booster Model notebook](https://github.com/ncrispino/covid_university_dates/blob/master/Covid%20Booster%20Model.ipynb) (see a preview above), along with sufficient explanations and sources. Note that the preprocessing transformations and final features used are listed in the Covid Model Creation notebook. For a summary, I used nested cross-validation (CV) with random search and the Matthews Correlation Coefficient (MCC) metric to select and evaluate logistic regression, random-forest, and support vector machine models for binary classification. In the end, I chose logistic regression as its model building method had good performance and a fairly lower standard deviation than the other models in nested CV. It performed fine on the test data with a MCC of ~0.316. This is not ideal (1 is the goal), but is somewhat expected on real-world data with a topic like this. In the future, I would like to collect more data and do more research on features, as many of the features I selected were based on my intuitions, not in-depth research. However, as this would take a long time to perfect--like any model--I accepted what I had was good enough for now and focused on deploying it so that I could gain practice creating an entire machine learning pipeline.

To showcase my model, I built a web-app using Dash and Heroku. Again, see the results [here](https://covid-university-boosters.herokuapp.com/).

*Note: This is just a broad overview of my project. My notebooks are very detailed and explain how my intentions changed throughout the project as I learned more. Also, Covid mandates for a given university are at least partially (though likely largely) based on the actions of its peers. My analysis does not take this correlation into account as it should; the observations aren't truly independent, which violates basic machine learning assumptions. My thought was the analysis will be more solid when I'm predicting a mandate in general using simple methods vs predicting the days it took to implement one taking correlation into account. So, I did the former.*
