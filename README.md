## Tweet & arXiv Short Text Dataset [![Build Status](https://travis-ci.org/lalxyy/shorttext-dataset.svg?branch=master)](https://travis-ci.org/lalxyy/shorttext-dataset)

This is the public dataset of China Patent *A Short Text-Hashtag Based Domain Tracking Method*. Contains Twitter tweet data since October 25, 2017 and arXiv paper summary since December 20, 2017.

The data is regularly updated every Saturday (Pacific Time).

**Notice:** GitHub has 2GB limitation per file; the largest full data here is 2.7GB. So the data here only includes the latest 100 records of each datasource. The full data is available on [Google Cloud Storage](https://console.cloud.google.com/storage/snrs/). Google account sign-in required.

### How to Start

To use the sample data on GitHub:

```shell
git clone https://github.com/lalxyy/shorttext-dataset.git
cd shorttext-dataset
git checkout -b master
```

The data is provided in JSON format, which can be imported into MongoDB through `mongoimport`.

```shell
mongoimport --db <database> --file arxiv.json
mongoimport --db <database> --file tweet-hashtag.json
mongoimport --db <database> --file tweet-timeline.json
```

If you'd like to use a completed data:

```shell
# Install gsutil first
# In Python 2.7 Environment
pip2 install gsutil

# Google account sign-in required
gsutil config

# Access data
gsutil ls -r gs://snrs
gsutil cp gs://snrs/*.json ./
```

### General

#### Tweet Data

Tweet data comes from 2 sources.

- The tweets of famous scientists related to recommender system. A detailed list of these people could be seen in our Twitter bot [BatCrwl Rs](https://twitter.com/BatCrwlRs)'s following list.

  These data is in `tweet-timeline.json`.

- The tweets containing following hashtags:

  ```
  #recsys
  #RecommenderSystem
  #ACMRecSys
  #recsys
  #recsyschallenge
  #recsys2017
  #bigdata
  #AI
  #datascience
  #dataviz 
  ```

  These data is in `tweet-hashtag.json`.

**Note:** Twitter streaming API fetches not only hashtags but also tweets containing the hashtag word. You may notice that `tweet-hashtag.json` contains fuzzy data at starting points - the reason is as above, Twitter pushed all tweets containing `ai`, not only the hashtag, to me. In November 2017 I removed `#AI` from the observing list. For this reason, the noise of initial data may affect your analysis results.

A typical record of tweet is like this. `ObjectId` and `NumberLong` are special data types in MongoDB.

```json
{
	"created_at" : "Sun May 06 05:09:32 +0000 2018",
	"id" : NumberLong("992994753284399104"),
	"id_str" : "992994753284399104",
	"text" : "RT @KirkDBorne: [Book] Artificial Intelligence with #Python: https://t.co/AxvPhG7Jep by @prateekvjoshi \n\n#abdsc #BigData #DataScience #AI #…",
	"source" : "<a href=\"http://twitter.com/download/iphone\" rel=\"nofollow\">Twitter for iPhone</a>",
	"truncated" : false,
	"in_reply_to_status_id" : null,
	"in_reply_to_status_id_str" : null,
	"in_reply_to_user_id" : null,
	"in_reply_to_user_id_str" : null,
	"in_reply_to_screen_name" : null,
	"user" : {
		"id" : NumberLong("2231464708"),
		"id_str" : "2231464708",
		"name" : "Barbara A.Zielonka",
		"screen_name" : "bar_zie",
		"location" : "Norway",
		"url" : "https://bethechangetakethechallenge.wordpress.com/",
		"description" : "learner/global educator/traveller/co-author of Skills/ ESL/reader/techie/foodie/minimalist/pacifist/PD/BYOD/e-learning/edtech/#TeachSDGs Ambassador/Top 10 GTP",
		"translator_type" : "none",
		"protected" : false,
		"verified" : false,
		"followers_count" : 11441,
		"friends_count" : 12545,
		"listed_count" : 3087,
		"favourites_count" : 91336,
		"statuses_count" : 227877,
		"created_at" : "Wed Dec 18 10:18:07 +0000 2013",
		"utc_offset" : null,
		"time_zone" : null,
		"geo_enabled" : false,
		"lang" : "en",
		"contributors_enabled" : false,
		"is_translator" : false,
		"profile_background_color" : "C0DEED",
		"profile_background_image_url" : "http://abs.twimg.com/images/themes/theme1/bg.png",
		"profile_background_image_url_https" : "https://abs.twimg.com/images/themes/theme1/bg.png",
		"profile_background_tile" : false,
		"profile_link_color" : "1DA1F2",
		"profile_sidebar_border_color" : "C0DEED",
		"profile_sidebar_fill_color" : "DDEEF6",
		"profile_text_color" : "333333",
		"profile_use_background_image" : true,
		"profile_image_url" : "http://pbs.twimg.com/profile_images/963667136106426368/atixwqb4_normal.jpg",
		"profile_image_url_https" : "https://pbs.twimg.com/profile_images/963667136106426368/atixwqb4_normal.jpg",
		"profile_banner_url" : "https://pbs.twimg.com/profile_banners/2231464708/1398248214",
		"default_profile" : true,
		"default_profile_image" : false,
		"following" : null,
		"follow_request_sent" : null,
		"notifications" : null
	},
	"geo" : null,
	"coordinates" : null,
	"place" : null,
	"contributors" : null,
	"retweeted_status" : {
		"created_at" : "Sun May 06 05:00:31 +0000 2018",
		"id" : NumberLong("992992484866260993"),
		"id_str" : "992992484866260993",
		"text" : "[Book] Artificial Intelligence with #Python: https://t.co/AxvPhG7Jep by @prateekvjoshi \n\n#abdsc #BigData… https://t.co/XirZ91jNrd",
		"display_text_range" : [
			0,
			140
		],
		"source" : "<a href=\"http://twitter.com/download/iphone\" rel=\"nofollow\">Twitter for iPhone</a>",
		"truncated" : true,
		"in_reply_to_status_id" : null,
		"in_reply_to_status_id_str" : null,
		"in_reply_to_user_id" : null,
		"in_reply_to_user_id_str" : null,
		"in_reply_to_screen_name" : null,
		"user" : {
			"id" : 534563976,
			"id_str" : "534563976",
			"name" : "Kirk Borne",
			"screen_name" : "KirkDBorne",
			"location" : "Booz Allen Hamilton",
			"url" : "http://www.linkedin.com/in/kirkdborne",
			"description" : "The Principal Data Scientist at @BoozAllen, PhD Astrophysicist. Top Data Science and Big Data Influencer. Ex-Professor http://rocketdatascience.org/ 📊📈🔭",
			"translator_type" : "none",
			"protected" : false,
			"verified" : true,
			"followers_count" : 195460,
			"friends_count" : 36731,
			"listed_count" : 7115,
			"favourites_count" : 142937,
			"statuses_count" : 85528,
			"created_at" : "Fri Mar 23 16:35:17 +0000 2012",
			"utc_offset" : -14400,
			"time_zone" : "Eastern Time (US & Canada)",
			"geo_enabled" : false,
			"lang" : "en",
			"contributors_enabled" : false,
			"is_translator" : false,
			"profile_background_color" : "C0DEED",
			"profile_background_image_url" : "http://pbs.twimg.com/profile_background_images/378800000110442114/094a0b4d38b70e3871a1bda7d7fe2341.jpeg",
			"profile_background_image_url_https" : "https://pbs.twimg.com/profile_background_images/378800000110442114/094a0b4d38b70e3871a1bda7d7fe2341.jpeg",
			"profile_background_tile" : true,
			"profile_link_color" : "0084B4",
			"profile_sidebar_border_color" : "FFFFFF",
			"profile_sidebar_fill_color" : "DDEEF6",
			"profile_text_color" : "333333",
			"profile_use_background_image" : true,
			"profile_image_url" : "http://pbs.twimg.com/profile_images/869301637269139458/3wIcLiQC_normal.jpg",
			"profile_image_url_https" : "https://pbs.twimg.com/profile_images/869301637269139458/3wIcLiQC_normal.jpg",
			"profile_banner_url" : "https://pbs.twimg.com/profile_banners/534563976/1521834569",
			"default_profile" : false,
			"default_profile_image" : false,
			"following" : null,
			"follow_request_sent" : null,
			"notifications" : null
		},
		"geo" : null,
		"coordinates" : null,
		"place" : null,
		"contributors" : null,
		"is_quote_status" : false,
		"extended_tweet" : {
			"full_text" : "[Book] Artificial Intelligence with #Python: https://t.co/AxvPhG7Jep by @prateekvjoshi \n\n#abdsc #BigData #DataScience #AI #MachineLearning #DeepLearning #NeuralNetworks #Algorithms #ComputerVision #NLProc #RecSys #PredictiveAnalytics #Coding https://t.co/bxVC29A6Ae",
			"display_text_range" : [
				0,
				241
			],
		},
		"quote_count" : 0,
		"reply_count" : 0,
		"retweet_count" : 4,
		"favorite_count" : 2,
		"favorited" : false,
		"retweeted" : false,
		"possibly_sensitive" : false,
		"filter_level" : "low",
		"lang" : "en"
	},
	"is_quote_status" : false,
	"quote_count" : 0,
	"reply_count" : 0,
	"retweet_count" : 0,
	"favorite_count" : 0,
	"favorited" : false,
	"retweeted" : false,
	"possibly_sensitive" : false,
	"filter_level" : "low",
	"lang" : "en",
	"timestamp_ms" : NumberLong("1525583372790"),
	"relevant" : 0
}
```

#### arXiv Data

arXiv data does not contain full PDF of the papers; only the matadata.

An example of arXiv data:

```json
{
    "id" : "arXiv:1805.01963v1",
    "url" : "http://arxiv.org/abs/1805.01963v1",
    "updated" : "2018-05-04T23:21:15Z",
    "published" : "2018-05-04T23:21:15Z",
    "title" : "MTFH: A Matrix Tri-Factorization Hashing Framework for Efficient\n  Cross-Modal Retrieval",
    "summary" : "Hashing has recently sparked a great revolution in cross-modal retrieval due to its low storage cost and high query speed. Most existing cross-modal hashing methods learn unified hash codes in a common Hamming space to represent all multi-modal data and make them intuitively comparable. However, such unified hash codes could inherently sacrifice their representation scalability because the data from different modalities may not have one-to-one correspondence and could be stored more efficiently by different hash codes of unequal lengths. To mitigate this problem, this paper proposes a generalized and flexible cross-modal hashing framework, termed Matrix Tri-Factorization Hashing (MTFH), which not only preserves the semantic similarity between the multi-modal data points, but also works seamlessly in various settings including paired or unpaired multi-modal data, and equal or varying hash length encoding scenarios. Specifically, MTFH exploits an efficient objective function to jointly learn the flexible modality-specific hash codes with different length settings, while simultaneously excavating two semantic correlation matrices to ensure heterogeneous data comparable. As a result, the derived hash codes are more semantically meaningful for various challenging cross-modal retrieval tasks. Extensive experiments evaluated on public benchmark datasets highlight the superiority of MTFH under various retrieval scenarios and show its very competitive performance with the state-of-the-arts.",
    "author" : [
        "Xin Liu",
        "Zhikai Hu",
        "Haibin Ling",
        "Yiu-ming Cheung"
    ],
    "primaryCategory" : "cs.CV",
    "category" : [
        "cs.CV"
    ],
    "timestamp_ms" : NumberLong("1525501275000")
}
```

You may see an extra `text` field in some records - that's the same as `summary`. A legacy issue in our system created this extra field.

### License

CC-4.0-BY
