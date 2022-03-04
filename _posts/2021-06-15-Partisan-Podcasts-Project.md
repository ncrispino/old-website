---
title: Partisan Podcasts Project
categories:
  - Projects
tags:
  - Pandas
  - Plotly
---
<!-- Center font in this document -->
<link href="\assets\css\minimal-table.css" rel="stylesheet" type="text/css">
<style>
.content {
  text-align: center;
}
</style>

<!-- <div class="change_img">Click the image to see the partisan leans across time.</div>

<figure>
  <img src="\..\podcast_day_data\podcast_leans_today.png" alt="Current day's partisan leans">
  <figcaption>Partisan Podcast Leans Today</figcaption>
</figure> -->

<div id="plotly-today"></div>
<div id="plotly-temporal"></div>
<!--more-->
<br />

<div id="fraction-compare">
  Fraction of today's podcasts (<em>left</em>) and average number of podcasts for all recorded days (<em>right</em>) for each political lean.
  <br />
  <br />
  <figure id="today-political">
  </figure>

  <figure id="mean-leans">
  </figure>  
</div>

<br />

Partisan Database
<!-- https://stackoverflow.com/questions/8988855/include-another-html-file-in-a-html-file -->
<div id="classify-justify"></div>

<br />

All podcasts classified as "Neither"
<div id="all-neither"></div>  


<!-- Full data available <a href="" target="_blank">here</a>. -->  
<br />
<details>
  <summary>Process for Obtaining Data</summary>

  <h3>Process</h3>

  Using Panda's dataframe to HTML, I created and displayed data for analysis. Originally, I tried to convert the dataframes to CSV, then display those on this page, though I learned it is much easier to display the html.

  To create the partisan database classification table, I created another Python file to run in the daily batch file, which would convert the necessary data to HTML format, updating everyday.

  Though the images and tables are automatically updated, the webpage isn't. This is due to the Python files running and storing the data locally. Ideally, these scripts should be run on the cloud and the webpage should fetch the data (including graphs) from the the cloud to be put on the webpage.

  This would require a lot of work--as I could no longer use Jekyll, which is made for static sites. Because my focus isn't in web-development but in economics/politics and data analysis, I'm going to focus on doing further analysis rather than creating a more interactive user experience. Perhaps in the future I could return to this using a web-framework like Django. However, my interests lie elsewhere, so for now, this must do.
</details>

<script src="\scripts\jquery.js"></script>
<script src="\scripts\partisan_script.js"></script>
