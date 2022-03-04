---
Creator: Nick
---
# Intro
Over the past two years, universities have made some tough decisions regarding COVID-19: when to implement online classes, have students return to campus, get vaccinated, and more.

As a student, I don't know much about what these decisions are based on; at all universities, there's a diverse group actively trying to do what's best for students (e.g., see [Stanford's plans](https://news.stanford.edu/report/2021/03/17/university-leaders-discuss-decision-making-time-covid-19/) for more detail).

However, the most prominent explanation I hear from other students for all COVID-related decision making is that of conformity; they think the decisions of "top universities" is the most important determinant of their school's policies. To test their hypothesis, I constructed a dataset with the dates of the top 100 universities' most impactful COVID decisions. This was a surprisingly tedious task, as there is no centralized database of COVID decisions. So, I had to scour each school's COVID response websites for university-wide updates, noting the dates for the corresponding actions. See the notes tab in the excel spreadsheet for more on the data.

*PUT LINK TO GITHUB with uploaded excel spreadsheet*

# Analysis
A common thought among students is that top-ranked universities are first-movers in COVID actions. To see if this is true, I regressed the number of days after the earliest school's covid action on rank and an assortment of controlling variables, including the number of cases in the zip code of the university (as more infections theoretically corresponds to earlier-imposed restrictions), public/private status, number of students, and which party holds governorship in the state (as recommendations and mandates come from the governor and can theoretically influence university attidudes, especially public ones). To create the dependent variable, I found the date of the university that made the first move, then calculated the difference between that day and the date of the corresponding action at all other universities in the dataset.

However, note that a key assumption of OLS and poisson regression is violated: we cannot assume independence of observations.
