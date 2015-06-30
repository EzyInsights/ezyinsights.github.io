---
---
Endpoints
=========

GET /stories
------------

Get all stories from EzyRealtime.

The results can be filtered with these parameters:

### Parameters

`datefrom` | `long` | Specifies the beginning [Unix Timestamp](https://en.wikipedia.org/wiki/Unix_time) of the results.
`dateto` | `long` | Specifies the ending [Unix Timestamp](https://en.wikipedia.org/wiki/Unix_time) of the results.
`country` | `string` | Filters results to the specified countries. Country codes follow the [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) standard. Specify multiple values by separating each value with a comma. e.g `US,GB,SE,FI`
`categories` | `string` |  Filters results to the specified categories. Valid values are: `NEW` (General News), `VIR` (Viral News), `TAB` (Tabloids), `BUS` (Business News), `SPO` (Sport), `RAD` (Radio Stations), `MAG` (Magazines), `LIF` (Lifestyle), `ENT` (Entertainment), `TEC` (Technology), `FOO` (Food) `TEL` (Television), `CLA` (Classifieds) `TRA` (Travel) and `EME` (Emergency Services). Specify multiple values by separating each value with a comma e.g. `NEW,VIR,SPO`
`languages` | `string` | Filters results to the specified languages. Language codes follow the [ISO 639-1 alpha-2](https://en.wikipedia.org/wiki/ISO_639) standard. Specify multiple values by separating each value with a comma. e.g. `en,sv,fi`
`content` | `string` | Filters contents to the specified content type. Valid values are `link`,`video` and `photo`. Specify multiple values by separating each value with a comma e.g. `link,video`
`itemtype` | `string` | Filters contents to the specified item type. Valid values are `NOTPOSTED`, `UNPOSTED` and `ALL`. Only one item type value can be specified.
`order` | `string` | Determines the order that the results are returned. Valid values are `SPEED`, `ENGAGEMENT` and `TIME`. Only one order value can be specified.
`threshold` | `double` | Speed threshold that each item must meet to be included.
`ignore`| `string` | Filters results to ignore stories sourced from specific publishers. Specify multiple values by separating each value with a comma.
`onlyshow`| `string` | Filters results to only return the stories sourced from specific publishers. Specify multiple values by separating each value with a comma.
`limit` | `integer` | The number of stories to return.
`offset` | `integer` | Where to start from. Used if paging is required.
`normalise` | `boolean` | Normalises story ranking by taking into account the engagement received against the source's fan base.

### Results
The results are returned in **JSON**. Each value returned is described in the sections below.

### Example Request

    $ curl https://realtime.ezyinsights.com
        /api/v1.0/stories
        ?datefrom=12312312
        &dateto=134123121
        &countries=SE,FI
        &order=SPEED

### Example Response
    [
      "story_id": "awrs3a",
      "canonical_url": "https://example.com/link_name_of_the_story.html",
      "headline": "The Sensational Headline of this Story!",
      "picture_url": "https://example.com/image.png",
      "description": "A paragraph about this story. Sometimes more than one sentence.",
      "published_date": 1231213121,
      "endorsed_date": 1231213121,
      "as_at": 1212313111,
      "media_type": "link,video",
      "engagement": 123115,
      "publisher_source": {
        "country": "SE",
        "category": "NEW",
        "language": "sv",
        "logo_url": "https://example.com/image.png"
      },
      "social_media_posts": {
        "total": 10,
        "facebook": 3,
        "twitter": 7
      },
      "extended_engagement": {
        "total": 1214311,
        "facebook": 12214,
        "twitter": 212,
        "linkedin": 24,
      }
      "cumulative_speed": {
        "last_hour": 121.456573,
        "lifetime": 34.225114
      }
    ],
    ...

#### Publisher Source
Name | Type | Description
---- | ---- | -----------
`country` | `string` |  The country code of the publisher source in [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) format.
`category` | `string` | The category of this publisher source (see the parameter 'categories' for a list of valid category values).
`language` | `string` | The language code of the publisher source in [ISO 639-1 alpha-2](https://en.wikipedia.org/wiki/ISO_639) format.
`logo url` | `string` | The URL to the logo image file associated with this publisher.

#### Story
Name | Type | Description
---- | ---- | -----------
`story_id` | `string` | The unique identifier for this story. This id is used to access additional results from other API endpoints.
`canonical_url` | `string` | The [canonical](https://en.wikipedia.org/wiki/Canonical_link_element) URL of the story.
`headline` | `string` | Short text indicating the [nature of the contents](https://en.wikipedia.org/wiki/Headline) of this story.
`picture_url` | `string` | The URL to the image file associated with this story.
`description` | `string` | A short paragraph indicating the jist of the story.
`published_date` | `long` | The [Unix Timestamp](https://en.wikipedia.org/wiki/Unix_time) of when the story was published to the website.
`endorsed_date` | `long` | The [Unix Timestamp](https://en.wikipedia.org/wiki/Unix_time) of the most recent action that occured to this story. For example, it may be the published time of the story or when the most recent post to social media was made about this story. This is the date that is used by the `datefrom` and `dateto` parameters.
`as_at` | `long` |  The [Unix Timestamp](https://en.wikipedia.org/wiki/Unix_time) indicating when the call to this endpoint was made.
`media_type` | `string` | Specifys the type of story i.e. if the story is a `link`, `photo` or `video`
`engagement` | `integer` | All engagement received on this story so far from all social media channels.

#### Social Media Posts
Name | Type | Description
---- | ---- | -----------
`total` | `integer` | The total number of social media posts made by publishers about this story on all social media channels.
`facebook` | `integer` | The number of social media posts made by publishers about this story on Facebook.
`linkedin` | `integer` | The number of social media posts made by publishers about this story on LinkedIn.
`pinterst` | `integer` | The number of social media posts made by publishers about this story on Pinterest.
`twitter` | `integer` | The number of social media posts made by publishers about this story on Twitter.

#### Extended Engagement
Name | Type | Description
---- | ---- | -----------
`total` | `integer` | The total amount of extended engagement received by this story on all social media channels.
`facebook` | `integer` | All extended engagement received by this story on Facebook.
`linkedin` | `integer` | All extended engagement received by this story on LinkedIn.
`pinterst` | `integer` | All extended engagement received by this story on Pinterest.
`twiter` | `integer` | All extended engagement received by this story on Twitter.

#### Cumulative Speed
Name | Type | Description
---- | ---- | -----------
`last_hour` | `double` | The engagements per minute of this story within the last hour.
`lifetime` | `double` | The engagements per minute of this story over it's whole lifetime.


GET /socialmediaposts
---------------------

Get the social media posts made for a story.

### Parameters

Name | Type | Description
------------ | ------------- | ------------
`storyid` | `string` | The unique identifier for a story (obtained from the stories endpoint).

### Results
The results are returned in **JSON**. Each value returned is described in the sections below.

### Example Request

    $ curl https://realtime.ezyinsights.com
        /api/v1.0/socialmediaposts
        ?storyid=asdas3f

### Example Response
      {
        "as_at": 1212313111,
        "facebook_posts": [
          {
            "story_id": "awrs3a",
            "post_id": "123456789_1234567",
            "post_date": 1231213121,
            "caption": "What the person who made this post says about it",
            "likes": 134,
            "shares": 23,
            "comments": 54,
            "speed": {
              "last_hour": 121.456573,
              "lifetime": 34.225114
            },
            ...
        ]
      }

#### Social Media Posts
Name | Type | Description
---- | ---- | -----------
`as_at` | `long` |  The [Unix Timestamp](https://en.wikipedia.org/wiki/Unix_time) indicating when the call to this endpoint was made.


#### Facebook Posts
Name | Type | Description
---- | ---- | -----------
`storyid` | `string` | The story id that this post is made about.
`post_id` | `string` | The Facebook post id for this post.
`post_date` | `long` | The [Unix Timestamp](https://en.wikipedia.org/wiki/Unix_time) of when the post was made on Facebook.
`caption` | `string` | The caption of this Facebook post.
`likes` | `integer` | How many likes this post has received until now.
`shares` | `integer` | How many shares this post has received until now.
`comments` | `integer` | How many comments this post has received until now.

#### Speed
Name | Type | Description
---- | ---- | -----------
`last_hour` | `double` | The engagements per minute of this social media post within the last hour.
`lifetime` | `double` | The engagements per minute of this social media post over it's whole lifetime.
