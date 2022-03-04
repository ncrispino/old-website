---
creator: Nick
---
After learning basic python (i.e., Numpy, Matplotlib, and Pandas) from [QuantEcon](https://quantecon.org), I wanted to create some projects of my own. Initially, I had planned to examine independent (alternative) media on YouTube, but that proved too difficult with the tools I had learned. Additionally, (and maybe more importantly), I realized it had already been done by [Pew](https://www.journalism.org/2020/09/28/a-closer-look-at-the-channels-producing-news-on-youtube-and-the-videos-themselves/). Still, the idea stuck with me.

So, I shifted my focus to podcasts. Podcast data are difficult to find; unlike YouTube, there are no fully-transparent statistics available for views, downloads, or revenue. Because I still wanted to focus on podcasts, I realized I needed to use other data as a proxy. Spotify and Apple podcasts, [two of the most popular podcast platforms](https://www.statista.com/statistics/943537/podcast-listening-apps-us/), both maintained a list of top news podcasts, which I obtained through [Chartable](https://chartable.com/charts/spotify/united-states-of-america-news-politics). This allowed me to extract the top 50 news and politics podcasts in America for any given day.

Using these data, I wanted to find <!-- both **1)** the impact of each podcast relative to each other and **2)** --> the number of podcasts per political leaning (simplified to left, center, and right, or neither if the podcast wasn't politically-based).

<!-- ### 1) Analyzing Podcast Impact Using Google Trends
Put code here. -->

### Finding Political Podcast Lean
Before I present these data nicely, I'll show my Jupyter Notebook, which details my thought process into how to go about classifying podcasts. Originally, I planned to use machine learning and natural language processing to classify podcasts based on their Spotify podcast description or episode descriptions. However, that proved too time-consuming and unnecessary. There are only so many media groups or people who create podcasts, and since the episode descriptions aren't standardized, a far-left podcast could use similar verbage as a far-right one, therefore limiting the usefulness of an algorithm. If I planned to include much more than the top 50 podcasts, this approach have been more useful (and I could have expanded my scope, maybe using each podcast/podcast creator's Twitter, which may lend itself to more accurate categorization than episode descriptions), as I could tolerate a few miscategorizations due to the large sample size. However, as I was only categorizing 50 podcasts, I wanted no errors. Thus, using a third-party website and supplementing it with my classifications seemed the best approach, the process of which is described in the Jupyter Notebook:

[Original Jupyter Notebook]({% link Partisan-Podcasts.html %}){:target="_blank"}

Currently, this code gets the current day's partisan podcast numbers. However, for meaningful analysis, these data would need to be collected over time. I was unable to find a source that kept track of each day's top 50 podcasts, so I decided to do so myself, using Hierarchical Data Format (HDF) to store each day's charts on my system.

Using Windows' Task Scheduler and the code I wrote, I created a batch file to run this code everyday. Then, I created another notebook to analyze the temporal data.

#### Task Scheduler
Thanks to [this](https://towardsdatascience.com/automate-your-python-scripts-with-task-scheduler-661d0a40b279), I made a batch file, then configured it to run using Task Scheduler at 3:00pm everyday (occasionally my computer wasn't running during that time and the program would run later). Originally, the file wouldn't run, but I unchecked the box [requiring AC power](https://superuser.com/questions/1149391/windows-10-scheduled-tasks-are-not-running), which fixed it. Additionally, I use a conda environment to run this code, so I put it in the batch file; however, it originally didn't run, due to my not using ["call"](https://stackoverflow.com/questions/24678144/conda-environments-and-bat-files) to (de)activate the environment.

In a few months, I should have enough data to make the analysis more interesting. Right now, I configured the program to only save the charts, not my partisan lean assignments. This is because many of the podcasts in the top charts stay there and so it won't be a momentous task to assign each podcast a partisan lean when all the daily data is combined into a dataframe.

#### Temporal Analyzer

[Updated Jupyter Notebook]({% link Temporal-Partisan-Podcasts.html %}){:target="_blank"}

Using code from my original notebook, I created a new notebook that would load in each day's data in the HDF (from June 16, 2021 onwards) and use a dictionary to categorize each podcast's political leans. The notebook would load the dictionary (created in my original notebook) in, then use data from AllSides to add categorizations to the dictionary if there were new podcasts that couldn't be classified using the already-existent dictionary. It then categorizes each day's podcast charts and displays the podcasts classified as "Neither". This allows the user to inspect the podcasts and manually add any unclassified political podcasts to the dictionary. Then, this new dictionary is re-uploaded and graphs are created showing the current day's number of classifications and the total number of classifications across time.

Example figures created on June 17, 2021 in new Jupyter Notebook also shown below:

Current Day:
![June 17, 2021 podcast leans classified](\..\images\podcast_leans_Jun1721.png)
Across time:
![June 16, 2021 to June 17, 2021 podcast leans classified](\..\images\temporal_leans_until_Jun1721.png)


### Analysis
Currently, I have only two days of data collected, so I can't do any viable analysis. However, it's worth noting the limitations of this project. Most importantly, this project has no carryover to anything except the top US news podcasts on Spotify; the charts are an unpredictable thing based on Spotify's algorithm. They have no direct carryover to the views or subscribers or revenue earned by each podcast. Perhaps some of the podcasts on the charts are the most viewed, but many worthwhile podcasts are excluded. Additionally, the narrow categorization of news excludes non-news-focused podcasts that still discuss politics and could have a broad political impact. For example, The Joe Rogan Experience is absent from these charts, but constantly engages in political conversations and has political guests (e.g., Vermont Senator--and former Democratic presidential candidate--Bernie Sanders). In some ways, podcasts like Rogan's could be far more influential than the podcasts in Spotify's news charts, as they can engage politically ambivalent folk who don't already have fixed views about US politics. Another area of concern for the analysis of these data is the method of classifying partisan leans. I mainly used AllSides, which is a nonprofit that has classified news sources according to political lean. I also classified podcasts myself; I listed some of my justifications in my [original Jupyter Notebook](#2-finding-political-podcast-lean) when I created the dictionary (I hope to list these in a more accessible way in the future). However, both my and AllSides' analysis could be incorrect. It's difficult to truly classify based on political lean unless it's explicitly stated. Even when it is, the words or actions of a podcaster could defy their self-description and they could be better placed in a different category. Ultimately, some classifications are vague or have poor justifications, but I think most are well-founded and agreed upon.

Next, the classifications I came up with--"Left", "Center", and "Right" (and "Neither", for non-politically focused podcasts)--oversimplify the political nature of the US. There are sharp divides in both the left and the right, and not everyone outside the dichotomy should be classified as "Center". Any classification system will have its flaws; however, the more a system aligns with a project's goals, the better. I categorized any podcast that reasonably criticizes both sides as being "Center", which best allows for analysis regarding the growing partisan divide. AllSides uses my classifications (excluding "Neither") and "Mixed", in addition to "Lean Left" or "Lean Right". I categorized the leans as their respective sides and "Mixed" as "Center", due to my focus on partisanship.

The main reason I had for the collection of these data was to inspect the top news podcasts on a top podcasting platform and see how balanced it was politically, i.e, to see if one party (or view) was dominating the others or if there was a more even distribution. So, my simple classification best shows the potential dominance of one way of thinking.

In America, there are about an [even number](https://www.pewresearch.org/fact-tank/2020/10/26/what-the-2020-electorate-looks-like-by-party-race-and-ethnicity-age-education-and-religion/) of registered voters for each of my classified political leans (excluding Neither):
>"Around a third of registered voters in the U.S. (34%) identify as independents, while 33% identify as Democrats and 29% identify as Republicans"

So far, the data appear to largely align with this idea (though "Center" is underrepresented), as ~38% of the political podcasts on June 17, 2021 are "Left", ~36% are "Right", and ~27% are "Center" ([updated jupyter notebook](#temporal-analyzer)). When there is sufficient data to actually perform an analysis, I will return to this question to see how well it reflects the percent of registered voters per party, among other questions.

### Future Goals

#### For Everyone
Future analysis may do well to focus on the rise of new media when discussing partisanship in politics, as their viewership is only growing. Real studies could investigate the partisan leans of top podcasts in a larger and more systematic way, with more concrete methods based on prior research in the field (see this [paper](https://www.researchgate.net/publication/254366452_Listening_In_Building_a_Profile_of_Podcast_Users_and_Analyzing_Their_Political_Participation) as an example). Outside of academia, both Democratic and Republican agents could find this information useful; perhaps they could see in what way they're ahead/behind the other party in the podcasting field and how best to focus their digital efforts to boost party growth. Researchers could analyze the conversations in each podcast (some form of which I'm sure has already been done) in an effort to determine partisan language, seeing for example if podcasts are more conducive to a hyper-partisan environment than other mediums. They could also retrieve more information, such as views or viewer engagement which act as a better proxy of public interest and podcast influence than the somewhat-random Spotify charts. Again, the scope of my analysis is very limited, as I do not have the tools to investigate much further nor the political knowledge to see the valuable (or worthless) applications of such analysis. This project was done for fun and does not have any remotely important conclusions.

#### For Me
Hopefully, I can find a way to present these data in a live webpage that can toggle through the different days and let the user inspect which podcasts were classified under each partisan lean (with justifications). Ideally, this webpage would update automatically so that one can see the partisan leans evolve over time, along with descriptive statistics regarding each side's dominance.

[Here](\..\projects\Partisan-Podcasts-Interactive.html) is my project so far, which will be updated regularly.

### Sources
[Chartable](https://chartable.com/charts/spotify/united-states-of-america-news-politics) (in the future, update my webscraping to obtain the data directly through the [Spotify charts](https://podcastcharts.byspotify.com/))

[AllSides](https://www.allsides.com/media-bias/media-bias-ratings)
  - AllSides Media Bias Ratings™ by AllSides.com are licensed under a Creative Commons Attribution-NonCommercial 4.0 International License. These ratings may be used for research or noncommercial purposes with attribution.
