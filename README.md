# Executive Summary
----
Submitted by Jane Liang 

## 1. Problem Statement

Korean Popular Music, the K-pop: has become increasingly visible to global audiences in the last decade thanks to evolution of YouTube, Facebook, Twitter and all other social medias. In the year 2017 and 2018, Kpop music industry finally break into the American market to make a significant wave in the US. On May 15th, 2017, Grammy.com posted an article titled "Why is K-pop’s popularity exploding in the United States?". In May, 2018, the boy band BTS made history as being first K-pop group to win No. 1 on the US Billboard Chart. On May 31st, 2018, the Guardian.com stated that "English is no longer the default language of American pop". A new-released K-pop music video can reach a million views on Youtube within a couple days, and the fans help promoting K-pop products by sharing them on their Facebook and Twitter. K-pop fans also believe that participating in discussion boards on Reddit is another important activity. 

Reddit's [K-pop subreddit](http://www.reddit.com/r/kpop) has over 325 thousand subscribers which is the one of the largest K-pop community for sharing K-pop news, videos, and other content. There are many types of post in K-pop subreddit which can post in their own channel categories(e.g., Discussion, News, Mv, Teaser etc.) depend on the content of the post. For instance, the majority of posts in "Discussion" channel are self-posts, with a title and a body of text written by the Reddit user whereas the posts in the "News" channel usually include a lot of url links to the original news publisher's websites. So, what K-pop fans are talking about and what can be a potential factors to drive the global success of K-pop in recent years.  

In this data science project, we collected the post on the K-pop subreddit which are submitted from 01/01/2013 to 12/15/2018. We wanted to build a classification model to classify which posts are belonged in recent two years. The purpose of this classification model is rather to find the most important text features with fairy acceptable accuracy than to produce the high accuracy classification model. Hence, the easily interpretable classification models such as Logistic Regression or Random Forest Classifiers are more suitable for achieving this purpose. This can be very useful to provide insights and suggestions for Korean Culture Center that they can identify the good strategies to keep the Korean Wave of pop culture going in US. 

## 2. Data Description

Pushshift API allows us to access the Reddit through building an URL with the relevant parameters without even needing Reddit credentials. With parameters, we will easily access the historical submissions written in unix timestamp. For example, with the url below:<br> 

https://api.pushshift.io/reddit/submission/search/?subreddit=kpop&limit=1000&after=1514764800&before=1517443200, <br>

we can collect 1000 posts submitted on the Reddit for a specific time period. If there's more than 1000 posts in this time period, we need to pull the last created timestamp and send another request to Pushshift API with updated the 'after' parameter. Therefore, the function is defined first for building the URLs, the function is called iteratively until we collect all the posts between 01/01/2013 to 12/15/2018.

---
**Responses from Pushshift API**
 
    [{'author': 'soshix21',
      'author_flair_css_class': 'fan',
      'author_flair_text': '1TYM',
      'created_utc': 1357028046,
      'domain': 'youtube.com',
      'full_link': 'https://www.reddit.com/r/kpop/comments/15rkbi/playlist_snsds_4th_album_youtube/',
      'id': '15rkbi',
      'is_self': False,
      'media': {'oembed': {'description': '"SNSD 4th", a playlist created by So Shi',
        'height': 450,
        'html': '&lt;iframe src="http://www.youtube.com/embed/videoseries?list=PLV2npvrON1KORMtq2-EA6Fq2LVISuV6Z2" width="600" height="450" frameborder="0"&gt;&lt;/iframe&gt;',
        'provider_name': 'YouTube',
        'provider_url': 'http://youtube.com',
        'thumbnail_height': 360,
        'thumbnail_url': 'http://i1.ytimg.com/vi/DIHZbwOX0Vs/hqdefault.jpg',
        'thumbnail_width': 480,
        .....]
---
We can access the information in JASON data by searching keys. The final resulted DataFrame:

|Column Names|Description|dtype|
|-----|----|----|
|Year| Post creation year| int|
|text| combined post title and body text|object|
|subchannel| subchannel names | object|
|class|1:posts created in 2017 or 2018; 0:posts created before 2017|int|


## 3. Contents of Jupyter Notebook

1. [Problem Statement and Data Collection](./Code/01_Problem%20Statement%20and%20Data%20Collection.ipynb)
    - 1.1 [Problem Statement](./Code/01_Problem%20Statement%20and%20Data%20Collection.ipynb#1.-Problem-Statement)
    - 1.2 [Data Collection](./Code/01_Problem%20Statement%20and%20Data%20Collection.ipynb#3.-Gathering-text-data-on-Reddit)
    - 1.3 [Data Cleaning](./Code/01_Problem%20Statement%20and%20Data%20Collection.ipynb#4.-Data-cleaning) 
    - 1.4 [Define Classes](./Code/01_Problem%20Statement%20and%20Data%20Collection.ipynb#5.-Define-classes)
    
    
2. [Cleaning and EDA](./Code/02_Cleaning%20and%20EDA.ipynb)   
    - 2.1 [Text preprocessing ](./Code/02_Cleaning%20and%20EDA.ipynb#3.-Text-Preprocessing)
    - 2.2 [EDA](./Code/02_Cleaning%20and%20EDA.ipynb#4.-Exploratory-data-analysis)
    

3. [Preprocessing and Modeling](./Code/03_Preprocessing%20and%20Modeling%20.ipynb)
    - 3.1 [Sklean TFIDFTransformer](./Code/03_Preprocessing%20and%20Modeling%20.ipynb#2.3-Initiate-and-fit-Tfidf)
    - 3.2 [Modeling](./Code/03_Preprocessing%20and%20Modeling%20.ipynb#2.-Modeling)
        - 3.2.1 [Logistic Regression Classifier](./Code/03_Preprocessing%20and%20Modeling%20.ipynb#2.2-Logistic-Regression)
        - 3.2.2 [Random Forest Classifier](./Code/03_Preprocessing%20and%20Modeling%20.ipynb#2.3-Random-Forest)
    - 3.3 [Conclusion](./Code/03_Preprocessing%20and%20Modeling%20.ipynb#3.-Conclusion)
    
## 4. Figures and Findings

[presentation.pdf](Reddit_NLP.pdf)

## 5. Conclusion 
By classifying if the Kpop Reddit post is created in the recent years, we wanted to attempt to retrieve important and trending text features for increasing the influence of Korean culture. 

According to the result of Logistic Regression model, I suggest to Korean Culture Center that Korean Wave phenomenon should keep integrating into a social media-embedded cultural landscape in US. Collaborate with popular Kpop artists like Wanna One, IZ\*One, (G)I-dle etc. who just made their debut in 2017 or 2018, make attractive video contents which can be a cover of other K-pop groups' or western artists' dance or songs and share these videio through social media websites. In addition, Kpop artists should keep trying to compose and produce their own songs for targeting global audiences. 