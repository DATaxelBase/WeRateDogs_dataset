# WeRateDogs Dataset

## Data Wrangling
Hello dear reader, 
The dataset that i will be wrangling (analyzing and visualizing) is the tweet archive of Twitter user @dog_rates, also known as WeRateDogs. WeRateDogs is a Twitter account that rates people's dogs with a humorous comment about the dog. These ratings almost always have a denominator of 10. The numerators, though? Almost always greater than 10. 11/10, 12/10, 13/10, etc. Why? Because ["they're good dogs Brent."](http://knowyourmeme.com/memes/theyre-good-dogs-brent) WeRateDogs has over 4 million followers and has received international media coverage.
WeRateDogs downloaded their Twitter archive and sent it to Udacity via email exclusively for me to use in this project. This archive contains basic tweet data (tweet ID, timestamp, text, etc.) for all 5000+ of their tweets as they stood on August 1, 2017. 
Added to dog names, we have also dog stages.[](https://video.udacity-data.com/topher/2017/October/59e04ceb_dogtionary-combined/dogtionary-combined.png) The Dogtionary explains the various stages of dog: doggo, pupper, puppo, and floof(er) (via the [#WeRateDogs](https://www.amazon.com/WeRateDogs-Most-Hilarious-Adorable-Youve/dp/1510717145) book on Amazon)

![Weratedogs](https://video.udacity-data.com/topher/2017/October/59dd378f_dog-rates-social/dog-rates-social.jpg)
To wrangle data for this project, i passed three big steps:
1. *Gahtering data* :
- I downloaded the WeRateDogs Twitter archive data, 
- I used the Requests library to download the tweet image prediction,
- I used the Tweepy library to query additional data via the Twitter API.
2. *Accessing data*
I took a look about each dataset. The more dirty dataset were the Twitter archive data. 
With programatic accessment , i discovered that we have retweets inside dataset to be excluded. I focused a little on dog names and rating numerator and rating denominator and understood that they came from text column. But there is a lot of issues with these columns. Some name aren't properly extracted in name column, probably due to name extraction rule. My hypothesis is that they extracted the word after the `is`. Unfortunately in some text , the name come after `named`. 
A second point ,the more problematic issue is the rating. In order to make properly the analysis ,i have to normalize the denominators. I though at beginning that all ratings will be set on 10 but there were some unbeleivable denominators. Fortunatelly the numerators in these cases were higher also. So i had to re-compute the rating from text to ensure that i would not have a lot of outliers. Also, there were some wrong ratings due to dates or links in text column, so as for name, i had to place properly the rating in dedicated columns.
In image prediction dataset, i payed attention on the result of algorithms (the p1_dog,p2_dog,p3_dog columns).If the image predicted is not a breed of dogs on at least 2 image algorithm prediction, sure that this tweet is not rating a dog but perhaps another animal. So i had to exclude these tweets.
At the end i had to merge some columns into one like rating and dog stages , and the three dataset on tweet_id. 
3. *Cleaning data*
The more tricky issue to be cleaned for me were the rating correction. Find the good regular expression which extract properly the rate and after perform the computation to force all denominators to `10`.

## Summary of Findings
I tried to answer these following questions:

Which breed is rated higher than the others?
Which dog stages have the most audience?
Which breed is more underrated by audience ?
What is the link between rating and retweet and favorite counts? 
So based on retweets and favorites counts , the best rating is 14/10 given tostandard_poodleat first place, Rottweiler at second place at third place the French bulldog. I payed attention on algorithm results, if the p1 is not confident about his prediction , there are p2 and p3 which provide also the prediction , but like the p1>p2>p3 about the probability to predict properly the breed of dog. When the p1 predict a swing , sure that i will find more suitable prediction on p2 side. The Lakeland terrier dog breed is very underrated by the audience based on p1 algorithm detection. The American Staffordshire terrier has the poorest rate but seems to be liked by people due to high number of favorite and retweet count.
The rating impacts the favorite count. This last grows expontentially when the rating increases. On another hand, the retweet count is proportional to favorite count.Inside data, we have a lot of pupper. Unfortunately puppers are underrated by audience and as expected their favorite and retweet counts are quite low. Contrary to doggo and puppo which have best results.

## Key Insights for Presentation

For the presentation, I focused on the more rated dogs and the preferences of audience. I tried to filter out how ratings are distributed in dataset and also how dog stages impact the favorite count and retweet count.
# WeRateDogs_dataset
