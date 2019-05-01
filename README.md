# Wikipedia-Influenza

* INTRODUCTION

The goal of this assignment is to try and reproduce for Italy
the results reported in this article for the USA:

[1] D.J. McIver & J. S. Brownstein (2014), "Wikipedia Usage Estimates Prevalence of Influenza-Like Illness in the United States in Near Real-Time", PLoS Comput Biol 10(4): e1003581 http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1003581

You will need:

1) OFFICIAL DATA ON INFLUENZA IN ITALY. The Italian health protection agency runs a flu surveillance program called "Influnet" that uses sentinel doctors. The project is described here: http://www.iss.it/iflu/index.php?lang=1&anno=2016&tipo=4 You can find the data in the Dropbox folder of the course, under "Assignments/influnet". The official data are reported in PDF files (see the "PDF" folders for examples) but a digitized version of the data is available for you under "data". You have one file for every flu season. You only need the 1st nd 5th columns of each file that are, respectively, the week of the year (https://en.wikipedia.org/wiki/ISO_week_date) and the estimated flu incidence for that week (i.e., fraction in the population of new weekly cases; watch out, the decimal separator is a comma instead of a period). These data will be your ground truth.

2) WIKIPEDIA PAGE VIEW DATA. Wikimedia Foundation makes available several datasets, tools and APIs to work with page view data. A summary can be found here: https://en.wikipedia.org/wiki/Wikipedia:Pageview_statistics
As an example, here you can see the "Influenza" and "Febbre" (fever) page view counts for the Italian Wikipedia: https://bit.ly/2SjFSsd
The raw data are available here: https://dumps.wikimedia.org/other/pageviews/
There is one compressed (gzip) file per hour (UTC time). Within a file, every row reports the number of hourly views for every page, according to the format:
		"it Influenza 8 0"
You only need the first three columns: the first is the language of the Wikipedia you are interested: you need to consider only the rows that have "it" or "it.m" here ("it.m" is the mobile version of the Wikipedia page). The 2nd column contains the name of the Wikipedia page ("Influenza" in the Italian Wikipedia in this case), and the 3rd columns if the number of page views (8 in this case) for that page during the hour the file corresponds to. You need to aggregate this data at the weekly scale, so that you can compare it with the official data described above. We are interested in the Italian Wikipedia only, so select only rows that begin with "it" or "it.m" and sum the pageview values for each page of interest.

* PART 1 (10 points)

	1.1 - Process the Wikipedia pageview data for the "Influenza" page of the Italian
	Wikipedia (https://it.wikipedia.org/wiki/Influenza), aggregate the pageviews
	on a weekly time scale, and plot the resulting time series of page views
	for the current year and - ideally - also for previous years.

	1.2 - Compare the time series from the official Influnet surveillance system
	with the time series of pageviews obtained in 1.1.
	Compute some measure of correlation between the two time series.
	Discuss your findings.

* PART 2 (10 points)

	2.1 - Try to find other Wikipedia pages related to flu whose pageview time series
	are correlated with the Influnet signal. For example, you could consider
	the pages linked from the "Influenza" page, such as symptom pages:
		- https://it.wikipedia.org/wiki/Febbre
		- https://it.wikipedia.org/wiki/Rinorrea
		- https://it.wikipedia.org/wiki/Mialgia
		- https://it.wikipedia.org/wiki/Cefalea
		- https://it.wikipedia.org/wiki/Vomito
	pages corresponding to medications for fever:
		- https://it.wikipedia.org/wiki/Paracetamolo
	and pages devoted to flu vaccines:
		- https://it.wikipedia.org/wiki/Vaccino_antinfluenzale#Vaccino_influenza_stagionale
	Use any strategy you think is appropriate to choose these pages.
	Compute their weekly pageview time series for the last year
	and - if possible - for the previous years,
	and plot them together with the Influnet signal as in 1.1.

	2.2 - For each of the selected Wikipedia pages, compute the same correlation
	with the Influnet time series that you computed in 1.2.
	Which of these correlations are strongest ?
	Did you discover a better page than "Influenza"
	in terms of correlation with the ground truth ?

* PART 3 (15 points)

	3.1 - Build a regression model that predicts the Influnet incidence
	for a given week based on the Wikipedia pageview data for the same week.
	Your features are the Wikipedia pageview counts for the "Influenza" page,
	for all the pages you have selected in Part 2,
	and for any other page that you think might help (there are probably
	global trends that have nothing to do with influenza,
	and you might think of ways to control for them in your model.)
	Carry out any feature selection you think it's appropriate.
	Evaluate the performance of your model via cross-validation.

	3.2 - Add these features to your model:
	- the Influnet incidence for the week preceding the target week
	- the pageview counts for all the pages you selected for the week preceding the target week
	Re-train your model and evaluate its performance via cross-validation.
	Did it improve ?
	How does it compare with the results reported in article [1] ?

* BONUS tasks (total bonus 5 points max)

	- nicely commented notebook with accurately discussed results (3 points)

	- timely completion of the assignment by due date December 16th (3 points)
