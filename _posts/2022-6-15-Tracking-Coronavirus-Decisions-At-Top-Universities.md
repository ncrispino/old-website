---
Creator: Nick
categories:
  - Blog
tags:
  - COVID
---
Over the past two years, universities have made some tough decisions regarding COVID-19: when to implement online classes, have students return to campus, get vaccinated, and more.

As a student, I don't know much about what these decisions are based on; at all universities, there's a diverse group actively trying to do what's best for students (e.g., see [Stanford's plans](https://news.stanford.edu/report/2021/03/17/university-leaders-discuss-decision-making-time-covid-19/) for more detail).

However, the most prominent explanation I hear from other students for all COVID-related decision making is that of conformity; they think the decisions of "top universities" is the most important determinant of their school's policies. To test their hypothesis, I constructed a dataset with the dates of the top 100 (currently 51) universities' most impactful COVID decisions. This was a surprisingly tedious task, as there is no centralized database of COVID decisions. So, I had to scour each school's COVID response websites for university-wide updates, noting the dates for the corresponding actions. See the notes tab in the excel spreadsheet for more on the data.

[Spreadsheet with data](https://github.com/ncrispino/covid_university_dates)

After finding the data, I wanted to create a model. Originally, I wanted to see how important rank was as a determinant of first-mover status in COVID guidelines for universities. However, I'm slightly switching my task for now to utilize the machine learning methods I've learned. Now, I want to predict the number of days it takes for a university to respond using a variety of variables (with rank as one of them). For this project, see [my next blog post]({% post_url 2022-7-05-Predicting-University-Covid-Mandates %})
