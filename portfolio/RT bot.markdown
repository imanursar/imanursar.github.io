---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: RT bot
parent: Portfolio
nav_order: 11
---

# Twitter RT Bot

Source code can be found on [my github](https://github.com/azukacchi/DKMKbot)

## Notes
This bot is made out of sheer desperation from the lack of my niche fandom contents.

## What does this bot do
This is a simple twitter bot that collects tweets containing a certain keyword, stores them in a database file, and retweets them at a certain time window, built in Python using Tweepy.

## What do I need
- Tweepy module; `pip install tweepy` (installation <a href="https://tweepy.readthedocs.io/en/latest/install.html">docs</a>)
- A Twitter developer account; sign in to your Twitter account then apply for a developer account <a href="https://developer.twitter.com/en/apply-for-access">here</a>. After your application is approved, make sure to change the permission to the "Read, Write, and Direct Messages".
- DB Browser for SQLite; download <a href="https://sqlitebrowser.org/dl/">here</a>.


## Why do I need a database file
I use this for my rarepair fandom; the contents are so rare which is why I collect them in a database file to be retrieved and retweeted at a certain time window. Anyone can use this method but only as long as the number of tweets collected is not too big. 

If you want to retweet tweets containing your keyword in real-time, you might need to use the streaming API instead of the REST API used in this bot. Read Twitter's documentation about <a href="https://developer.twitter.com/en/docs/twitter-api/v1/tweets/filter-realtime/overview">streaming API</a> and Tweepy's documentation about <a href="https://tweepy.readthedocs.io/en/latest/streaming_how_to.html">StreamListener</a>.

## Files
### 1. main.py
Contains all the main functions, which will be imported to each respected .py file.
### 2. createtable.py
The `createtable()` function creates the database file and the table inside. You only need do this once in the beginning, by running this code or creating the table manually with the same specified field (`ID`, `Username`, `Time`, `Tweet`, `RTStatus`, `DMSender`) and data type.
```
connection = sqlite3.connect(db_path)
create_twt_table = '''CREATE TABLE IF NOT EXISTS tweets (
    ID INTEGER PRIMARY KEY AUTOINCREMENT,
    Username TEXT NOT NULL,
    Time DATETIME NOT NULL,
    Tweet TEXT NOT NULL,
    RTStatus INTEGER,
    DMSender INTEGER);'''

cursor = connection.cursor()
cursor.execute(create_twt_table)
connection.commit()
```
The most important fields for this bot are `ID` (ID of the tweet), `RTSTatus`, and `DMSender`. The others (`Username`, `Time`, `Tweet`) are added so it's easier to check whether your program is working and collecting the tweets. If you think the additional fields will increase your database size (again, idk how big is big) (for illustration, my database after 7 days running the bot contains 223 rows and has size of 60.0 KB), you can omit them but only after modification in the code related to updating the database. 

### 3. updatebot.py
This file runs the `updatetwt()` function which collects the tweets containing the keyword through API.search and and API.favorites (refer to Tweepy's API reference <a href="https://tweepy.readthedocs.io/en/latest/api.html">here</a>).
#### API.search part explanation:
```
# checking newest tweets to 7 days back

n = 40 # max of how many tweets are retrieved in each request

search_words = 'YOUR-KEYWORDS' # put your keywords here, example: your rarepair name

criteria='min_faves:15 filter:media' #example of filter and criteria
# more details read the link I gave about Twitter standard search operator

date_since = date.today() - timedelta(days=7)
# max search is to 7 days back

new_search = search_words + " " + criteria
# joins your keyword with the search criteria

tweets = tweepy.Cursor(api.search, q=new_search, lang='ko', since=date_since, tweet_mode='extended').items(n)
# the api.search function
# notice the lang parameter! it's set as Korean
# change it to your contents' primary language, e.g. EN for english
```

#### API.favorites part explanation:
You might ask, why the API.favorites? This is used to collect the tweets from the authenticated user's (your bot account's) favorite tab. Twitter's Standard search API (the free one) limits the search query to 7 days back, which means if my ***rarepair*** (in bold and italic, lol) bot were to collect the tweets through API.search method, the contents of my bot would be very limited. The workaround is to search the tweets manually (like you usually do on your mobile/desktop) using standard search operator (read <a href="https://developer.twitter.com/en/docs/twitter-api/v1/tweets/search/guides/standard-operators">here</a>). On mobile/desktop you can easily search tweets way far back than just the 7 days limit by API.search. Then the bot will scrape them for you and unlike the tweets. 
```
tweets2 = tweepy.Cursor(api.favorites, q=api.me().screen_name, tweet_mode='extended', lang='ko').items()
for tweet in tweets2:
    # .... (the cleaning part)
    api.destroy_favorite(tweet.id)

```
#### Updating the database
Tweets that are collected through the `updatetwt()` function will not be given any RTStatus value (so its value stays NULL).
```
connection = sqlite3.connect(db_path)
crud_query = '''INSERT OR IGNORE INTO tweets (ID, Username, Time, Tweet) values (?,?,?,?);'''

zipobj = zip(twtid, username, twtdate, items)

input_list = [*zipobj]

cursor = connection.cursor()
cursor.executemany(crud_query,input_list)
connection.commit()
```
See the code details in `main.py` under `updatetwt()` function on how the tweet ID, username, date, and tweet text are scraped.

### 4. retweetbot.py

Another feature of this bot is collecting suggestion (tweets to be retweeted) through DM, which is done by the `checkdm()` function. The submission should be written as `<triggerword> <link to the tweet>` in one message, thus the tweet will be collected ONLY if the DM contains the trigger word AND a link to a tweet. The tweets that are collected through submission will be given the priority to be retweeted, thus will be given `RTStatus` value of 2.
#### checkdm() part explanation:
```
dms = api.list_direct_messages(count=15)

for dm in dms:
        
    if '(YOUR-TRIGGER-WORD-HERE)' in dm.message_create['message_data']['text']:
        urls = dm.message_create['message_data']['entities']['urls']
        if len(urls) >0:
            linkcontent = urls[0]['expanded_url']
            regex = r'(?=twitter\.com\/\w+\/status\/(\d+))'
            dmtwtid = int(re.findall(regex, linkcontent)[0])
```


#### retweet() part explanation:
```
# Calling for tweet that hasn't been retweeted yet from the database
    
connection = sqlite3.connect(db_path)
cursor = connection.cursor()

cursor.execute('SELECT ID, RTStatus, DMSender FROM tweets WHERE \
    RTStatus == 2 OR RTStatus IS NULL GROUP BY Username ORDER BY RTStatus DESC')
datafin1 = cursor.fetchmany(1) # I only take 1 tweet each time I retweet
connection.commit()
        
idtwt = [twt[0] for twt in datafin1]
rtstatus = [twt[1] for twt in datafin1]
dmsender = [twt[2] for twt in datafin1]
# i'll use dmsender for senddm()

for id in idtwt:
    try:
        api.retweet(id=id)
        if rtstatus == 2:
            senddm(api, dmsender)

        for id in idtwt:
            cursor.execute('UPDATE tweets SET RTStatus=1 WHERE ID=?', (id,))
            connection.commit()

    except tweepy.error.TweepError:
        cursor.execute("DELETE FROM tweets WHERE ID=?", (id,))
        connection.commit()
```
#### senddm() part explanation:
Because the bot will not retweet the suggestion as soon as the DM is received, I added the feature to notify the DM sender when the suggestion is retweeted with this function. You can omit this function by deleting this block inside the `retweet()` function.
```
if rtstatus == 2:
    senddm(api, dmsender)
```
### 5. config.py
Paste your keys and tokens you get from your Twitter developer account in this file.


## How do I automate the script
I use Task Scheduler on Windows (open Start then search Task Scheduler) to run the `retweetbot.py` every two hours and `updatebot.py` every 8 hours. This app is quite simple to use, the only downturn is it only runs when your computer is either turned on or sleep but not shutdown (obviously). Some helpful tutorials can be found [here](https://www.jcchouinard.com/python-automation-using-task-scheduler/) and [here](https://dev.to/abautista/automate-a-python-script-with-task-scheduler-3fb6).
