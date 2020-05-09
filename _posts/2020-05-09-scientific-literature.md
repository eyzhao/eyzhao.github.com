---
title: Keeping up with scientific literature and my experience with SciReader.
published: true
---

The march of scientific progress waits for no-one. This is what makes what we do
exciting, but also at times overwhelming. It has been rightly noted that
[keeping up with literature can be a bit of a chore, and even at times disheartening](https://www.sciencemag.org/careers/2016/11/how-keep-scientific-literature),
if we find the exciting ideas we are pursuing have been done before. And yet,
my PhD supervisor's words echo in my head, "an hour in the library could save
you a week in the lab." He has been correct many times.

In order for research to have impact, it must fit its audience, context,
and scope. This requires a good understanding of the surrounding scientific
literature. Putting aside the fact that reading academic articles is a
skill requiring deliberate practice and patient persistence, today's
academic may find themselves deluged by the sheer volume of published
research. At the start of medical school, I was told that studying
medicine would be like drinking from a fire hydrant. This is doubly true
of research, except you cannot be sure when the stream ends or if you are
even at the right hydrant. Knowledge and established paradigms
become outdated so quickly that they often feel like passing fads.

I'd like to review some methods that I've personally tried to stay on
top of things. I'll also go into the latest method
I've been trying, which makes use of the
[SciReader](http://scireader.org/) recommender engine.

## What I've tried

In my search to tame the information torrent, I came across the
[Fraser Lab method at UCSF](https://fraserlab.com/2013/09/28/The-Fraser-Lab-method-of-following-the-scientific-literature/).
In short, they endorse the use of RSS feeds browsed with a central
app such as [Feedly](https://feedly.com/) or [InoReader](https://www.inoreader.com/).
This method saw me through the last half of my PhD, and often made me
the first among my peers to come across relevant new papers.
Over a few years, I built up a list of over 600 papers of interest.
The downside was the upkeep. Working in an interdisciplinary
field, I needed to keep abreast of papers from a wide range of journals,
and screening the titles of hundreds of articles for a
handful of relevant ones became tedious. I would fall behind whenever
deadlines loomed, and after returning to the clinical world,
this method fell by the wayside.

What became more useful were the few [PubMed search alerts I had set up](https://www.nlm.nih.gov/bsd/disted/pubmedtutorial/040_060.html).
This approach has better specificity, but poor sensitivity,
which can make it difficulty to discover work in complementary fields.
Alternatively, you could use the [PubCrawler web service](http://pubcrawler.gen.tcd.ie/)
to have matching articles emailed to you.

## Do Machine Learning to it

Enter SciReader. As described on the bioRxiv, it is a cloud-based personalized recommender system
that uses topic modeling and machine learning. Give it a list of papers or topics of interest
 and it will return an evolving list of recommended articles. This sounded familiar to me,
as I used a similar service called PubChase, which unfortunately closed down a few years ago.
But given my struggles, I was willing to give the concept another try.

I created a SciReader account and entered some preliminary information about topics of interest
and my own publication list. SciReader takes roughly a day to generate recommendations for you.

SciReader's parameterization of manuscripts considers article content,
metrics of paper quality and relevance, and the activity of other users with similar interests.
It performs topic modeling on the complete pubmed corpus by latent dirichlet allocation on the
TF-IDF metric with a cosine distance metric. One potential limitation is that it matches
based on abstracts only, as full text often sits behind a paywall. This may obscure
papers containing findings of interest buried in the results section, but for the
most part should suffice for most users.

## Detour: Exporting Articles from Feedly

For those wanting a jumpstart, you can export citations from EndNote or Mendeley in BibTeX format
and import them. However, as someone who's changed research fields a few times, and has used
these tools to write numerous course papers, I recognized that this would introduce many
unrelated topics into the system.

Instead, I turned to my Feedly "Read Later" list, which contained some 700 articles I had specifically
flagged as interesting to me. With some javascript magic, I scraped the titles, sources, and URLs of
every paper I'd flagged. I filtered these to contain only research articles.

In order to import into Feedly, I needed to convert this data into
[BibTeX format](http://www.bibtex.org/Format/),
which at least requires the author list, year, and journal.
Luckily, Google Scholar has the handy ability to find almost any
article by its title alone, and
helpfully generates citations in BibTeX format. Using a
[Python Selenium](https://selenium-python.readthedocs.io/) script, I was able to automate the
process of pulling down the hundreds of articles in BibTeX format (much to the Google CAPTCHA's
chagrin, but I don't think I caused any damage). Perhaps someone knows a better
way to rapidly convert a set of journal article titles into citations.
I then verified that Google Scholar's resulting articles matched
my chosen articles with some fuzzy string matching, using one of my favorite packages
[FuzzyWuzzy](https://github.com/seatgeek/fuzzywuzzy). This gave me a unified BibTeX file to
upload into SciReader.

I've put the code I used into a [GitHub repo](https://github.com/eyzhao/feedly-to-scireader).
The documentation is admittedly sparse, but it might serve as a launching-off point
for someone who wants to do something similar.

## The Verdict

SciReader's engine recommended numerous recent publications clearly linked to my personal area of
interest and expertise. It captures results from a wide range of journals. It also does a great
job highlighting groundbreaking recent advances in fields adjacent to my own. I suspect this
is the combination of topic modeling, quality assessment, and collaborative filtering at work.
It might take a little while for me to get a full sense of how well this system works for me,
so I will report back down the road.

The site itself can be buggy at times. In particular, I found the "Load more" button 
(which shows you more recommendations) would sometimes not work, requiring a page reload.
Also, during the month of March 2020, the site seemed to be down altogether - I'm not sure
who is maintaining it presently.

All in all, this is what I would consider a hacked-together approach to give me one
more angle of attack when it comes to dealing with the research literature glut.
Whether it translates into actionable insights, I don't know. But it's gotten me to
think more about how I stay on top of my reading.
